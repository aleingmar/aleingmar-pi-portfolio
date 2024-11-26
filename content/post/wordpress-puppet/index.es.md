---
title: Despliegue automatizado de Wordpress usando Vagrant y Puppet
description: Proyecto académico | Despliegue automatizado de página web en Wordpress (en local) utilizando como herramienta IaC Vagrant y para su aprovisionamiento Puppet.
slug: wordpress-puppet
date: 2024-12-01 00:00:00+0000
image: wordpress-puppet.png
categories:
    - DevOps
tags:
    - Vagrant
    - Puppet
    - Apache
    - MV's
    - VirtualBox
    - MySQL
    - Wordpress
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura de Automatización de Despliegues, como parte del máster universitario oficial en Desarrollo y Operaciones (DevOps).

El objetivo principal de este proyecto es desplegar de forma automática un entorno web de prueba con un WordPress personalizado, utilizando Vagrant como herramienta de Infraestructura como Código (IaC) y Puppet para su aprovisionamiento automatizado. 
Simplemente ejecutando en la terminal el comando `vagrant up` en el directorio donde se encuentra el Vagrantfile, se despliega todo el entorno sin necesidad de realizar configuraciones adicionales. 
Antes de desplegar el entorno WordPress configurado, es necesario llevar a cabo varias tareas de aprovisionamiento y configuración, entre ellas:

1.	Preparar y configurar la máquina virtual (MV) con un servidor web Apache para redirigir y servir todo el contenido.
2.	Instalar los módulos específicos de PHP requeridos por WordPress.
3.	Configurar una base de datos MySQL que será utilizada por WordPress para su funcionamiento.

Para verificar el correcto funcionamiento, basta con acceder a `localhost:8080` desde el navegador.


**Repositorio de GitHub:** https://github.com/aleingmar/WordPress_deployment-puppet-vagrant


El proyecto incluye dos versiones del entorno, organizadas en directorios separados:

- `/puppet-two-nodes`
En esta versión se despliegan dos nodos Puppet: un Puppet Master y un Puppet Client.

Cada cliente (nodo) aloja un entorno de WordPress, aprovisionado con las directivas enviadas desde el Puppet Master. Cada min los puppet clients solicitan la nueva configuracon de pupet si la hubiera mediante una tarea cron.
- `/puppet-one-node`
En esta versión se levanta únicamente una máquina virtual (MV) con un cliente Puppet que se autoaprovisiona, sin necesidad de un Puppet Master.

### Vagrantfile de puppet-one-node
El Vagrantfile define la configuración básica de la máquina virtual (MV) para crear un entorno de infraestructura como código (IaC). Se especifica la caja base de Ubuntu que se utilizará, las opciones de red (incluyendo el redireccionamiento de puertos y la asignación de una IP privada), y se asigna 1024 MB de memoria RAM a la MV. Además, se instala Puppet en modo agente, eliminando la necesidad de un servidor Puppet maestro, y se configura para utilizar el manifiesto principal `default.pp`, los módulos desde el directorio `modules` y el archivo de configuración de Hiera `hiera.yaml` para gestionar datos de forma centralizada.

### Estructura general del proyecto de aprovisionamiento con puppet

A continuación, se detalla la organización de los archivos y módulos, lo que facilita la comprensión del funcionamiento general del proyecto:

- **Archivo principal**: `manifests/default.pp`
Este archivo actúa como el punto de inicio de Puppet. Desde aquí se importan los módulos necesarios para configurar todos los componentes del entorno. En este caso, el código está dividido en tres módulos: **apache, mysql y wordpress**, que son ejecutados e importados en este orden. La instalación de PHP he decidido codificarla directamente en este módulo, sin añadir un módulo más simplemente para esto ya que son apenas 3 o 4 líneas de código. La instalación de estos componentes se hace en este orden: **apache, php, mysql y wordpress**.

- **Gestión de variables con Hiera**: `hiera.yaml, data/common.yaml`
Para gestionar las variables, se utiliza Hiera, lo que permite separar las claves del código fuente. Esto asegura un enfoque más seguro, ya que evita exponer credenciales sensibles al subir el proyecto a un repositorio en la nube. Aunque este proyecto es académico y no incluye variables encriptadas, Hiera también ofrece la posibilidad de encriptar claves.
-	Las variables se declaran junto con sus valores en `data/common.yaml`.
-	El archivo `hiera.yaml` configura el funcionamiento de Hiera.
-	Para integrar Hiera con Vagrant, se añade la línea `puppet.hiera_config_path = "hiera.yaml"` en el Vagrantfile.


- **Módulos utilizados**:
El proyecto está dividido en tres módulos principales, lo que garantiza modularidad y organización en el código:

1. **Módulo apache**
Este módulo aprovisiona y configura el servidor web Apache en la MV, dejándolo preparado y activo para que el módulo wordpress pueda administrar y servir contenido desde él.

2. **Módulo mysql**
En este módulo se instala y configura un servidor MySQL en la MV, asegurando el correcto funcionamiento del gestor de bases de datos. Además, se crea la base de datos necesaria para WordPress mediante el archivo `init-wordpress.sql.erb`

3. **Módulo wordpress**
Este módulo instala y configura WordPress, dejándolo completamente funcional. Las principales acciones realizadas son:

-	Instalación de los paquetes y dependencias de Wordpress y activación del servicio.
-	Configuración del archivo `wp-config.conf.erb`, que configura el servicio, entre otras cosas, conecta WordPress con la base de datos y define claves de acceso generadas previamente.
-	Instalación y uso de la herramienta `wp-cli` para automatizar la configuración del sitio web.
-	Inicialización de la base de datos mediante el archivo `init-wordpress-content.sql.erb` con un contenido mínimo necesario para lanzar una página web.
-	Configuración de Apache para servir el contenido de la página, utilizando el archivo `wp-apache-config.conf.erb`.


El servicio es accesible desde el host en `localhost:8080` gracias a la redirección del puerto 8080 del host al puerto 80 de la máquina virtual, donde Apache escucha las solicitudes HTTP entrantes.

{{< youtube "xQdjuHr-2-U" >}}
