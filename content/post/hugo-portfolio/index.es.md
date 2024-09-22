---
title: Despliegue y creación de portfolio web con Hugo.
description: Proyecto personal | Creación y despliegue de portfolio web en mi servidor RPI5 para la presentación de los proyectos que he realizado durante mi carrera académica y profesional. Efectivamente, el portfolio web donde está leyendo esto ahora mismo :)
slug: hugo-portfolio
date: 2024-09-01 00:00:00+0000
image: hugo-portfolio.png
categories:
    - DevOps
    - Desarrollo web
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
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
Este proyecto tiene como objetivo crear un portfolio web para runir todos los proyectos que he desarrollado durante mi carrera académica y personal, desplegarlo en mi propio servidor RPI5 y hacerlo accesible de manera segura desde internet.

## Desarrollo Web


Para la construcción de mi portfolio elegí **Hugo**, una plataforma de generación de sitios web estáticos que permite crear páginas modernas de frontend utilizando archivos **Markdown**. La decisión de usar Hugo se basó en que ya había redactado una parte de mi portfolio en Obsidian, una herramienta (donde también se escribe en Markdown) que utilizo habitualmente para tomar notas y organizar mis apuntes. La capacidad de Hugo para aprovechar archivos en formato Markdown me permitió migrar este contenido fácilmente y enfocarme más en la calidad del contenido que en el desarrollo técnico.

El tema que seleccioné para mi portfolio es [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack), debido a su formato limpio y moderno, que se ajusta perfectamente a la estructura y diseño que buscaba. Esta plantilla, con su enfoque en el rendimiento y la simplicidad, me permitió optimizar el desarrollo de mi portfolio sin necesidad de invertir demasiado tiempo en el diseño de la interfaz. Aun así, he programado nuevas funcionalidades que difieren del proyecto base open source para mi uso personal.

## DevOps y Despliegue


En cuanto al despliegue y la gestión operativa, mi portfolio está alojado en mi servidor Raspberry Pi 5 con 8 GB de RAM, lo que proporciona una solución eficiente y de bajo consumo energético. Para garantizar un entorno ordenado y aislado, utilizo Docker, donde el portfolio se ejecuta dentro de un contenedor. Esto me permite empaquetar la aplicación de forma independiente del resto del sistema, facilitando la gestión y evitando conflictos con otros servicios que corren en el mismo servidor.

El servidor web que gestiona las peticiones es **Caddy**, una solución ligera que me permite asegurar la conexión con HTTPS de manera automática y redirigir el tráfico a los diferentes servicios que tengo desplegados. Además de mi propio portfolio, en otro contenedor también alojo el portfolio de un compañero de carrera. Para monitorizar el portfolio web utilizo Google Analytics 4 (GA4) lo que me permite ver estadísticas sobre los accesos al sitio web.

Para el desarrollo, suelo trabajar en local utilizando **Visual Studio Code**, aunque en ocasiones utilizo **GitHub Codespaces** cuando prefiero trabajar en un entorno remoto. El proceso de despliegue es sencillo: me conecto al servidor mediante SSH, realizo un pull de los últimos cambios desde GitHub y reinicio el contenedor Docker que ejecuta Hugo. Este flujo de trabajo está totalmente automatizado mediante un script de bash y un archivo Docker Compose, lo que simplifica el proceso de levantar la aplicación web con cada actualización.