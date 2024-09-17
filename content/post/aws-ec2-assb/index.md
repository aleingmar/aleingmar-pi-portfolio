---
title: Web service deployment with EC2 AWS
description: Academic project | Load balancer that distributes requests between two EC2 instances, each with its own Apache server and web page.
slug: aws-ec2-assb
date: 2024-01-01 00:00:00+0000
image: aws-ec2.png
categories:
    - DevOps
    - Cloud
tags:
    - Bash
    - WSL
    - EC2
    - Apache
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for a Systems Architectures and Distributed Systems (ASSB) assignment during my fourth year of undergraduate studies. The main objective was to deploy a functional web service in a cloud environment using **AWS** services, staying within the limits of the free plan.

**The deployed web service consists of a load balancer that distributes requests between two EC2 instances, each with its own Apache server and web page.

The main tasks performed included:

- **Controlling and creating cost alerts**: Setting up alerts in AWS to ensure that all operations conformed to the free plan, avoiding unwanted additional charges.
- **Deployment of EC2 instances**: Raise two instances of **EC2** and connect to them via **SSH**. On each of the instances, install the **Apache** web server.
- **Configuring Apache web servers**: Configuring the Apache services on both instances to serve a static web page created by myself.
- **Deployment of a load balancer**: Deployment of a load balancer on AWS to evenly distribute incoming requests between the two Apache servers, optimising the load and ensuring higher availability.


[**View memory in pdf**](assb-aes-ec2.pdf)

