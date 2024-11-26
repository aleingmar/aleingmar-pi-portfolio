---
title: Despliegue de servicio web con EC2 AWS 
description: Proyecto académico | Balancedor de carga que distribuye las solicitudes entre dos instancias de EC2, cada una con su propio servidor Apache y página web.
slug: aws-ec2-assb
date: 2024-11-25 00:00:00+0000
image: aws-ec2.png
categories:
    - DevOps
    - Cloud
tags:
    - Bash
    - WSL
    - EC2
    - Apache
    - AWS
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para un trabajo de la asignatura Arquitecturas de Sistemas y Sistemas Distribuidos (ASSB) durante mi cuarto año de carrera. El objetivo principal era desplegar un servicio web funcional en un entorno en la nube utilizando los servicios de **AWS**, manteniéndonos dentro de los límites del plan gratuito.

**El servicio web desplegado se conforma por un balancedor de carga que distribuye las solicitudes entre dos instancias de EC2, cada una con su propio servidor Apache y página web.**

Las principales tareas realizadas incluyeron:

- **Control y creación de alertas de costes**: Configuración de alertas en AWS para asegurar que todas las operaciones se ajustaran al plan gratuito, evitando cargos adicionales no deseados.
- **Despliegue de instancias EC2**: Levantar dos instancias de **EC2** y conectarnos a ellas mediante **SSH**. En cada una de las instancias, instalar el servidor web **Apache**.
- **Configuración de servidores web Apache**: Configuración de los servicios de Apache en ambas instancias para que sirvieran una página web estática creada por mi mismo.
- **Implementación de un balanceador de carga**: Despliegue de un balanceador de carga en AWS para distribuir de manera equitativa las peticiones entrantes entre los dos servidores Apache, optimizando la carga y asegurando una mayor disponibilidad.


[**Visualizar memoria en pdf**](/post/aws-ec2-assb/assb-aes-ec2.pdf)