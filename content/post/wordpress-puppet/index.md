---
title: Automated Wordpress deployment using Vagrant and Puppet
description: Academic project | Automated deployment of a test web environment with a custom Wordpress service (on-premises) using Vagrant as IaC tool and Puppet for provisioning.
slug: wordpress-puppet
date: 2024-11-25 00:00:00+0000
image: wordpress-puppet.png
categories:
    - DevOps
tags:
    - Vagrant
    - Puppet
    - Apache
    - VM's
    - VirtualBox
    - MySQL
    - Wordpress
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the Deployment Automation course, as part of the official university master's degree in Development and Operations (DevOps).

The main objective of this project is to automatically deploy a test web environment with a custom WordPress service, using Vagrant as the Infrastructure as Code (IaC) tool and Puppet for automated provisioning. 
By simply running the `vagrant up` command in the terminal in the directory where the Vagrantfile is located, the entire environment is deployed without any additional configuration.
Before you can deploy a WordPress web service, you need to perform several provisioning and configuration tasks, including the following:

1. Install, configure and set up an Apache web server to redirect and serve all content.
2. Install all the specific PHP packages and modules required by WordPress.
3.	Install, configure and set up a MySQL database that will be used by WordPress for the persistence of its data.

To verify correct operation, simply access `localhost:8080` from the browser.


**GitHub repository:** https://github.com/aleingmar/WordPress_deployment-puppet-vagrant

The project includes two different versions of the environment, organised in separate directories:

- `/puppet-two-nodes`.
In this version, three Puppet nodes are deployed: one Puppet Master and two Puppet Clients.

Each client (node) hosts a WordPress environment, provisioned with the directives sent from the Puppet Master. Every min the puppet clients automatically request the new puppet configuration if any via a cron job.

- `/puppet-one-node`
In this version, only one virtual machine (VM) with a self-provisioning Puppet client is raised, without the need for a Puppet Master.

## Self-provisioning version: puppet-one-node 
In this version of the environment, only one mv is raised, a self-provisioning puppet agent/client without the need for a Puppet master node. The whole deployment process is done fully automatically.
### puppet-one-node: Vagrantfile
The Vagrantfile defines the basic virtual machine (VM) configuration for creating an Infrastructure-as-Code (IaC) environment. It specifies the Ubuntu base box to be used, the networking options (including port forwarding and assigning a private IP), and allocates 1024 MB of RAM to the VM. In addition, Puppet is installed in agent mode, eliminating the need for a master Puppet server, and is configured to use the main manifest `default.pp`, modules from the `modules` directory and the Hiera configuration file `hiera.yaml` to centrally manage data.

## Client-server architecture version: puppet-two-nodes 
In this version of the environment 3 mvs are raised, one puppet master and two puppet clients. The mvs are automatically raised and their corresponding puppet versions are installed (to the master node the master is installed and so on).
Once the client node is up (which is up after the master), as soon as it starts it sends its certificate to the master (which knows it because it is in its puppet.config file).
In a **MANUAL** way, you have to perform the different administration tasks:
1. **SERVER side**:
Manually, the only thing the sysadmin in charge of this environment has to do is to do an:
`sudo /opt/puppetlabs/bin/puppetserver ca sign --all` to sign all the unsigned certificates that have arrived (in this case one for each client node) and send them signed to the corresponding clients. 
- On a voluntary basis, but recommended for security purposes, especially in real production environments, you should run **before** signing them a:
`sudo /opt/puppetlabs/bin/puppetserver ca list --all` to list all the certificates and verify that you don't sign a certificate that you shouldn't.
2. **CLIENT side**:
Once this is done on the server, the corresponding client should receive its signed certificate, with which it will be able to communicate with the master node and
ask for puppet configuration/provisioning by executing this command: `sudo /opt/puppetlabs/bin/puppet agent --test`. 


### General structure of the puppet provisioning project

The organisation of the files and modules is detailed below, which makes it easier to understand the general functioning of the project:

- **Main file**: `manifests/default.pp`.
This file acts as the starting point for Puppet. The modules needed to configure all the components of the environment are imported from here. In this case, the code is split into three modules: **apache, mysql and wordpress**, which are executed and imported in this order. The PHP installation I have decided to code it directly in this module, without adding another module just for this as it is only 3 or 4 lines of code. The installation of these components is done in this order: **apache, php, mysql and wordpress**.

- Variables management with Hiera**: `hiera.yaml, data/common.yaml`.
To manage variables, Hiera is used, which allows the keys to be separated from the source code. This ensures a more secure approach, as it avoids exposing sensitive credentials when uploading the project to a cloud repository. Although this project is academic and does not include encrypted variables, Hiera also offers the possibility to encrypt keys.
- Variables are declared along with their values in `data/common.yaml`.
- The `hiera.yaml` file configures how Hiera works.
- To integrate Hiera with Vagrant, the line `puppet.hiera_config_path = ‘hiera.yaml’` is added to the Vagrantfile.

- **Modules used**:
The project is divided into three main modules, which guarantees modularity and organisation in the code:

1. **Apache module**: This module provisions and configures the Apache web server in the VM.
This module provisions and configures the Apache web server in the VM, leaving it ready and active so that the wordpress module can manage and serve content from it.

2. **mysql module**
In this module a MySQL server is installed and configured in the VM, ensuring the correct functioning of the database manager. In addition, the necessary database for WordPress is created using the `init-wordpress.sql.erb` file.

3. **wordpress module**
This module installs and configures WordPress, making it fully functional. The main actions performed are:

- Installation of the wordpress packages and dependencies and activation of the service.
- Configuration of the `wp-config.conf.erb` file, which configures the service, among other things, connects WordPress with the database and defines previously generated access keys.
- Installation and use of the `wp-cli` tool to automate the configuration of the website.
- Initialisation of the database using the `init-wordpress-content.sql.erb` file with the minimum content necessary to launch a web page.
- Configuration of Apache to serve the page content, using the `wp-apache-config.conf.erb` file.


The service is accessible from the host at `localhost:8080` thanks to port 8080 redirection from the host to port 80 on the virtual machine, where Apache listens for incoming HTTP requests.

Deployment of the puppet-one-node version enviroment:
{{< youtube "xQdjuHr-2-U" >}}