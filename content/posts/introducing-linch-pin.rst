+++
date = "2016-10-19T10:56:43-06:00"
draft = false
title = "Introducing Linch-Pin: Hybrid cloud provisioning using Ansible"
series = ["Linch-Pin"]
tasks = [
    'Write up more about the credentials',
    'Update/document linchpin_config.yml variables',
    'Cover filter_plugins, InventoryFilters, modules/library'
]

+++
Background
----------

Over the past 6+ months, I've been working at `Red Hat <https://redhat.com>`_. During this time, I've been working mostly with Continuous Integration projects and the like. Recently, I joined a new team, called Continouous Infrastructure and started working on automating use cases around `Project Atomic <https://projectatomic.io>`_ and `OpenShift <https://openshift.com>`_.

As part of that project, we have an internal tool, called ci-factory. It has within its components, a provisioner that works with OpenStack, Beaker, etc. However, it doesn't support a broader set of clouds/infrastructure, including Amazon AWS, Google Compute Engine, Libvirt, etc. Additionally, ci-factory provided some tooling for ansible dynamic inventories. However, the configurations that generated this were not very flexible, and sometimes outright incorrect.

Enter Provisioner 2.0 (Linch-Pin)
=====================================

Beginning in June this year, our team started creating a new tool. Lead by developer extraordinaire, `Samvaran Rallabandi <https://github.com/samvarankashyap>`_ (we call him SK), we now have `Linch-Pin <https://github.com/CentOS-PaaS-SIG/linch-pin>`_.

The concept of Linch-Pin was to retool the basic ci-factory provisioner into something much more flexible. While provisioning was important, ci-factory was written in a mix of python and bash scripts. Provisioner 2.0 is written completely in Ansible. Because Ansible is excellent at both configuration management and orchestration of systems, it could be used to both provision and configure systems. Ansible can handle complex cluster configurations (eg `openshift-ansible <https://github.com/openshift/openshift-ansible>`_) as well as much simpler tasks, like adding users to a system idempotently.

Additional, considerations for Provisioner 2.0 would allow leveraging of existing Ansible cloud modules, reducing the amount of code needing to be written. So far, this has proven very valuable and made development time much shorter overall. There are, however certain modules, Libvirt for example, that seem poorly implemented in Ansible. Thus, an updated module will need to be written.

Lastly, Provisioner 2.0 should exist upstream. Linch-Pin has been an upstream project since the first working code was created. This was done to encourage contribution from inside and outside of Red Hat. We believe that many projects will be able to take advantage of Linch-Pin and contribute back to the project as a whole. Many other upstream and downstream projects have expressed interest in Linch-Pin just from a basic demonstration.

Linch-Pin Architecture
----------------------

Linch-Pin has some basic components that make it work. First we'll cover the file structure, then dive into the core bits::

    provision/
    ├── group_vars/
    ├── hosts
    ├── roles/
    └── site.yml

At one point in time, Linch-Pin was going to have both `provision` and `configure` playbooks. The provision components became Linch-Pin, while the configure components became external repositories of useful components which leverage Linch-Pin in some way. A couple of examples are the CentOS PaaS SIG's `paas-sig-ci project <https://github.com/CentOS-PaaS-SIG/paas-sig-ci>`_, and the `cinch project <https://github.com/RedHatQE/cinch>`_, by, Red Hat Quality Engineering.

Both `group_vars` and `hosts` paths are related to `inventory <https://docs.ansible.com/ansible/intro_inventory.html>`_.

The `roles` path is the meat of Linch-Pin. All of the power that makes hybrid cloud provisioning possible exists here. Ansible defines things called `playbooks <https://docs.ansible.com/ansible/playbooks.html>`_ to drive these roles.  The `site.yml` is the playbook itself, which start the execution.

Other paths exist::

    ├── outputs/
    ├── filter_plugins/
    ├── InventoryFilters/
    └── library/

We will cover these components later on in this post, or later in the series.

Topologies
==========

To consider complex cloud infrastructure, a topology definition can help. The topology definition is created using YAML. Before Linch-Pin provisions anything, the topology must be validated using a predefined schema. Schemas can be created to change the way the topology works if desired. However, there is a default schema already defined for simplicity.

After validation, the topology is then used to provision resources. A topology is broken into its resource components, and each is delegated to the appropriate resource provisioner. This is generally done asynchronously, meaning that nodes on different cloud providers can be provisioned at the same time using appropriate credentials. Assuming a successful provisioning event per provider, the resource provisoner(s) will return appropriate response data to the topology provisioner.

As mentioned above, credentials may be required for some cloud providers. This is handled by the credentials manager. The credentials details are stored in the topology definition as a reference to the vault/location of said credentials. The resource provisioner uses these to authenticate to the appropriate cloud provider as necessary.

A very simple example topology definition is provided here.

.. code-block:: yaml

   # openstack-3node-cluster.yml
   ---
   topology_name: "openstack_3node_cluster"
   site: "ci-osp"
   resource_groups:
     -
       resource_group_name: "os"
       res_group_type: "openstack"
       res_defs:
         -
           res_name: "3node_inst"
           flavor: "m1.small"
           res_type: "os_server"
           image: "rhel-7.3-server-x86_64-latest"
           count: 3
           networks:
             - "atomic-e2e-jenkins"
       assoc_creds: "openstack_creds"

This topology describes a single set of instances, which will run on the local *ci-osp* site. There will be 3 nodes, given network devices on the 'atomic-e2e-jenkins' network. Each instance will be of type 'm1.small'. Keep in mind, the openstack server must actually be configured and accept the above options. This is out of scope of this post, however.

Topology terminology explained:

* ``topology_name``: a reference point which Linch-Pin uses to track the nodes, networks, and other resources throughout provisioning and teardown
* ``resource_groups``: a set of resource definitions. One or many groups of nodes, storage, etc.
* ``res_group_type``: a predefined set of group types (eg. openstack, aws, gcloud, libvirt, etc.)
* ``res_defs``: A definition of a resource with its component attributes (flavor, image, count, region, etc.)
* ``res_type``: A predefined cloud resource name (eg. os_server, gcloud_gce, aws_ec2, os_heat)

As mentioned above, the topology describes the resources needed. When Linch-Pin is invoked, this file will be read and create the described systems. More information about topologies and structures is described in the `Linch-Pin documentation <https://linch-pin.readthedocs.io/en/latest/example_topologies.html>`_. More complex examples can be found in the `Linch-Pin github repository <https://github.com/CentOS-PaaS-SIG/linch-pin/tree/master/ex_topo>`_.

Provisioning
============

To provision the `openstack-3node-cluster.yml`, Linch-Pin currently uses the ``ansible-playbook`` command. There are many options available that can be passed as ``--extra-vars``, but here, we only show two: `state` and `topology`. Simply calling the provision playbook will provision resources::

    $ ansible-playbook /path/to/linch-pin/provision/site.yml \
    topology='/path/to/openstack-3node-cluster.yml' state=present"

.. note:: There are other --extra-vars options documented `here <https://github.com/CentOS-PaaS-SIG/linch-pin/blob/master/README.md>`_.

The diagram shows this process, the topology definition is provided to the provisioner, which then provisions the requested resources. Once provisioned, all cloud data is gathered and stored.

.. figure:: {{<siteurl>}}uploads/2016/10/Linch-Pin_Provision_Resources.png
   :target: {{<siteurl>}}uploads/2016/10/Linch-Pin_Provision_Resources.png
   :scale: 90%
   :alt: Click image to see full size

A great many things happen when this playbook is run. Let's have a look at the process in a bit more detail.

Determining Defaults
++++++++++++++++++++

Linch-Pin first discovers the needed configurations. Either from the ``--extra-vars`` as shown above, or from the `linchpin_config.yml <https://github.com/CentOS-PaaS-SIG/linch-pin/blob/master/linchpin_config.yml>`_. This determines the schema, topology, and some paths for outputs and the like (covered later in this post).

Schema Check
++++++++++++

Once everything is configured properly, a schema check is performed. This process is used to ensure the topology file matches up with the defined constraints. For example, there are specific resource types *(res_type)*, like os_server, aws_ec2, and gcloud_gce. Others, like libvirt, beaker, and docker are not yet implemented. The schema check ensures that further processing only occurs for resource types that are currently supported.

Provisioning Nodes
++++++++++++++++++

Once the schema check passes, the topology is provisioned with the cloud provider(s). In the example, there is only one, openstack, but there could be several clouds provisioned at once. The provisioner plugin is called for each cloud provider, credentials are passed along as needed. If all is successful, nodes will be provisioned according to the topology definition.

.. note:: Additional example topologies available at the `Linch-Pin github <https://github.com/CentOS-PaaS-SIG/linch-pin/tree/master/ex_topo>`_.

Determining Credentials
+++++++++++++++++++++++

It may not have been clear above, but when provisioning nodes from certain cloud providers, credentials are required. In the topology definition file, there is one line that indicates credentials::

     assoc_creds: "openstack_creds"

However, this doesn't really tell us anything. It turns out, each provisioner plugin has an ansible `role`. Each `role` contains some variables for determining how to connect to the cloud provider. For instance, with openstack, the ``roles/openstack/vars/openstack_creds.yml`` relates to our topology definition::

    --- # openstack credentials
    endpoint: "{{ lookup('env','OS_AUTH_URL') }}"
    project: "{{ lookup('env','OS_TENANT_NAME') }}"
    username: "{{ lookup('env','OS_USERNAME') }}"
    password: "{{ lookup('env','OS_PASSWORD') }}"

The openstack credentials currently come from environment variables. Simply export these variable to the shell and they will be picked up properly. From this point, openstack will grant access according to its policies. The environmental variables are used this way, where appropriate, for all cloud providers.

In the future, there will be a way to manage credentials a bit more succinctly. See https://github.com/CentOS-PaaS-SIG/linch-pin/issues/76 for updates.

Outputs and Teardown
++++++++++++++++++++

Teardown is fairly straightforward. The command is similar to provisioning. The main difference is `state=absent`, telling the provisioner to perform a teardown instead of provisioning a new resource::


    $ ansible-playbook /path/to/linch-pin/provision/site.yml \
    topology='/path/to/openstack-3node-cluster.yml' state=absent"

This process requires knowledge of the outputs, as mentioned previously. Outputs are tracked by a few variables in the linchpin_config.yml. Specifically, the `outputfolder_path` provides the location of the output, along with the filename, which is based upon the `topology_name`. 

Consider the following; `outputfolder_path=/tmp/outputs`, and `topology_name=openstack_3node_cluster`. From this, the output of provisioning would reside at `/tmp/outputs/openstack_3node_cluser.yml`.

The contents of this file may look something like this::

    aws_ec2_res: []
    duffy_res: []
    gcloud_gce_res: []
    os_server_res:
    -   _ansible_item_result: true
        _ansible_no_log: false
        changed: true
        id: f5832fcc-4e1b-442d-8be8-ba5e3783e7f2
        instance:
        - <endpoint>
        - <username>
        - <password>
        - <username>
        - present
        - rhel-6.5_jeos
        - <ssh-key-reference>
        - m1.small
        - <network>
        - testgroup2
        - ano_inst
        - 0
        invocation:
            module_args:
                api_timeout: 99999
                auth:
                    auth_url: VALUE_SPECIFIED_IN_NO_LOG_PARAMETER
                    password: VALUE_SPECIFIED_IN_NO_LOG_PARAMETER
                    project_name: VALUE_SPECIFIED_IN_NO_LOG_PARAMETER
                    username: VALUE_SPECIFIED_IN_NO_LOG_PARAMETER
                auth_type: null
                auto_ip: true
                availability_zone: null
                boot_from_volume: false
                boot_volume: null
                cacert: null
                cert: null
                cloud: null
                config_drive: false
                endpoint_type: public
                flavor: m1.small
                flavor_include: null
                flavor_ram: null
                floating_ip_pools: null
                floating_ips: null
                image: rhel-6.5_jeos
                image_exclude: (deprecated)
                key: null
                key_name: <ssh-key-reference>
                meta: null
                name: testgroup2_ano_inst_0
                network: VALUE_SPECIFIED_IN_NO_LOG_PARAMETER
                nics: []
                region_name: null
                scheduler_hints: null
                security_groups:
                - default
                state: present
                terminate_volume: false
                timeout: 180
                userdata: null
                verify: true
                volume_size: false
                volumes: []
                wait: true
            module_name: os_server
        openstack:
            HUMAN_ID: true
            NAME_ATTR: name
            OS-DCF:diskConfig: MANUAL
            OS-EXT-AZ:availability_zone: nova
            OS-EXT-STS:power_state: 1
            OS-EXT-STS:task_state: null
            OS-EXT-STS:vm_state: active
            OS-SRV-USG:launched_at: '2016-07-26T16:56:40.000000'
            OS-SRV-USG:terminated_at: null
            accessIPv4: 10.8.183.233
            accessIPv6: ''
            addresses:
                <network>:
                -   OS-EXT-IPS-MAC:mac_addr: fa:16:3e:48:cf:fb
                    OS-EXT-IPS:type: fixed
                    addr: 172.16.100.26
                    version: 4
                -   OS-EXT-IPS-MAC:mac_addr: fa:16:3e:48:cf:fb
                    OS-EXT-IPS:type: floating
                    addr: 10.8.183.233
                    version: 4
            adminPass: <redacted>
            az: nova
            cloud: defaults
            config_drive: ''
            created: '2016-07-26T16:56:10Z'
            flavor:
                id: '2'
                name: m1.small
            hostId: 6363c13fc31066a15f2ff4c81bf054290d4d56d4d08e568570354580
            human_id: testgroup2_ano_inst_0
            id: f5832fcc-4e1b-442d-8be8-ba5e3783e7f2
            image:
                id: 3bcfd17c-6bf0-4134-ae7f-80bded8b46fd
                name: rhel-6.5_jeos
            interface_ip: 10.8.183.233
            key_name: <ssh-key-reference>
            metadata: {}
            name: testgroup2_ano_inst_0
            networks:
                <network>:
                - 172.16.100.26
                - 10.8.183.233
            os-extended-volumes:volumes_attached: []
            private_v4: 172.16.100.26
            progress: 0
            public_v4: 10.8.183.233
            public_v6: ''
            region: ''
            security_groups:
            -   description: Default security group
                id: df1a797b-009c-4685-a7c9-43863c36d653
                name: default
                security_group_rules:
                -   direction: ingress
                    ethertype: IPv4
                    id: ade9fcb9-14c1-4975-a04d-6007f80005c1
                    port_range_max: null
                    port_range_min: null
                    protocol: null
                    remote_ip_prefix: null
                    security_group_id: df1a797b-009c-4685-a7c9-43863c36d653
                -   direction: ingress
                    ethertype: IPv4
                    id: d03e4bae-24b6-415a-a30c-ee0d060f566f
                    port_range_max: null
                    port_range_min: null
                    protocol: null
                    remote_ip_prefix: null
                    security_group_id: df1a797b-009c-4685-a7c9-43863c36d653
            status: ACTIVE
            tenant_id: f1dda47890754241a3e111f9b7394707
            updated: '2016-07-26T16:56:40Z'
            user_id: 9c770dbddda444799e627004fee26e0a
            volumes: []
        server:
            HUMAN_ID: true
            NAME_ATTR: name
            OS-DCF:diskConfig: MANUAL
            OS-EXT-AZ:availability_zone: nova
            OS-EXT-STS:power_state: 1
            OS-EXT-STS:task_state: null
            OS-EXT-STS:vm_state: active
            OS-SRV-USG:launched_at: '2016-07-26T16:56:40.000000'
            OS-SRV-USG:terminated_at: null
            accessIPv4: 10.8.183.233
            accessIPv6: ''
            addresses:
                <network>:
                -   OS-EXT-IPS-MAC:mac_addr: fa:16:3e:48:cf:fb
                    OS-EXT-IPS:type: fixed
                    addr: 172.16.100.26
                    version: 4
                -   OS-EXT-IPS-MAC:mac_addr: fa:16:3e:48:cf:fb
                    OS-EXT-IPS:type: floating
                    addr: 10.8.183.233
                    version: 4
            adminPass: <redacted>
            az: nova
            cloud: defaults
            config_drive: ''
            created: '2016-07-26T16:56:10Z'
            flavor:
                id: '2'
                name: m1.small
            hostId: 6363c13fc31066a15f2ff4c81bf054290d4d56d4d08e568570354580
            human_id: testgroup2_ano_inst_0
            id: f5832fcc-4e1b-442d-8be8-ba5e3783e7f2
            image:
                id: 3bcfd17c-6bf0-4134-ae7f-80bded8b46fd
                name: rhel-6.5_jeos
            interface_ip: 10.8.183.233
            key_name: <ssh-key-reference>
            metadata: {}
            name: testgroup2_ano_inst_0
            networks:
                <network>:
                - 172.16.100.26
                - 10.8.183.233
            os-extended-volumes:volumes_attached: []
            private_v4: 172.16.100.26
            progress: 0
            public_v4: 10.8.183.233
            public_v6: ''
            region: ''
            security_groups:
            -   description: Default security group
                id: df1a797b-009c-4685-a7c9-43863c36d653
                name: default
                security_group_rules:
                -   direction: ingress
                    ethertype: IPv4
                    id: ade9fcb9-14c1-4975-a04d-6007f80005c1
                    port_range_max: null
                    port_range_min: null
                    protocol: null
                    remote_ip_prefix: null
                    security_group_id: df1a797b-009c-4685-a7c9-43863c36d653
                -   direction: ingress
                    ethertype: IPv4
                    id: d03e4bae-24b6-415a-a30c-ee0d060f566f
                    port_range_max: null
                    port_range_min: null
                    protocol: null
                    remote_ip_prefix: null
                    security_group_id: df1a797b-009c-4685-a7c9-43863c36d653
            status: ACTIVE
            tenant_id: f1dda47890754241a3e111f9b7394707
            updated: '2016-07-26T16:56:40Z'
            user_id: 9c770dbddda444799e627004fee26e0a
            volumes: []

Because the `linchpin_config.yml` contains the path to the output file, it is then parsed and used to teardown the resources. In this case, the single openstack node listed and its networking resources are torn down. If there were more nodes, more data would exist. Similarly, if there were additional clouds, the data would be populated for the appropriate output fields.


Conclusion
==========

Finally! We've made it through the introduction to Linch-Pin. As you can see, running Linch-Pin is pretty easy, but there's a lot to it internally. Now it's time to use the provisioner, so go ahead and try it out.

Cheers,

herlo
