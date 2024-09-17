---
title: Base de datos relacional para la gestión del equipamiento de quirófanos.
description: Proyecto académico | Base de datos relacional para la gestión de instalaciones y equipamientos electromédicos de quirófanos.
slug: bd-quirofano
date: 2021-04-01 00:00:00+0000
image: bd.png
categories:
    - Bases de Datos
tags:
    - SQL
    - MariaDB
    - HeidiSQL
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado durante la asignatura de Bases de Datos (BD) durante mi segundo año de carrera. El objetivo principal era diseñar, modelar y desarrollar una base de datos SQL para gestionar y almacenar la información de las instalaciones y equipamientos electromédicos de un quirófano. La base de datos permitiría no solo gestionar los equipos y su mantenimiento, sino también asegurar el cumplimiento de regulaciones sanitarias, controlar el valor del equipamiento, supervisar las revisiones periódicas...

Algunas de las tareas realizadas incluyen:

- **Diseño y modelado de la base de datos**: A partir de un análisis exhaustivo de los requisitos, se elaboró un modelo relacional que representa los diferentes elementos del quirófano, los equipos electromédicos, las instalaciones de climatización y electricidad, y los perfiles de los usuarios que gestionan esta información (ingenieros biomédicos, ingenieros de mantenimiento y directores de servicios generales).

- **Gestión del ciclo de vida de los equipos**: La base de datos almacena información clave sobre el equipamiento, como su fecha de adquisición, vida útil, proveedor, valor de compra y parámetros técnicos que deben mantenerse dentro de ciertos rangos para asegurar su correcto funcionamiento. Esto permite controlar los plazos de mantenimiento y prever sustituciones de manera oportuna.

- **Automatización de revisiones**: A través de **triggers** y **procedimientos almacenados**, la base de datos es capaz de generar alertas cuando se acerquen las fechas de revisión o cuando un equipo esté próximo a superar su vida útil. Esto asegura que el quirófano se mantenga dentro de los estándares requeridos sin interrupciones imprevistas​.

- **Consultas avanzadas y generación de reportes**: Implementación de una serie de **vistas** y **consultas** para facilitar el acceso a la información relevante, como el estado de las revisiones, el coste total del equipamiento o el historial de mantenimientos realizados por los ingenieros. Esto permite a los usuarios obtener informes personalizados que pueden ser utilizados para la toma de decisiones estratégicas dentro del hospital.

Documentación del proyecto: [**Visualizar documentación en pdf**](bd-quirofano.pdf)