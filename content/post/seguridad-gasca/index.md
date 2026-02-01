---
title: Client-Server Architecture in Java using TLS
description: Academic project | Implementation of a Secure Client-Server Architecture in Java using TLS to secure communications.
slug: security-gasca
date: 2021-12-01 00:00:00+0000
image: java3.png
categories:
    - Cybersecurity
tags:
    - WSL
    - Java
    - Wireshark
weight: 50 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed during the Security, Confidentiality and Identity Management (SCGI) course during my third year. This project focused on the design and development of a secure client-server architecture using the Transport Layer Security (TLS) protocol, with the aim of ensuring the confidentiality, integrity and authenticity of communications.

## Context and Objective
The project arose from the need to secure communications in an application that allows the transmission of sensitive data, such as user credentials (login/password), between clients and a central server. This type of application is especially relevant in environments where data privacy is crucial, such as the health sector, banking and any system where users must authenticate their identity to access services.

## Configuring KeyStores and TrustStores
To implement TLS security, it was necessary to configure both the KeyStore and the TrustStore. These elements allow mutual authentication between the client and the server. The KeyStore contains the private keys and associated certificates that identify the entity (client or server), while the TrustStore manages the certificates of the trusted entities, allowing validation that the communication partners are legitimate.

In the development of this project, Keytool, a tool included in the **Java** JDK, was used to create and manage the certificates. The process required the configuration of environment variables such as JAVA_HOME and PATH, to facilitate the use of this tool from the command line.

## Implementation of TLS Sockets
The communication between the client and the server was done through SSL (Secure Sockets Layer) sockets, over which the TLS protocol was integrated. At both ends, client and server, secure sockets were configured to allow the transmission of encrypted data. The server was designed to listen for incoming connections on a specific port (in this case, port 3343), authenticating clients by verifying their credentials.

- **TLS Server**: The server was responsible for receiving client connections and authenticating each user by verifying their credentials (username and password). It also provided responses based on the result of this verification, informing the client whether the authentication was successful or unsuccessful.

- **TLS client**: The client established a secure connection to the server and sent the user's credentials for verification. The server's response was displayed in a simple user interface, indicating whether the authentication process was successful or if there was an error.

## Communication and security testing
Both secured and unsecured communication tests were conducted in order to highlight the importance of using TLS in applications that handle sensitive information. For the unsecured tests, an unencrypted socket was implemented to observe how an attacker, using tools such as **Wireshark**, could capture and display in clear text the transmitted user credentials.

In contrast, by enabling TLS, it was observed that all transmitted data was encrypted, making it impossible for an attacker to read the captured data on the network. This demonstrated the effectiveness of TLS in protecting the confidentiality and integrity of information.

## Performance and Concurrency
A key aspect of this project was the validation of system performance, specifically the ability to handle multiple concurrent connections. The server was configured to handle up to 300 concurrent connections, which was achieved by using Java threads to handle parallel requests. Although connections were made sequentially in the initial tests (one every second), the system proved to be robust in processing requests efficiently without compromising security or stability.



Project documentation: [**View documentation in pdf**](/post/seguridad-gasca/conexion_TLS.pdf)