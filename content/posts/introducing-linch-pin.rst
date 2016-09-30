+++
date = "2016-09-28T10:56:43-06:00"
draft = true
title = "Introducing linch-pin: Simple hybrid cloud provisioning using Ansible"

+++
Background
----------

Over the past 6+ months, I've been working at `Red Hat <https://redhat.com>`_. During this time, I've been working mostly with Continuous Integration projects and the like. Recently, I joined a new team, called Continouous Infrastructure and started working on automating use cases around `Project Atomic <https://projectatomic.io>`_ and `OpenShift <https://openshift.com>`_.

As part of that project, we have an internal tool, called ci-factory. It has within its components, a provisioner that works with OpenStack, Beaker, docker? etc. However, it doesn't support a broader set of clouds/infrastructure, including Amazon AWS, Google Compute Engine, Libvirt, etc. Additionally, ci-factory provided some tooling for ansible dynamic inventories. However, the configurations that generated this were not very flexible, and sometimes outright incorrect.

Enter Provisioner 2.0 (linch-pin)
=====================================

The concept of linch-pin was to retool the basic ci-factory provisioner into something much more flexible. While provisioning was important, ci-factory was written in a mix of python and bash scripts. Provisioner 2.0 is written completely in Ansible. Because Ansible is excellent at both configuration management and orchestration of systems, it could be used to both provision and configure systems. Ansible can handle complex cluster configurations (eg `openshift-ansible <https://github.com/openshift/openshift-ansible>`_) as well as much simpler tasks, like adding users to a system idempotently.

Additional, considerations for Provisioner 2.0 would allow leveraging of existing Ansible cloud modules, reducing the amount of code needing to be written. So far, this has proven very valuable and made development time much shorter overall. There are, however certain modules, Libvirt for example, that seem poorly implemented in Ansible. Thus, an updated module will need to be written.

Lastly, Provisioner 2.0 should exist upstream. Linch-pin has been an upstream project since the first working code was created. This was done to encourage contribution from inside and outside of Red Hat. We believe that many projects will be able to take advantage of Linch-pin and contribute back to the project as a whole. Many other upstream and downstream projects have expressed interest in linch-pin just from a basic demonstration.

Linch-pin Architecture
----------------------

Linch-pin has some basic components that make it work.

Topologies and Provisioning
===========================

To consider complex cloud infrastructure, a topology definition can help. The topology definition is created using YAML. Before linch-pin provisions anything, the topology must be validated using a predefined schema. Schemas can be created to change the way the topology works if desired. However, there is a default schema already defined for simplicity.

After validation, the topology is then used to provision resources. This is done by the topology provisioner process. Essentially, a topology is broken into its resource components, and each is delegated to the appropriate resource provisioner. This is generally done asynchronously, meaning that nodes on different cloud providers can be provisioned at the same time using appropriate credentials. Assuming a successful provisioning event per provider, the resource provisoner(s) will return appropriate response data to the topology provisioner.

As mentioned above, credentials may be required for some cloud providers. This is handled by the credentials manager. The credentials details are stored in the topology definition as a reference to the vault/location of said credentials. The resource provisioner uses these to authenticate to the appropriate cloud provider as necessary.

A very simple example topology definition is provided here. More complex examples can be found in the `linch-pin github repository <https://github.com/CentOS-PaaS-SIG/linch-pin>`_.
