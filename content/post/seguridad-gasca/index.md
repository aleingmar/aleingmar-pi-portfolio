---
title: Secure Client-Server Architecture in Java
description: Academic project | Implementation of a secure client-server architecture in Java using TLS to secure communications.
slug: seguridad-gasca
date: 2021-12-01 00:00:00+0000
image: openssl.png
categories:
    - Cybersecurity
tags:
    - WSL
    - Java
    - Wireshark
    - OpenSSL
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed during the Security, Confidentiality and Identity Management (SCGI) course during my third year of studies. In this project I implemented a secure client-server architecture in Java, using the TLS protocol to secure all communications between both ends. I configured keystores (KeyStores) and certificates to guarantee mutual authentication between client and server, ensuring that only authorised users and servers can access the system.

The server was designed to handle up to 300 concurrent connections, with rigorous testing to verify stability and performance under high load. TLS sockets were implemented to allow credentials and messages to be transmitted in a secure and encrypted manner, ensuring that data is protected throughout the communication process.

The development of this system involved the configuration of KeyStores and the integration of the necessary certificates on both the client and the server, enabling fully secure authentication and data transmission. In addition, the handling of multiple simultaneous connections was optimised to ensure smooth performance even in high-demand scenarios.


Project documentation: [**View documentation in pdf**](/post/seguridad-gasca/conexion_TLS.pdf)