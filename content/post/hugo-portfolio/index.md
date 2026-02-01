---
title: Deployment and creation of a web portfolio with Hugo.
description: Personal project | Creation and deployment of web portfolio on my RPI5 server for the presentation of the projects I have done during my academic and professional career. Indeed, the web portfolio where you are reading this right now :)
slug: hugo-portfolio
date: 2024-09-01 00:00:00+0000
image: hugo-portfolio.png
categories:
    - DevOps
    - Web Development
tags:
    - Markdown
    - Bash
    - Hugo
    - Docker
    - Caddy
    - Git, Github
    - Html, Css, Js
    - VSCode
    - RPI5
    - GoogleAnalytics
weight: 6       # You can add weight to some posts to override the default sorting (date descending)
---
This project aims to create a web portfolio to show all the projects I have developed during my academic and personal career, deploy it on my own RPI5 server and make it securely accessible from the internet.

## Web Development


For the construction of my portfolio I chose **Hugo**, a static website generation platform that allows you to create modern frontend pages using **Markdown** files. The decision to use Hugo was based on the fact that I had already written part of my portfolio in Obsidian, a tool (also written in Markdown) that I regularly use to take notes and organise my notes. Hugo's ability to take advantage of Markdown format files allowed me to migrate this content easily and focus more on the quality of the content than on the technical development.

The theme I selected for my portfolio is [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack), because of its clean and modern format, which fits perfectly with the structure and design I was looking for. This template, with its focus on performance and simplicity, allowed me to optimise the development of my portfolio without having to invest too much time in interface design. Even so, I have programmed new functionalities that differ from the open source base project for my personal use.

## DevOps and Deployment


In terms of deployment and operational management, my portfolio is hosted on my Raspberry Pi 5 server with 8 GB of RAM, which provides an efficient and energy-efficient solution. To ensure an orderly and isolated environment, I use Docker, where the portfolio runs inside a container. This allows me to package the application independently from the rest of the system, facilitating management and avoiding conflicts with other services running on the same server.

The web server that handles the requests is **Caddy**, a lightweight solution that allows me to secure the connection with HTTPS automatically and redirect the traffic to the different services I have deployed. In addition to my own portfolio, I also host the portfolio of a colleague in another container. To monitor the web portfolio I use Google Analytics 4 (GA4) which allows me to see statistics about the accesses to the website.

For development, I usually work locally using **Visual Studio Code**, although sometimes I use **GitHub Codespaces** when I prefer to work in a remote environment. The deployment process is simple: I connect to the server via SSH, pull the latest changes from GitHub and restart the Docker container running Hugo. This workflow is fully automated through a bash script and a Docker Compose file, which simplifies the process of lifting the web application with each update.

**Web portfolio change deployment process with bash scripting:**

{{< youtube "j6_zmGQ0YFM" >}}