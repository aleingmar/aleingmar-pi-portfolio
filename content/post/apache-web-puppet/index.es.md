---
title: Despliegue automatizado de servidor web con Vagrant y Puppet
description: Proyecto académico | Despliegue automatizado en local de servidor web Apache utilizando Vagrant y Puppet.
slug: apache-web-puppet
date: 2024-10-11 00:00:00+0000
image: vagrantPuppet.png
categories:
    - DevOps
tags:
    - Vagrant
    - Puppet
    - Apache
    - MV's
    - VirtualBox
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura de Automatización de Despliegues, como parte del máster universitario oficial en Desarrollo y Operaciones (DevOps).

El objetivo del proyecto es desplegar y configurar de manera automatizada un entorno web en una máquina virtual que hospeda un servidor Apache, el cual sirve una página web básica. La máquina virtual se crea mediante IaC (Infrastructure as Code) con Vagrant, y para su aprovisionamiento se utiliza Puppet, que gestiona la instalación de Apache y la carga automática de un archivo HTML simple, creando así un servicio web funcional.

En definitiva, simplemente ejecutando un `vagrant up` comienza todo el proceso de despliegue y aprovisionamiento y de forma automática (sin hacer nada más) se levanta una máquina virtual en la cual se instala puppet, se configura e instala un servidor web Apache para que se active y escuche el puerto 80 (http) de la Mv y para que devuelva una página web simple que se introduce en su interior.

**Repositorio de GitHub:** https://github.com/aleingmar/Despliegue_web_apache_Vagrant-Puppet


El repositorio de GiHub se compone de un directorio donde se encuentra un fichero "Vagrantfile" y una carpeta "manifests" en cuyo interior se encuentra el fichero "apache.pp".

- En el Vagrantfile se define la infraestructura de máquinas virtuales que es necesaria desplegar para sustentar el servicio web. De esto se encarga Vagrant y por debajo, usa como proveedor de virtualización VirtualBox.

 - En el Vagrantfile antes de indicarle a Vagrant que debe hacer el aprovisionamiento de la infraestructura usando Puppet, se ejecuta un script para instalar Puppet dentro de las máquinas virtuales. Puppet en este caso trabaja en modo stand-alone (sin seguir modelo cliiente-servidor).

- En el fichero "apache.pp" se define la configuración deseada para esta infraestructur y le sirve a Puppet de guía declarativa para desarrollar su trabajo. Como Puppet usa un lenguaje declarativo no se le indica como se quiere que se hagan las cosas, sino solo lo que se quiere conseguir y Puppet se encarga del resto.


El servicio es accesible desde el host en `localhost:8080` gracias a la redirección del puerto 8080 del host al puerto 80 de la máquina virtual, donde Apache escucha las solicitudes HTTP entrantes.

{{< youtube "8K7JzFuzGvg" >}}
