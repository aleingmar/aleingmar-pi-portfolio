---
title: My own RPI5 server
description: Personal project | Configuration, administration and deployment of services on my own Rasberrypi 5 server. A VPN, a password manager, a container manager and a DNS ad and tracker blocker.
slug: my-server
date: 2024-08-01 00:00:00+0000
image: rasberry.png
categories:
    - DevOps
tags:
    - Bash
    - Linux
    - Docker
    - Caddy
    - RPI5
weight: 6       # You can add weight to some posts to override the default sorting (date descending)
---
This project consists of hosting and managing autonomously certain services on my own server, a RasberryPi 5 with 8gb of Ram. 

For the administration and configuration of both the server and its hosted services, I access remotely via SSH protocol.

The server is associated to a main domain managed by **DuckDNS**, which allows me to access the services remotely through the browser. To prevent the dynamic IP of my home network from changing and losing access to the server, I have a service that automatically updates this IP every 5 minutes, ensuring that it is always correctly synchronised.

To organise access via subdomains and ensure connection to my services via **HTTPS**, I use **Caddy** as a web server, which acts as an intermediary and handles the TLS/SSL certificates, guaranteeing secure and uncomplicated access.

In addition, I have implemented an advanced control panel called **Homarr**, which provides me with a centralised interface from which I can easily log in and access the different services deployed on the server. 

All the services hosted on the server including the ones mentioned above are hosted using **Docker containers** and are organized in specific subdomains.
At the time of writing, the unmentioned services hosted on the server are:

- **Vaultwarden**: A password manager.
- **Portainer**: A container manager with a web interface.
- **Pi-hole**: An ad-blocking DNS service.
- **WireGuard**: A VPN service.

WireGuard is integrated with Pi-hole. This setup allows me not only to redirect my traffic through my server to secure my connection, but also to enjoy ad-free browsing, no matter where I am.

{{< youtube "ZHQXSUq01k0" >}}