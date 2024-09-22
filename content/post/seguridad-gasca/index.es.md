---
title: Arquitectura Segura Cliente-Servidor en Java
description: Proyecto académico | Implementación de una arquitectura segura cliente-servidor en Java utilizando TLS para asegurar las comunicaciones.
slug: seguridad-gasca
date: 2021-12-01 00:00:00+0000
image: openssl.png
categories:
    - Ciberseguridad
tags:
    - WSL
    - Java
    - Wireshark
    - OpenSSL
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado durante la asignatura de Seguridad, Confidencialidad y Gestión de la Identidad (SCGI) durante mi tercer año de carrera. En este proyecto implementé una arquitectura segura cliente-servidor en Java, utilizando el protocolo TLS para asegurar todas las comunicaciones entre ambos extremos. Configuré almacenes de claves (KeyStores) y certificados para garantizar la autenticación mutua entre el cliente y el servidor, asegurando así que sólo usuarios y servidores autorizados puedan acceder al sistema.

El servidor fue diseñado para manejar hasta 300 conexiones concurrentes, con pruebas rigurosas para verificar la estabilidad y el rendimiento bajo alta carga. Se implementaron sockets TLS que permiten transmitir credenciales y mensajes de manera segura y cifrada, asegurando que los datos estén protegidos durante todo el proceso de comunicación.

El desarrollo de este sistema implicó la configuración de KeyStores y la integración de los certificados necesarios tanto en el cliente como en el servidor, permitiendo una autenticación y transmisión de datos completamente seguras. Además, el manejo de múltiples conexiones simultáneas se optimizó para garantizar un rendimiento fluido incluso en escenarios de alta demanda.


Documentación del proyecto: [**Visualizar documentación en pdf**](/post/seguridad-gasca/conexion_TLS.pdf)