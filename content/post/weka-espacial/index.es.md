---
title: Proyecto de datos con Weka
description: Proyecto académico | Proyecto de análisis de datos con Weka para predecir qué pasajeros serían transportados a una dimensión alternativa por un accidente durante viaje espacial.
slug: weka-espacial
date: 2021-10-01 00:00:00+0000
image: weka.png
categories:
    - Análisis de datos
    - Aprendizaje Automático
tags:
    - Weka
weight: 50       ## You can add weight to some posts to override the default sorting (date descending)
---

Este proyecto fue desarrollado como parte de la asignatura de Sistemas Inteligentes (SI) durante mi tercer año de carrera. El trabajo consistió en aplicar diferentes algoritmos de clasificación y preprocesamiento de datos para resolver un problema hipotético sobre un viaje espacial en un futuro distante. El objetivo principal era predecir, basado en ciertos atributos de los pasajeros, si estos serían transportados a una dimensión alternativa tras un accidente espacial.

## Contexto y Objetivo
El problema plantea la situación en la que una nave espacial, con miles de pasajeros a bordo, choca con una anomalía espacio-temporal, y la mitad de los pasajeros son transportados a otra dimensión. El reto del proyecto consistía en desarrollar un modelo predictivo para identificar qué pasajeros habrían sido transportados a esa dimensión alternativa, basado en atributos como la edad, el planeta de origen, si estaban en crio sueño, y otros factores.

## Preprocesamiento de Datos
El conjunto de datos proporcionado contenía información sobre aproximadamente 8700 pasajeros, y constaba de 14 atributos, tanto numéricos como nominales. Inicialmente, se eliminaron ciertas variables consideradas irrelevantes, como el destino del pasajero y las cantidades gastadas en servicios de lujo. A continuación, se realizaron imputaciones de valores perdidos y se binarizaron las variables categóricas utilizando One Hot Encoding.

Para mejorar la eficiencia de los algoritmos de clasificación basados en distancia, como KNN, se realizó la normalización de las variables numéricas, en particular la edad de los pasajeros, con el fin de garantizar una comparación justa entre los diferentes atributos.

## Algoritmos Implementados
Se probaron diversos algoritmos de clasificación, entre ellos:

- **ZeroR**: Utilizado como baseline, clasificando todos los pasajeros en función del valor de la clase más frecuente.
- **J48**: Un algoritmo de tipo árbol de decisión que mostró buenos resultados tras un proceso de poda para evitar el sobreajuste.
- **KNN** (k-Nearest Neighbors): Este clasificador se basó en la similitud entre individuos para predecir si un pasajero sería transportado. Se probaron diferentes valores de K, siendo 9 el valor que obtuvo mejores resultados.
- **Naive Bayes**: Un algoritmo que, pese a su simplicidad, proporcionó buenos resultados al asumir la independencia entre los atributos.

## Resultados
El mejor rendimiento se obtuvo utilizando el algoritmo KNN con un valor de K=9, logrando una precisión del 74.3%. En comparación, los otros algoritmos mostraron rendimientos ligeramente inferiores. Los experimentos realizados con **validación cruzada** ayudaron a evaluar de manera más confiable los modelos, asegurando que no hubiese sobreajuste.


Documentación del proyecto: [**Visualizar documentación en pdf**](/post/weka-espacial/viaje-espacial-weka.pdf)