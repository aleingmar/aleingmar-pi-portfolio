---
title: Automatic web server deployment using Vagrant and Puppet
description: Academic project | Automatic local deployment of Apache web server using Vagrant and Puppet.
slug: apache-web-puppet
date: 2024-10-11 00:00:00+0000
image: vagrantPuppet.png
categories:
    - DevOps
tags:
    - Vagrant
    - Puppet
    - Apache
    - VM's
    - VirtualBox
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the Deployment Automation course, as part of the official university master's degree in Development and Operations (DevOps).

The aim of the project is to deploy and configure in an automated way a web environment on a virtual machine hosting an Apache server, which serves a basic web page. The virtual machine is created using IaC (Infrastructure as Code) with Vagrant, and Puppet is used for its provisioning, which manages the installation of Apache and the automatic loading of a simple HTML file, thus creating a functional web service.

In short, simply running a `vagrant up` starts the whole deployment and provisioning process and automatically (without doing anything else) a virtual machine is raised in which puppet is installed, an Apache web server is configured and installed to activate and listen to port 80 (http) of the VM and to return a simple web page that is inserted inside it.

**GitHub repository:** https://github.com/aleingmar/Despliegue_web_apache_Vagrant-Puppet


The GiHub repository consists of a directory containing a ‘Vagrantfile’ file and a ‘manifests’ folder containing the ‘apache.pp’ file.

- The Vagrantfile defines the virtual machine infrastructure that needs to be deployed to support the web service. This is taken care of by Vagrant and underneath it, it uses VirtualBox as virtualisation provider.

 - In the Vagrantfile, before telling Vagrant to provision the infrastructure using Puppet, a script is run to install Puppet inside the virtual machines. Puppet in this case works in stand-alone mode (without following the client-server model).

- The file ‘apache.pp’ defines the desired configuration for this infrastructure and serves as a declarative guide for Puppet to develop its work. Since Puppet uses a declarative language, you don't tell it how you want things to be done, only what you want to achieve, and Puppet does the rest.


The service is accessible from the host on `localhost:8080` by redirecting port 8080 on the host to port 80 on the virtual machine, where Apache listens for incoming HTTP requests.


{{< youtube "8K7JzFuzGvg" >}}