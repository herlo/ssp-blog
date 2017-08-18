+++
date = "2017-06-30 08:56:43-06:00"
draft = false
title = "LinchPin v1.0: Simplified Cloud Orchestration with Ansible"
series = ["linch-pin"]
tasks = [
]

+++

Late last year, we announced `LinchPin <http://sexysexypenguins.com/posts/introducing-linch-pin/>`_, a hybrid cloud orchestration tool using Ansible. Provisioning cloud resources has never been easier or faster. With the power of Ansible behind LinchPin, many cloud resources are available at users' fingertips. In this article, I'll introduce LinchPin and look at how the project has matured in the past 10 months.

Back when LinchPin was introduced, using the ansible-playbook command to run LinchPin was complex. Although that can still be accomplished, LinchPin now has a new front-end command-line user interface (CLI), which is written using `Click <http://click.pocoo.org/>`_ which makes LinchPin even simpler than it was before.

Not to be outdone by the CLI, LinchPin now also has a Python API, which can be used to manage resources, such as Amazon EC2 and OpenStack instances, networks, storage, security groups, and more. The API `documentation <http://linchpin.readthedocs.io/en/develop/libdocs.html>`_ can be helpful when you're trying out LinchPin's Python API.

Playbooks as a Library
======================

Because the core bits of LinchPin are Ansible Playbooks, the roles, modules, filters, and anything else to do with calling Ansible modules has been moved into the LinchPin library. What this means is that while one can still call the playbooks directly, it's not the preferred mechanism for managing resources. The ``linchpin`` executable has become the de facto front end for the command-line.

Command-Line In Depth
=====================

Let's have a look at the ``linchpin`` command in depth.

.. code-block:: bash

    $ linchpin
    Usage: linchpin [OPTIONS] COMMAND [ARGS]...

      linchpin: hybrid cloud orchestration

    Options:
      -c, --config PATH       Path to config file
      -w, --workspace PATH    Use the specified workspace if the familiar Jenkins
                              $WORKSPACE environment variable is not set
      -v, --verbose           Enable verbose output
      --version               Prints the version and exits
      --creds-path PATH       Use the specified credentials path if WORKSPACE
                              environment variable is not set
      -h, --help              Show this message and exit.

    Commands:
      init     Initializes a linchpin project.
      up       Provisions nodes from the given target(s) in...
      destroy  Destroys nodes from the given target(s) in...

What can be seen immediately is a simple description, along with options and arguments that can be passed to the command. The three commands found near the bottom of this help are where the focus will be for this document.

Configuration
-------------

In the past, there was `linchpin_config.yml`. This file is no longer, and has been replaced with an ini-style configuration file, called `linchpin.conf`. While this file can be modified, or placed elsewhere, it's placement in the library path allows easy lookup of configurations. `linchpin.conf` file should not need to be modified in most cases.

Workspaces
----------

The workspace is a defined filesystem path, which allows grouping of resources in a logical way. A workspace can be considered a single point for a particular environment, set of services, or some other logical grouping. It can also be just one big storage bin of all managed resources.

The workspace can be specified on the command line with the ``--workspace (-w)`` option, followed by the workspace path. It can also be specified with an environment variable. (eg. ``$WORKSPACE`` in bash). The default workspace is the current directory.

Initialization (init)
---------------------

Running ``linchpin init`` will generate the directory structure needed, along with an example `PinFile`, `topology`, and `layout` files.

.. code-block:: bash

    $ export WORKSPACE=/tmp/workspace
    $ linchpin init
    PinFile and file structure created at /tmp/workspace
    $ cd /tmp/workspace/
    $ tree
    .
    ├── credentials
    ├── hooks
    ├── inventories
    ├── layouts
    │   └── example-layout.yml
    ├── PinFile
    ├── resources
    └── topologies
        └── example-topology.yml

At this point, one could execute ``linchpin up`` and provision a single libvirt virtual machine, with a network named `linchpin-centos71`. An inventory would be generated and placed in ``inventories/libvirt.inventory``. This can be known by reading the ``topologies/example-topology.yml`` and gleaning out the `topology_name` value.

Provisioning (linchpin up)
--------------------------

Once a PinFile, topology, and optionally a layout are in place, provisioning can happen.

.. note:: We use the dummy tooling as it is much simpler to configure. It
    doesn't require anything extra (authentication, network, etc.). The dummy
    provider creates a temporary file, which represents provisioned hosts.
    If the temporary file does not have any data, hosts have not been
    provisioned, or they have been recently destroyed.

The tree for the dummy provider is very simple.

.. code-block:: bash

    $ tree
    .
    ├── hooks
    ├── inventories
    ├── layouts
    │   └── dummy-layout.yml
    ├── PinFile
    ├── resources
    └── topologies
        └── dummy-cluster.yml

The PinFile is also very simple. It specifies which topology, and optional layout to use for the ``dummy1`` target.

.. code-block:: yaml

    ---
    dummy1:
      topology: dummy-cluster.yml
      layout: dummy-layout.yml

The ``dummy-cluster.yml`` topology file is a reference to provision three (3) resources of type `dummy_node`.

.. code-block:: yaml

    ---
    topology_name: "dummy_cluster" # topology name
    resource_groups:
      -
        resource_group_name: "dummy"
        resource_group_type: "dummy"
        resource_definitions:
          -
            name: "web"
            type: "dummy_node"
            count: 3


Performing the command ``linchpin up`` should generate `resources` and `inventory` files based upon the `topology_name`. In this case, is ``dummy_cluster``.

.. code-block:: bash

    $ linchpin up
    target: dummy1, action: up

    $ ls {resources,inventories}/dummy*
    inventories/dummy_cluster.inventory  resources/dummy_cluster.output

To verify resources with the dummy cluster, check ``/tmp/dummy.hosts``

.. code-block:: bash

    $ cat /tmp/dummy.hosts
    web-0.example.net
    web-1.example.net
    web-2.example.net

.. note:: The Dummy module provides a very basic tooling for pretend (or dummy) provisioning. Check out the details for openstack, AWS EC2, google cloud, and more in the LinchPin `examples <https://github.com/CentOS-PaaS-SIG/linchpin/tree/develop/linchpin/examples/topologies>`_.

Inventory Generation
--------------------

As part of the PinFile mentioned above, a `layout` can be specified. If this file is specified and exists in the correct location, an Ansible static inventory file will be generated automatically for the resources provisioned.

.. code-block:: yaml

    ---
    inventory_layout:
      vars:
        hostname: __IP__
      hosts:
        example-node:
          count: 3
          host_groups:
            - example

When the ``linchpin up`` execution is complete, the resources file provides useful details. Specifically, the IP address(es) or host name(s) are interpolated into the static inventory.

.. code-block:: cfg

    [example]
    web-2.example.net hostname=web-2.example.net
    web-1.example.net hostname=web-1.example.net
    web-0.example.net hostname=web-0.example.net

    [all]
    web-2.example.net hostname=web-2.example.net
    web-1.example.net hostname=web-1.example.net
    web-0.example.net hostname=web-0.example.net


Teardown (linchpin destroy)
---------------------------

LinchPin can also perform a teardown of resources.  A teardown action generally expects that resources have been provisioned; however, because Ansible is idempotent, ``linchpin destroy`` will only check to make sure the resources are up.  Only if the resources are already up will the teardown happen.

The command ``linchpin destroy`` will either use resources and/or topology files to determine the proper teardown procedure.

.. note:: The `dummy` Ansible role does not use the resources, only the topology during teardown.

.. code-block:: bash

    $ linchpin destroy
    target: dummy1, action: destroy

    $ cat /tmp/dummy.hosts
    -- EMPTY FILE --


.. note:: The teardown functionality is slightly more limited around ephemeral
    resources, like networking, storage, etc. It is possible that a network
    resource could be used with multiple cloud instances. In this way,
    performing a ``linchpin destroy`` does not teardown certain resources. This
    is dependent on each providers implementation.
    See specific implementations for each of the `providers
    <https://github.com/CentOS-PaaS-SIG/linch-pin/tree/develop/linchpin/provision/roles>`_.

The LinchPin Python API
=======================

Much of what is implemented in the ``linchpin`` command-line tool has been written using the Python API. The API, while not complete, has become a vital component of the LinchPin tooling.

The API consists of three packages:

* linchpin
* linchpin.cli
* linchpin.api

The command-line tool is managed at the base `linchpin` package. It imports the `linchpin.cli` modules and classes, which subclasses `linchpin.api`. The purpose for this is to allow for other possible implementations of LinchPin using the `linchpin.api`, like a planned RESTful API.

For more information see the `Python API library documentation on readthedocs <http://linchpin.readthedocs.io/en/develop/libdocs.html>`_.

Hooks
=====

One of the big improvements in LinchPin 1.0 going forward is hooks. The goal with hooks is to allow additional configuration using external resources in certain specific states during linchpin execution. The states currently are as follows:

* preup - executed before provisioning the topology resources
* postup - executed after provisioning the topology resources, and generating the optional inventory
* predestroy - executed before teardown of the topology resources
* postdestroy - executed after teardown of the topology resources

In each case, these hooks allow external scripts to run. Several types of hooks exist, including custom ones. These are called Action Managers. Here's a list of built-in Action Managers.

* shell - Allows either inline shell commands, or an executable shell script
* python - Executes a python script
* ansible - Executes an Ansible playbook, allowing passing of a `vars_file` and `extra_vars` represented as a python dict
* nodejs - Executes a nodejs script
* ruby - Executes a ruby script

.. note:: A hook is bound to a specific target, and must be restated for each target used. In the future, hooks will be able to be global, and then named in the `hooks` section for each target more simply.

Using Hooks
-----------

Because it's simple enough to describe hooks, it might not be that simple to understand their power. The reason this feature exists is to provide flexible power to the user for things that the LinchPin developers might not consider. This concept could lead to a simple way to ping a set of systems, for instance, before running another hook.

Looking into the 'workspace` more closely, one might have noticed the `hooks` directory. Let's have a look inside this directory to see the structure.

.. code-block:: bash

    $ tree hooks/
    hooks/
    ├── ansible
    │   ├── ping
    │   │   └── dummy_ping.yaml
    └── shell
        └── database
            ├── init_db.sh
            └── setup_db.sh

In every case, hooks can be used in the `PinFile`, shown here.

.. code-block:: yaml

    ---
    dummy1:
      topology: dummy-cluster.yml
      layout: dummy-layout.yml
      hooks:
        postup:
          - name: ping
            type: ansible
            actions:
              - dummy_ping.yaml
          - name: database
            type: shell
            actions:
              - setup_db.sh
              - init_db.sh


The basic concept here would be that there are three postup actions to complete. Hooks are executed in top-down order. Thus, the ansible `ping` task would run first, followed by the two shell tasks, `setup_db.sh`, followed by `init_db.sh`. Assuming the hooks execute successfully, a ping of the systems would occur, then a database would be setup, and initialized.

Authentication Driver
=====================

In the initial design of LinchPin, it was determined to have authentication be managed within the ansible playbooks. However, moving to a more API and command-line driven tool meant that authentication should really be outside of the library where the playbooks now reside, and still pass authentication values along as needed.

Configuration
-------------

To accomplish this task, it was determined that the easiest thing to do for a user was to let them use the authentication method provided by the driver used. For instance, if the topology called for openstack, the standard method is to use either a yaml file, or similar `OS_` prefixed environment variables. A clouds.yaml file consists of a profile, with an `auth` section.

.. code-block:: yaml

    clouds:
      default:
        auth:
          auth_url: http://stack.example.com:5000/v2.0/
          project_name: factory2
          username: factory-user
          password: password-is-not-a-good-password

.. note:: More detail in the `openstack documentation <https://docs.openstack.org/developer/python-openstackclient/configuration.html>`_

This clouds.yaml, or any other authentication file, is located in the `default_credentials_path` (eg. ~/.config/linchpin) and referenced in the topology.


.. code-block:: yaml

    ---
    topology_name: openstack-test
    resource_groups:
      -
        resource_group_name: linchpin
        resource_group_type: openstack
        resource_definitions:
          - name: resource
            type: os_server
            flavor: m1.small
            image: rhel-7.2-server-x86_64-released
            count: 1
            keypair: test-key
            networks:
              - test-net2
            fip_pool: 10.0.72.0/24
        credentials:
          filename: clouds.yaml
          profile: default

.. note:: The `default_credentials_path` can be changed by modifying the linchpin.conf

The topology includes a new `credentials` section at the bottom. With `openstack`, `ec2`, and `gcloud` modules, the credentials can be specified similarly. The Authentication driver, will then look in the given 'filename' `clouds.yaml`, and search for the 'profile' named `default`.

Assuming authentication is found and loaded, provisioning will continue as normal.

Simplicity
==========

Although LinchPin can be complex around topologies, inventory layouts, hooks, and authentication management, the ultimate goal is simplicity. By simplifying with a command-line interface, along with goals to improve the developer experience coming post-1.0, LinchPin continues to show that complex configurations can be managed with simplicity.

Community Growth
================

Over the past year, LinchPin's community has grown. To the point that we now have a `mailing list <https://www.redhat.com/mailman/listinfo/linchpin>`_, an IRC channel (#linchpin on chat.freenode.net), and even manage our sprints in the open with `GitHub <https://github.com/CentOS-PaaS-SIG/linch-pin/projects/4>`_.

The community membership has grown immensely. From 2 core developers to about 10 contributors over the past year. More people continue to work with the project. The future is bright for sure! If you've got an interest, drop us a line, file an issue on github, join up on IRC, or send us an email.


Cheers,

herlo


PS - This article is crossposted on `Opensource.com <https://opensource.com/article/17/6/linchpin>`_. Special thanks to Rikki Endsley and Jen Wike Huger for helping it get published!

