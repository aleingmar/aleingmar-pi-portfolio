---
title: Computación paralela en sistemas distribuidos con MPI.
description: Proyecto académico | Programas desarrollados de forma paralela en C con MPI para cálcular el producto vectorial de vectores y para calcular integrales con el método de los trapecios aprovechando las múltiples máquinas del clúster donde se ejecuta. 
slug: mpi-assb
date: 2023-11-01 00:00:00+0000
image: mpi-logo.png
categories:
    - Programación paralela
tags:
    - C
    - MPI
    - WSL
    - Bash
weight: 6       # You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado para la asignatura Arquitectura de Sistemas y Software de Base (ASSB), durante mi cuarto año de carrera. El objetivo principal era familiarizarse con la programación paralela en computadores de memoria distribuida utilizando la **librería MPI** en **C** (Message-Passing Interface). Una técnica muy utilizada para la computación distribuida en múltiples máquinas, comúnmente utilizado en clústeres de alto rendimiento. En el caso de este proyecto todo se ejecutó en mi propio computador, entendiendo mi computador como una especie de clúster y sus diferentes núcleos como máquinas que forman este.

Las principales tareas de este proyecto son:

- **Desarrollo del programa de "Hola Mundo" con MPI**: Como primer paso, programé un programa básico para que **cada proceso imprimiera un mensaje con su rango y el nombre del procesador en el que estaba ejecutándose**. Además, experimenté con la posibilidad de lanzar más procesos que el número de núcleos físicos disponibles, observando cómo MPI gestiona este escenario aunque pierda rendimiento.

- **Producto escalar de vectores en paralelo**: Implementé un programa con MPI que **calcula el producto escalar de dos vectores** de gran tamaño, distribuyendo el trabajo entre varios procesos. Cada proceso calculaba una parte del producto escalar, y luego los resultados se reunían en el proceso de rango 0, que mostraba el resultado total. También se añadió una medición del tiempo de ejecución, lo que permitió analizar cómo variaba el rendimiento al cambiar el número de procesos.

- **Resolución de integrales con el método de los trapecios**: Posteriormente, **implementé un programa para calcular integrales mediante el método de los trapecios**, paralelizando el programa para que cada proceso calculara la suma de los trapecios en un subintervalo específico. Al igual que antes, el proceso de rango 0 era responsable de sumar los resultados de todos los procesos y mostrar el valor final de la integral.

- **Análisis de rendimiento y escalabilidad**: Para evaluar el rendimiento del programa paralelo, medí los tiempos de ejecución y la aceleración al utilizar diferentes cantidades de procesos, desde 1 hasta más del doble del número de núcleos físicos disponibles. Los resultados se visualizaron mediante gráficos que mostraban cómo la aceleración mejoraba conforme aumentaba el número de procesos, pero también cómo disminuía la eficiencia en ciertos puntos debido a la sobrecarga en la comunicación entre procesos.

Documentación del proyecto: [**Visualizar documentación en pdf**](/post/paralelizacion-mpi-assb/ASSB-mpi.pdf)