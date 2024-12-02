---
title: Automated Wordpress Deployment using Vagrant and Puppet
description: Academic project | Automated deployment of Wordpress website (locally) using Vagrant as IaC tool and Puppet as provisioning tool.
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

The main objective of this project is to automatically deploy a test web environment with a custom WordPress, using Vagrant as the Infrastructure as Code (IaC) tool and Puppet for automated provisioning. 
By simply running the `vagrant up` command in the terminal in the directory where the Vagrantfile is located, the entire environment is deployed without any additional configuration. 
Before deploying the configured WordPress environment, several provisioning and configuration tasks need to be performed:

1. prepare and configure the virtual machine (VM) with an Apache web server to redirect and serve all content.
2. Install the specific PHP modules required by WordPress.
3.	Configure a MySQL database that will be used by WordPress for its operation.

To verify correct operation, simply access `localhost:8080` from the browser.

**GitHub repository:** https://github.com/aleingmar/WordPress_deployment-puppet-vagrant


The project includes two versions of the environment, organised in separate directories:

- `/puppet-two-nodes`.
This version deploys two Puppet nodes: a Puppet Master and a Puppet Client.

Each client (node) hosts a WordPress environment, provisioned with directives sent from the Puppet Master. Every min the puppet clients request the new puppet configuration if any via a cron job.
- `/puppet-one-node`
In this version, only one virtual machine (VM) is raised with a self-provisioning Puppet client, without the need for a Puppet Master.

### puppet-one-node Vagrantfile
The Vagrantfile defines the basic virtual machine (VM) configuration for creating an Infrastructure-as-Code (IaC) environment. It specifies the Ubuntu base box to be used, the networking options (including port forwarding and assigning a private IP), and allocates 1024 MB of RAM to the VM. In addition, Puppet is installed in agent mode, eliminating the need for a master Puppet server, and configured to use the main manifest `default.pp`, modules from the `modules` directory, and the Hiera configuration file `hiera.yaml` to centrally manage data.

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