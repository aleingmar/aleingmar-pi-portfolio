---
title: Despliegue automatizado de Wordpress usando Vagrant y Puppet
description: Proyecto académico | Despliegue automatizado de entorno web de prueba con un servicio Wordpress personalizado (en local) utilizando como herramienta IaC Vagrant y para su aprovisionamiento Puppet.
slug: wordpress-puppet
date: 2024-11-25 00:00:00+0000
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
weight: 4       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura de Automatización de Despliegues, como parte del máster universitario oficial en Desarrollo y Operaciones (DevOps).

El objetivo principal de este proyecto es desplegar de forma automática un entorno web de prueba con un servicio WordPress personalizado, utilizando Vagrant como herramienta de Infraestructura como Código (IaC) y Puppet para su aprovisionamiento automatizado. 
Simplemente ejecutando en la terminal el comando `vagrant up` en el directorio donde se encuentra el Vagrantfile, se despliega todo el entorno sin necesidad de realizar configuraciones adicionales.
Antes de poder desplegar un servicio web de WordPress, es necesario llevar a cabo varias tareas de aprovisionamiento y configuración previas, entre ellas están:

1.	Instalar, configurar y levantar un servidor web Apache para redirigir y servir todo el contenido.
2.	Instalar todos los paquetes y módulos específicos de PHP requeridos por WordPress.
3.	Instalar, configurar y levantar una base de datos MySQL que será utilizada por WordPress para la persistencia de sus datos.

Para verificar el correcto funcionamiento, basta con acceder a `localhost:8080` desde el navegador.


**Repositorio de GitHub:** https://github.com/aleingmar/WordPress_deployment-puppet-vagrant


El proyecto incluye dos versiones diferentes de entorno, organizadas en directorios separados:

- `/puppet-two-nodes`
En esta versión se despliegan tres nodos Puppet: un Puppet Master y dos Puppet Client.

Cada cliente (nodo) aloja un entorno de WordPress, aprovisionado con las directivas enviadas desde el Puppet Master. Cada min de forma automática los puppet clients solicitan la nueva configuracon de puppet si la hubiera mediante una tarea cron.

- `/puppet-one-node`
En esta versión se levanta únicamente una máquina virtual (MV) con un cliente Puppet que se autoaprovisiona, sin necesidad de un Puppet Master.

## Versión de autoaprovisionamiento: puppet-one-node 
En esta version del entorno se levanta solo una mv, un puppet agente/cliente que se autoaprovisiona sin necesidad de ningún nodo master. Todo el proceso de despliegue se hace totalmente de forma automática.
### puppet-one-node: Vagrantfile
El Vagrantfile define la configuración básica de la máquina virtual (MV) para crear un entorno de infraestructura como código (IaC). Se especifica la caja base de Ubuntu que se utilizará, las opciones de red (incluyendo el redireccionamiento de puertos y la asignación de una IP privada), y se asigna 1024 MB de memoria RAM a la MV. Además, se instala Puppet en modo agente, eliminando la necesidad de un servidor Puppet maestro, y se configura para utilizar el manifiesto principal `default.pp`, los módulos desde el directorio `modules` y el archivo de configuración de Hiera `hiera.yaml` para gestionar datos de forma centralizada.

## Versión de arquitectura cliente-servidor: puppet-two-nodes 
En esta version del entorno se levantan 3 mvs, un puppet master y dos puppet clients. De forma automática se levantan las mvs y se instalan sus correspondientes versiones de puppet (al nodo master se instala el master y asi).
Una vez que se levanta el nodo cliente (que se levanta despues del master), nada mas que arranca envia su certificado al master (que lo conoce porque esta en su fichero puppet.config).
De forma **MANUAL** hay que realizar las distintas tareas de administración:
1. **Lado del SERVER**:
De forma manual, lo único que tiene que hacer el administrador de sistemas que se encargue de este entorno es hacer un:
`sudo /opt/puppetlabs/bin/puppetserver ca sign --all` para firmar todos los certificados sin firmar que le han llegado (en este caso uno por cada nodo cliente) y mandarselos firmados a los clientes correspondientes. 
- De forma voluntaria pero recomendable a nivel de seguridad sobre todo en entornos más reales de producción, deberia de ejecutar **antes** de firmarlos un:
`sudo /opt/puppetlabs/bin/puppetserver ca list --all` para listar todos los certificados y verificar que no firma un certificado que no deberia.
2. **Lado del CLIENTE**:
Una vez hecho esto en el server, al cliente correspondiente le debe de llegar su certificado ya firmado, con el que podrá comunicarse ante el nodo master y
pedirle la configuraciones/aprovisionamiento de puppet ejecutando este comando: `sudo /opt/puppetlabs/bin/puppet agent --test` 


## Estructura general del proyecto de aprovisionamiento con puppet

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

Despliegue del entorno en la versión puppet-one-node:
{{< youtube "xQdjuHr-2-U" >}}
