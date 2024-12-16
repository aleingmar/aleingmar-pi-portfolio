---
title: Creation and automated deployment of image in multicloud environment.
description: Academic project | Creation and automated deployment of image in multicloud environment (Azure and AWS). Creation of web app image (Nodejs and NginX) using Packer, deployment of cloud infrastructure using Terraform and provisioning of the infrastructure with Ansible.
slug: imagen-multicloud-packer
date: 2024-12-14 00:00:00+0000
image: imagen-multicloud-packer2.png
categories:
    - DevOps
    - Cloud
tags:
    - Packer
    - Terraform
    - Ansible
    - AZURE
    - AWS
    - NginX
    - VM's
    - Bash
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the DevOps Tools course, as part of the official university master's degree in Development and Operations (DevOps).

The aim of the project is to **create and automatically deploy an image of a complete web system in a multicloud environment of Azure and AWS**. This web system is composed of a small application written with Nodejs and a Nginx web server. To achieve this, I use Terraform, Ansible and Packer technologies mainly. 

### Technologies used:

- **Terraform:** With Terraform I centralize all the execution of the process and deploy the necessary infrastructure to raise an instance in the cloud created from the image of the system and accessible through the internet. 
- **Packer:** With Packer I build the complete system image. Packer uses the cloud as a provider for the creation of the image. It builds an instance and all the necessary infrastructure for the creation of the image and destroys it when it is finished.
- **Ansible:** with ansible the provisioning of the instance that packer raises and from which the image is created is carried out. In the case of Azure I do this provisioning with Ansible, in the case of AWS I do the same but directly with Bash scripting.

To control multicloud deployment, a parameter has been implemented that must be passed to the `terraform apply ‘deployment_target=’`, indicating whether you want to deploy in both clouds simultaneously or in a single cloud. If this is the case, you must indicate in which one you want to deploy.

### Creation and deployment process:

The sequence of steps in the process would be as follows: 
1. Initialise by manually executing a `terraform init && terraform apply` in the shell.
2. After that, terraform executes the `packer build` command, which takes care of setting up all the necessary infrastructure and the machine used for the creation of the image. In the case of Azure, an Ansible is installed on this machine and it auto-provisions itself by running a playbook and a series of tasks defined in it. In the case of AWS, the same steps are executed, but instead of an Ansible directly by manual scripting in Bash. The provisioning is based among other things on the installation and management of the services: Nodejs, Nginx, pm2 and App.js on the instance that creates the image.
- **Nodejs:** Provides an environment with everything necessary for the application to run and function correctly.
- **Nginx:** Web server that will be in charge of redirecting all the traffic to the application and forwarding its responses. It is very important to configure it so that when the image is deployed the server is active and correctly configured to serve the app. Passes traffic from port 80 to port 3000 (where the app.js listens).
- **PM2:** Nodejs process manager which is used to ensure that the app.js is active when the image is deployed without having to do anything else (this step is particularly tricky).
- **app.js**: core, functional application of the image, it is important to transfer the source code of the app so that it is accessible by the instance that creates the image.

3. After this, Packer creates the image and destroys all the infrastructure it has needed to build on the corresponding cloud provider. 
4. Terraform, after waiting for the image creation to finish successfully, builds all the necessary infrastructure (key pair, security group, disk...) to build an instance from this image.
5. Once the deployment is finished, this instance is accessible through the internet via the public ip.

In short, just by executing a `terraform init && terraform apply` you deploy a functional web environment accessible from the internet in the public cloud of Azure and AWS. And you also create a reusable image so you can deploy more instances identical to these in the future in a much faster and safer way against possible human errors.


**GitHub repository:** https://github.com/aleingmar/CreateImages_Nginx-Nodejs_Packer

### Repository contents and project files:

The GiHub repository consists of two main directories with two different versions: `/version-2` and `/version-3.1`.
The fully functional directory containing the latest version of the project is the second one (`/version-3.1`). This is the directory where you have to be located to deploy the `terraform init && terraform apply` (`cd version-3.1/te*`).


Briefly explaining the contents of the directory:
- `/packer/`: directory where all the content necessary for Packer to run and build the image is located.
    - `/packer/main.pkr.hcl`: Packer's main file where all the resources needed to build the image are defined as well as all the variables to be used.
    - `/packer/variables.pkrvars.hcl`: file where I assign values to all the variables defined in the `main.pkr.hcl` except for the credentials of the two clouds that for security reasons, I define and assign values as environment variables of my host operating system that I use to launch the terraform. I pass these values as parameters in the `terraform apply` and `packer build` command.
    - `/packer/providers/`: directory where we can find the auxiliary files used to create the image, such as the apache configuration file (`nginx_default.conf`), the playbook that defines the provisioning with ansible (`provision.yml`) and the nodejs application code (`app.js`). 
- `/terraform/`: directory where all the content necessary for terraform to run and deploy all the necessary infrastructure for the project is located.
    - `/terraform/main.tf`: main file of terraform, where all the process flow that the deployment must follow and all the infrastructure to be deployed is defined.
    - `/terraform/variables.tf`: file where all the variables used by terraform are defined.
    - `/terraform/terraform.tfvars`: file where all the variables are given values except for the credentials of the two clouds that, for security reasons, I define and assign values in environment variables of my host operating system from where I launch terraform. I pass these values as parameters in the `terraform apply` and `packer build` command.

![Directory content](ficheros.png)

### Contents of Packer main:

The content of this file can be differentiated in several parts in which the following components necessary for the creation of the image are defined:
- **PLUGINS**: Defines the plugins needed for the template.
- **Definition of variables**: (no value is assigned here, only maybe the default value).

- **BUILDER**: Define how the AMI is built in AWS --> `source{}`--> define the base system on which I want to create the image (ubuntu ISO) and the provider for which we create the image (technology with which the image will be deployed) --> AMAZON. AZURE
- **PROVISIONERS**: Configure the operating system and the application, how the software will be installed and configured --> `build{}`. 


### Experimentation video and report of the project:
Project documentation: [**View the pdf**](/post/imagen-multicloud-packer/Act1_Packer_AlejandroIngles.pdf)

{{< youtube "BhRB0716G5w" >}}