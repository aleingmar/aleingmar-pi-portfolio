---
title: Automatic deployment of multilayer MEAN service on AWS
description: Academic project | Creation and automatic deployment of a multi-tier MEAN system on AWS using Terraform, Packer and Ansible. Modular infrastructure with load balancer, multiple instances for the application and a MongoDB database.
slug: stack-mean-terraform
date: 2025-01-14 00:00:00+0000
image: stack.png
categories:
    - DevOps
    - Cloud

tags:
    - Packer
    - Terraform
    - Ansible
    - MongoDB
    - Angular
    - Express
    - AWS
    - NginX
    - VM's
    - Bash
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the DevOps Tools course, as part of the university's master's degree in Development and Operations (DevOps).

The objective of the project was to automatically deploy a fully functional multi-layer MEAN system in the AWS cloud. This system consists of a load balancer, several instances for the web application and a dedicated instance for the MongoDB database. I use Terraform, Packer and Ansible for infrastructure automation and provisioning.

### Technology Stack

- **Terraform**: with terraform I centralise the whole deployment process and manage infrastructure elements such as networks, instances, load balancers... elements that help me to support the service.

- **Packer**: with Packer I create images that serve as the basis for the instances that I build with Terraform. In this project, Packer generates a custom image for the first layer of the system, provisioning it with the necessary services such as Node.js, Nginx, Angular...

- **Ansible**: with Ansible I do the provisioning of the instance that is raised and used by Packer for the creation of the image. In this project, Ansible automatically provisions the instance with Angular, Express, MongoDB, Nginx, Node...

- **MEAN stack**: The system builds a service with the MEAN technology stack, widely used in the industry for its versatility and performance:
    - **MongoDB**: Non-relational document-oriented database, ideal for handling large volumes of structured and unstructured data.
    - **Express**: Backend framework for Node.js that facilitates the development of robust and scalable web applications.

    - **Angular**: Frontend framework that allows the development of modern and reactive interfaces, improving the user experience.

    - **Node.js**: Execution environment for server-side Js.

### Modularisation of the Terraform template

#### Importance of modularisation

Modularisation in Terraform not only improves code readability and maintainability, but also allows responsibilities to be divided and configurations to be reused between projects. Although managing variables between modules can be complex, this practice is essential in large, dynamic infrastructures.

#### Project modules

- **Security module**: This module manages the security groups that define the traffic rules to and from the instances, enabling traffic from protocols such as SSH, HTTP.... It also configures the SSH keys needed to access the instances remotely.

- **Networking module**: Defines the private networks and subnets required for system connectivity. Configures routing tables and gateways to ensure access between infrastructure layers. Ensures that instances of the second layer (database) remain accessible only from the internal network.

- **Instance Module**: Deploys the first and second layer instances, assigning public and private IP addresses. Provisions the instances with basic initial configurations for integration into the system.

- **Load Balancer Module**: Configures the load balancer that distributes traffic between the first layer instances. Defines target groups and distribution strategies such as round-robin and persistent sessions to improve system availability and consistency.

- **Image module**: Integrates Terraform with Packer for the creation of base images. Terraform runs packer build, retrieves the generated image and uses it to instantiate first layer resources.

![Directory structure](modulos.png)

### Deployment process

The deployment starts with the integration of Terraform and Packer. Terraform invokes Packer, which is responsible for raising a temporary instance on AWS to generate a base image. During this process, the instance is provisioned with Ansible, which installs and configures services such as Angular, Express and MongoDB, as well as copying essential files from the local environment. Once provisioning is complete, Packer creates the base image and destroys the temporary instance, leaving an image ready for reuse.

With the image generated, Terraform proceeds to deploy the complete infrastructure. First, the networks and subnets are configured, ensuring internal connectivity between the layers of the system. Next, the first layer instances are deployed using the base image. These instances host the frontend and backend of the application, with Node.js and Nginx serving as the operational core.

At the same time, Terraform builds the second tier instance, dedicated to data persistence with MongoDB. This instance is connected via a private network to the first layer instances, guaranteeing secure and stable communication. In addition to this, terraform also raises a load balancer, configured to distribute the traffic between the first layer instances, which ensures high availability and scalability.

The last step is the final provisioning. Terraform uses eh Bash scripting to finish configuring the deployed instances. For example, in the first layer instances, Angular configurations are adjusted to include the IP addresses of the backend, which allows static files to be generated and served by Nginx with the necessary routes to connect the client to the backend.

This entire process ensures a fully automated deployment, resulting in a functional, production-ready system, with components integrated and configured for optimal performance.


**GitHub repository:** 
https://github.com/aleingmar/Multi-layer_MEAN_Deployment


### Video of the experimentation and project report:
Project documentation: [**View documentation in pdf**](/post/stack-MEAN-Terraform/Act2_StackMEAN_Terraform_AlejandroIngles.pdf)

{{< youtube "zRGhkBebEbA" >}}