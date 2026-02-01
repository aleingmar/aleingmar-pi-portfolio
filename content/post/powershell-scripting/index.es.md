---
title: PowerShell Scripting 
description: Proyecto académico | Programación de scripts de PowerShell para la automatización de tareas en entornos Windows
slug: powershell-scripting
date: 2025-02-17 00:00:00+0000
image: powershell-logo.png
categories:
    - SysAdmin

tags:
    - PowerShell
weight: 12       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura de Administración de Sistemas Cloud como parte del máster universitario oficial en Desarrollo y Operaciones (DevOps).

El objetivo principal del proyecto fue desarrollar scripts en Powershell para automatizar tareas comunes en entornos Windows, optimizando procesos que normalmente requerirían intervención manual.
## Piceladas conceptuales de PowerShell
PowerShell es el intérprete de comandos y lenguaje de scripting de Microsoft, diseñado específicamente para la administración de sistemas Windows. Se basa en un lenguaje orientado a objetos, lo que significa que la salida de los comandos no es simplemente texto, sino objetos estructurados con propiedades y métodos que pueden ser manipulados fácilmente.

Por ejemplo, en Bash, la comunicación entre procesos en las tuberías (|) se da en texto plano, lo que obliga a utilizar herramientas adicionales como grep, awk o sed para procesar la salida. En PowerShell, en cambio, las tuberías intercambian objetos, permitiendo trabajar directamente con sus atributos sin necesidad de hacer parsing de texto.

### Ejemplo Comparativo de PowerShell vs. Bash
**PowerShell (trabajando con objetos):**


`Get-Process | Where-Object { $_.CPU -gt 10 } | Select-Object Name, CPU`

Aquí, `Get-Process` devuelve una lista de procesos como objetos, y filtramos aquellos cuyo uso de CPU (`$_ .CPU`) sea mayor a 10. Luego, seleccionamos solo las propiedades Name y CPU.

**Bash (trabajando con texto):**

`ps aux | awk '$3 > 10 {print $11, $3}'`

`ps aux` devuelve la lista de procesos como texto plano, por lo que es necesario usar awk para extraer y comparar la tercera columna (uso de CPU).

## Tareas automatizadas mediante los scripts:
En concreto las cuatro tareas a automatizar son las siguientes:

1. **Listado de archivos según tamaño** 

Escribir un script que muestre un listado de los ficheros del directorio actual que ocupe más de 1024 bytes.

2. **Renombrado de archivos JPG con fecha** 

Escribir un script que renombre todos los ficheros con extensión JPG del directorio actual, añadiendo un prefijo con la fecha en formato año, mes, día. Por ejemplo, un fichero con nombre «imagen1.jpg» pasaría a llamarse «20240413-image1.jpg», si el script se ejecuta el 13 de abril de 2024.

3. **Monitorización del espacio en discos duros** 

Programar un script en PowerShell que muestre los discos duros con un porcentaje de espacio libre inferior a un parámetro dado. El script debe imprimir la letra de la unidad y los valores en GB de espacio libre y tamaño sin decimales. La expresión Get-WmiObject Win32_LogicalDisk recupera la información de los discos del sistema.

4. **Creación de un menú interactivo**

Programar un script que muestre un menú con las siguientes opciones, de manera que se ejecute la opción asociada al número que introduzca el usuario:
- Listar los servicios arrancados.
- Mostrar la fecha del sistema.
- Ejecutar el Bloc de notas.
- Ejecutar la Calculadora.
- Salir.



**Repositorio de GitHub:** 
https://github.com/aleingmar/Powershell-Scripting


## Vídeo de la experimentación y memoria del proyecto:
Documentación del proyecto: [**Visualizar documentación en pdf**](/post/powershell-scripting/PowershellScripting.pdf)

{{< youtube "trwkbmmlKwY" >}}

