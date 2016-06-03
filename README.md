# iRODS
The Integrated Rule-Oriented Data System (iRODS) is an open source data management software used by research organizations and government agencies worldwide. This package contains Ansible scripts for installation and deployment of iRODS on a cluster of virtual machines. It also includes [Cloud Browser](https://github.com/DICE-UNC/irods-cloud-browser), which gets installed on the iCAT server.

![Alt text] (images/iRODS-Logo.png "iRODS")

## Requirements

[Ansible](https://www.ansible.com/), [Vagrant](https://www.vagrantup.com/), and access to one of the supported VM providers. This repository was made with Ansible 2.1, Vagrant 1.7.4, and Ubuntu 14.04 virtual machines.

## Configuration

Before starting the iRODS deployment, it's recommended that you generate some specific configuration keys.

Zone key:

    $ (openssl rand -base64 32 | sed 's,/,S,g' | sed 's,+,_,g' | cut -c 1-32 | tr -d '\n' ; echo "")

Negotiation key:

    $ openssl rand -base64 32 | sed 's,/,S,g' | sed 's,+,_,g' | cut -c 1-32

Control plane key:

    $ openssl rand -base64 32 | sed 's,/,S,g' | sed 's,+,_,g' | cut -c 1-32
    
Place new keys in the ``group_vars/all`` and make any other desired changes.

## Create Virtual Machines

Vagrantfiles have been provided in the appropriate folders for a number of VM providers. Choose one to launch your cluster with.

## Hosts File

Edit the ``hosts`` file in the same folder of the Vagrantfile you used.

## Start Deployment

Run the playbook:

    $ ansible-playbook -i <vm_provider>/hosts playbook.yml

## Test iRODS and Cloud Browser

If deployment finished successfully then the iRODS iCommands should be available on each node of the cluster and Cloud Browser should be available at ``https://<hostname_or_ip_of_icat>``

## iRODS use cases:

* iRODS enables data discovery using a metadata catalog that describes every file, every directory, and every storage resource in the data grid.
* iRODS automates data workflows, with a rule engine that permits any action to be initiated by any trigger on any server or client in the grid.
* iRODS enables secure collaboration, so users only need to log in to their home grid to access data hosted on a remote grid.
* iRODS implements data virtualization, allowing access to distributed storage assets under a unified namespace, and freeing organizations from getting locked in to single-vendor storage solutions.
