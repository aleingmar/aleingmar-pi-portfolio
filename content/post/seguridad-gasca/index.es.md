---
title: Implementación de una Arquitectura Segura Cliente-Servidor en Java utilizando TLS
description: Proyecto académico | Implementación de una Arquitectura Segura Cliente-Servidor en Java utilizando TLS para asegurar las comunicaciones.
slug: seguridad-gasca
date: 2021-12-01 00:00:00+0000
image: java3.png
categories:
    - Ciberseguridad
tags:
    - WSL
    - Java
    - Wireshark
    - OpenSSL
weight: 1       ## You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado durante la asignatura de Seguridad, Confidencialidad y Gestión de la Identidad (SCGI) durante mi tercer año de carrera. Este proyecto se centró en el diseño y desarrollo de una arquitectura cliente-servidor segura utilizando el protocolo Transport Layer Security (TLS), con el objetivo de asegurar la confidencialidad, integridad y autenticidad de las comunicaciones.

## Contexto y Objetivo
El proyecto surgió de la necesidad de asegurar las comunicaciones en una aplicación que permitiera la transmisión de datos sensibles, como credenciales de usuario (login/password), entre clientes y un servidor central. Este tipo de aplicaciones es especialmente relevante en entornos donde la privacidad de los datos es crucial, como el sector de la salud, la banca y cualquier sistema donde los usuarios deban autenticar su identidad para acceder a servicios.

## Configuración de KeyStores y TrustStores
Para implementar la seguridad mediante TLS, fue necesario configurar tanto el almacén de claves (KeyStore) como el almacén de certificados (TrustStore). Estos elementos permiten la autenticación mutua entre el cliente y el servidor. El KeyStore contiene las claves privadas y los certificados asociados que identifican a la entidad (cliente o servidor), mientras que el TrustStore gestiona los certificados de las entidades de confianza, permitiendo validar que las contrapartes de la comunicación son legítimas.

En el desarrollo de este proyecto, se utilizó Keytool, una herramienta incluida en el JDK de **Java**, para crear y gestionar los certificados. El proceso requirió la configuración de las variables de entorno como JAVA_HOME y PATH, para facilitar el uso de esta herramienta desde la línea de comandos.

## Implementación de Sockets TLS
La comunicación entre el cliente y el servidor se realizó mediante sockets SSL (Secure Sockets Layer), sobre los cuales se integró el protocolo TLS. En ambos extremos, cliente y servidor, se configuraron sockets seguros que permitían la transmisión de datos encriptados. El servidor estaba diseñado para escuchar conexiones entrantes en un puerto específico (en este caso, el puerto 3343), autenticando a los clientes mediante la verificación de sus credenciales.

- **Servidor TLS**: El servidor se encargaba de recibir las conexiones de los clientes y autenticar a cada usuario mediante la verificación de sus credenciales (nombre de usuario y contraseña). Además, proporcionaba respuestas basadas en el resultado de esta verificación, informando al cliente si la autenticación había sido exitosa o fallida.

- **Cliente TLS**: El cliente establecía una conexión segura con el servidor y enviaba las credenciales del usuario para su verificación. La respuesta del servidor se mostraba en una interfaz de usuario sencilla, indicando si el proceso de autenticación había sido exitoso o si hubo algún error.

## Pruebas de Comunicación y Seguridad
Se realizaron pruebas de comunicación tanto con seguridad como sin ella, con el fin de destacar la importancia del uso de TLS en aplicaciones que manejan información sensible. Para las pruebas sin seguridad, se implementó un socket sin cifrado que permitía observar cómo un atacante, usando herramientas como **Wireshark**, podía capturar y visualizar en texto claro las credenciales de usuario transmitidas.

En contraste, al habilitar TLS, se observó cómo toda la información transmitida se encontraba encriptada, imposibilitando que un atacante pudiera leer los datos capturados en la red. Esto demostró la efectividad de TLS para proteger la confidencialidad y la integridad de la información.

## Rendimiento y Concurrencia
Un aspecto clave de este proyecto fue la validación del rendimiento del sistema, específicamente la capacidad de manejar múltiples conexiones concurrentes. El servidor fue configurado para gestionar hasta 300 conexiones simultáneas, lo cual fue logrado utilizando hilos (threads) en Java para manejar las solicitudes en paralelo. A pesar de que las conexiones se realizaban de forma secuencial en las pruebas iniciales (una cada segundo), el sistema demostró ser robusto al procesar las peticiones de forma eficiente sin comprometer la seguridad o la estabilidad.

Documentación del proyecto: [**Visualizar documentación en pdf**](/post/seguridad-gasca/conexion_TLS.pdf)