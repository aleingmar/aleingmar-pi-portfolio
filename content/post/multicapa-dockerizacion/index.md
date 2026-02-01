---
title: Dockerization of a Multi-layer application 
description: Academic project | Dockerisation of a Multilayer application, a first container for the presentation layer with Nginx, a second container for the business logic layer with Nodejs and Express, and a third container for the persistence layer with MongoDB.
slug: multilayer-dockerisation
date: 2025-04-19 00:00:00+0000
image: dockerizacion.png
categories:
    - SysAdmin
    - DevOps

tags:
    - Docker
weight: 6 # You can add weight to some posts to override the default sorting (date descending)
---
This project was developed for the Containers subject as part of the official university master's degree in Development and Operations (DevOps).
The main objective of this project is to dockerise a simple multilayer application, designed with a pedagogical perspective to illustrate the layered architecture and its deployment using containers. This application has been designed with three different layers: web presentation, business logic and data persistence.
Although a MEAN (Mongo - Express - Angular - Node) stack was initially considered, the presentation layer based on Angular and Nginx has not been fully implemented. Therefore, the final structure of the project is configured as follows:

- First layer, presentation layer: Nginx + Website

- Second layer, business logic layer: App.js application developed using Express on Node.js.

- Persistence layer: Implemented using MongoDB.


The functionality of the application is deliberately simple, with the aim of focusing on structure and deployment. It is a kind of ‘Hello World’, where the client initially connects to the presentation layer (Nginx), which delivers an index.html file. 
This file contains a call that triggers a second HTTP request to the same Nginx server, but which is processed differently depending on the PATH of the request. 

![Index.html](image-1.png)
![Nginx.conf](image-2.png)

This request is redirected to the backend layer, where the Express application is deployed.

![](image-3.png)

From there, the application tries to establish a connection to the MongoDB database. 

![](image-4.png)


Depending on the result of that connection, the backend responds to the client with a message in JSON format, indicating if the connection was successful (‘Hello world, connection successfully established’) or if an error occurred. 


![Architecture](image.png)


**GitHub repository:** 
https://github.com/aleingmar/multi-layer-app-dockerisation


## Experimentation video and project memory:
Documentation of the project: [**View documentation in pdf**](/post/multicapa-dockerizacion/Act1_Dockerizacion_AlejandroIngles.pdf)

{{< youtube "vvb0ahpH7mE" >}}