---
title: My own Rasverrypi5 server
description: Configuración, administración y despliegue de servicios en mi propio servidor Rasberrypi5
slug: rasberrypi
date: 2024-08-01 00:00:00+0000
image: rasberry.png
categories:
    - DevOps
tags:
    - Bash
    - Linux
    - Docker
    - Caddy
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
Proyecto personal para tener mi propio servidor y desplegar mis propios servicios.
- Actualmente puedo acceder por ssh al servidor de forma remota para la configuración del propio servidor como de los servicios.
- Tengo un dominio principal en DuckDNS a través del cual puedo acceder a mis servicios por https (protocolo seguro de TLS/SSL) desde el navegador. 
	- gestionado y actualizado (la ip de la red de mi casa) por un contenedor que de forma automática cada 5 min actualiza la ip del servidor
- El acceso a mis servicios está securizado (https, TLS/SSL) y tiene como intermediario por el servidor web de Caddy. 
- Tengo un dashboard avanzado llamado Homarr a través del cual puedo loguearme y acceder al resto de mis servicios clickando sobre ellos.
- Tengo en subdominios específicos mis servicios web accesibles, entre los cuales se incluyen:
	- Gestor de contraseñas Vaultwarden
	- Gestor de contenedores web Portainer
	- DNS anti-anuncios Pihole
- Tengo mi propia VPN con WireGuard, conectada con Pihole, el cual me permite no solo pivotar mi conexión a la red a través de mi servidor y securizarla sino navegar con el bloqueador de anuncios

![Dashboard Homarr](homarr.png)![Gestor de contraseñas Vaultwarden](vaultwarden.png) 

![Gestor de contenedores Portainer](portainer.png)![DNS Antianuncios Pihole](pihole.png) 
