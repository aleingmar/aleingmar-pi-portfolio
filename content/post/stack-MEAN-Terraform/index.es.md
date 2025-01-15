---
title: Despliegue automático de servicio MEAN multicapa en AWS
description: Proyecto académico | Creación y despliegue automático de un sistema MEAN multicapa en AWS mediante Terraform, Packer y Ansible. Infraestructura modular con balanceador de carga, múltiples instancias para el aplicativo y una base de datos MongoDB.
slug: stack-mean-terraform
date: 2025-01-14 00:00:00+0000
image: stack.png
categories:
    - DevOps
    - Cloud

tags:
    - Packer
    - Terraform
    - Ansible
    - MongoDB
    - Angular
    - Express
    - AWS
    - NginX
    - MV's
    - Bash
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura de Herramientas DevOps, como parte del máster universitario en Desarrollo y Operaciones (DevOps).

El objetivo del proyecto fue desplegar de forma automática un sistema MEAN multicapa completamente funcional en la nube de AWS. Este sistema se compone de un balanceador de carga, varias instancias para la aplicación web y una instancia dedicada para la base de datos MongoDB. Utilizo Terraform, Packer y Ansible para la automatización de infraestructura y aprovisionamiento.

### Stack Tecnológico

- **Terraform**:  con terraform centralizo todo el proceso de despliegue y gestiono elementos de infraestructura como son las redes, instancias, balanceadores de carga... elementos que me sirven para sustentar el servicio.

- **Packer**: con packer creo imágenes que me sirven como base para las instancias que levanto con Terraform. En este proyecto, Packer genera una imagen personalizada para la primera capa del sistema, aprovisionándola con los servicios necesarios como Node.js, Nginx, Angular...

- **Ansible**: con Ansible realizo el aprovisionamiento de la instancia que levanta y usa Packer para la creación de la imagen. En este proyecto, Ansible aprovisiona de forma automática la instancia con Angular, Express, MongoDB, Nginx, Node...

- **Stack MEAN**: El sistema levanta un servicio con el stack tecnológico MEAN, ampliamente utilizado en la industria por su versatilidad y rendimiento:
    - **MongoDB**: Base de datos no relacional orientada a documentos, ideal para manejar grandes volúmenes de datos estructurados y no estructurados.
    - **Express**: Framework backend para Node.js que facilita el desarrollo de aplicaciones web robustas y escalables.

    - **Angular**: Framework frontend que permite desarrollar interfaces modernas y reactivas, mejorando la experiencia del usuario.

    - **Node.js**: Entorno de ejecución para Js en el lado del servidor.

### Modularización de la plantilla Terraform

#### Importancia de la modularización

La modularización en Terraform no solo mejora la legibilidad y mantenimiento del código, sino que también permite dividir responsabilidades y reutilizar configuraciones entre proyectos. Aunque la gestión de variables entre módulos puede ser compleja, esta práctica resulta esencial en infraestructuras grandes y dinámicas.

#### Módulos del proyecto

- **Módulo de seguridad**: Este módulo gestiona los grupos de seguridad que definen las reglas de tráfico hacia y desde las instancias, posibilitando tráfico de protocolos como SSH, HTTP... También se configuran las claves SSH necesarias para acceder a las instancias de forma remota.

- **Módulo de redes**: Define las redes y subredes privadas necesarias para la conectividad del sistema. Configura tablas de enrutamiento y gateways para garantizar el acceso entre las capas de la infraestructura.

- **Módulo de instancias**: Despliega las instancias de la primera y segunda capa, asignando direcciones IP públicas y privadas. Aprovisiona las instancias para su correcto funcionamiento en el sistema.

- **Módulo de balanceador de carga**: Configura el balanceador de carga que distribuye el tráfico entre las instancias de la primera capa. Define grupos de destino y estrategias de distribución como round-robin y sesiones persistentes para mejorar la disponibilidad y consistencia del sistema.

- **Módulo de imagen**: Integra Terraform con Packer para la creación de imágenes base. Terraform ejecuta packer build, recupera la imagen generada y la utiliza para instanciar recursos de la primera capa.

![Estructura de directorios](modulos.png)

### Proceso de despliegue

El despliegue comienza con la integración de Terraform y Packer. Terraform invoca a Packer, que se encarga de levantar una instancia temporal en AWS para generar una imagen base. Durante este proceso, la instancia es aprovisionada con Ansible, que instala y configura servicios como Angular, Express y MongoDB, además de copiar ficheros esenciales desde el entorno local. Una vez completado el aprovisionamiento, Packer crea la imagen base y destruye la instancia temporal, dejando preparada una imagen lista para su reutilización.

Con la imagen generada, Terraform procede a desplegar la infraestructura completa. En primer lugar, se configuran las redes y subredes, asegurando la conectividad interna entre las capas del sistema. A continuación, se despliegan las instancias de la primera capa utilizando la imagen base. Estas instancias alojan el frontend y backend de la aplicación, con Node.js y Nginx sirviendo como núcleo operativo.

Simultáneamente, Terraform levanta la instancia de la segunda capa, dedicada a la persistencia de datos con MongoDB. Esta instancia se conecta mediante una red privada a las instancias de la primera capa, garantizando una comunicación segura y estable. Además de esto, terraform también levanta un balanceador de carga, configurado para distribuir el tráfico entre las instancias de la primera capa, lo que asegura alta disponibilidad y escalabilidad.

El último paso es el aprovisionamiento final. Terraform utiliza scripting eh Bash para terminar de configurar las instancias desplegadas. Por ejemplo, en las instancias de la primera capa, se ajustan las configuraciones de Angular para incluir las direcciones IP del backend, lo que permite que se generen los ficheros estáticos que son servidos por Nginx con las rutas necesarias para conectar el cliente con el backend.

Todo este proceso asegura un despliegue completamente automatizado, resultando en un sistema funcional y listo para producción, con componentes integrados y configurados para ofrecer un rendimiento óptimo.


**Repositorio de GitHub:** 
https://github.com/aleingmar/Multi-layer_MEAN_Deployment


### Vídeo de la experimentación y memoria del proyecto:
Documentación del proyecto: [**Visualizar documentación en pdf**](/post/stack-MEAN-Terraform/Act2_StackMEAN_Terraform_AlejandroIngles.pdf)

{{< youtube "zRGhkBebEbA" >}}



