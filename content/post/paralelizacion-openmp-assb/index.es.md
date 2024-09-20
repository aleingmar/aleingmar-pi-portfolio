---
title: Computación paralela en procesadores multinúcleos con OpenMP.
description: Proyecto académico | Programa escrito de forma paralela en C con OpenMP que cálcula el valor del número Pi mediante el método Montecarlo aprovechando los múltiples núcleos del procesador multinúcleo de la máquina donde se ejecuta.  
slug: openmp-assb
date: 2023-10-01 00:00:00+0000
image: openmp-logo.png
categories:
    - Programación paralela
tags:
    - C
    - OpenMP
    - WSL
    - Bash
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado durante la asignatura de Arquitectura de Sistemas y Software de Base (ASSB) durante mi cuarto año de carrera. El objetivo principal era implementar un algoritmo para el cálculo del número Pi utilizando el método de MonteCarlo programando en C tanto de forma secuencial como utilizando técnicas de programación paralela para aprovechar al máximo los recursos de los procesadores multinúcleo mediante la librería OpenMP, que permite ejecutar código en múltiples hilos de manera eficiente.

Las principales tareas realizadas fueron las siguientes:

- **Desarrollo de la versión secuencial y paralela del algoritmo**: Implementé un programa que simula el lanzamiento de "dardos" aleatorios dentro de un cuadrado inscrito en un círculo. La relación entre los aciertos dentro del círculo y los lanzamientos totales permite calcular el valor de Pi. En la versión paralela, utilicé OpenMP para dividir el trabajo entre varios hilos, aprovechando al máximo los recursos de los procesadores multinúcleo.

- **Mediciones de tiempo y análisis de rendimiento**: Tras desarrollar las dos versiones del programa, realicé mediciones de tiempo para evaluar el rendimiento de la versión paralela en comparación con la secuencial. Utilicé diferentes configuraciones de hilos, desde un solo hilo hasta más del doble de los núcleos físicos del procesador, con el objetivo de analizar la aceleración y escalabilidad del algoritmo. La aceleración se calculó como la relación entre el tiempo de ejecución en un único hilo y el tiempo de ejecución con varios hilos.

- **Optimización y gestión de recursos compartidos**: Durante el desarrollo, fue necesario resolver problemas comunes de la programación paralela, como las condiciones de carrera. En este caso, utilicé directivas de OpenMP para definir variables privadas en cada hilo, evitando que varios hilos accedieran simultáneamente a las mismas variables globales y afectaran el resultado final.

- **Generación de gráficos de rendimiento**: Tras recopilar los datos de tiempos de ejecución y aceleración, generé gráficos para visualizar el rendimiento del programa a medida que aumentaba el número de hilos. Estos gráficos demostraron cómo la aplicación escalaba con un mayor número de hilos, destacando las ventajas y limitaciones de la paralelización en un entorno de memoria compartida. 


Documentación del proyecto: [**Visualizar documentación en pdf**](/post/paralelizacion-openmp-assb/ASSB-openmp.pdf)