---
title: Data project with Weka
description: Academic project | Data analysis project with Weka to predict which passengers would be transported to an alternative dimension by an accident during space travel.
slug: weka-espacial
date: 2021-10-01 00:00:00+0000
image: weka.png
categories:
    - Data Analysis
    - Machine Learning
tags:
    - Weka
weight: 6 # You can add weight to some posts to override the default sorting (date descending)
---
This project was developed as part of the Intelligent Systems (IS) course during my third year of studies. The work consisted of applying different classification and data pre-processing algorithms to solve a hypothetical problem about space travel in the distant future. The main objective was to predict, based on certain attributes of the passengers, whether they would be transported to an alternative dimension after a space accident.

## Context and Objective
The problem posed the situation where a spacecraft, with thousands of passengers on board, collides with a space-time anomaly, and half of the passengers are transported to another dimension. The challenge of the project was to develop a predictive model to identify which passengers would have been transported to that alternate dimension, based on attributes such as age, planet of origin, whether they were in cryo-sleep, and other factors.

## Data Preprocessing
The dataset provided contained information on approximately 8700 passengers, and consisted of 14 attributes, both numerical and nominal. Initially, certain variables considered irrelevant, such as passenger destination and amounts spent on luxury services, were removed. Next, missing value imputations were performed and categorical variables were binarised using One Hot Encoding.

To improve the efficiency of distance-based ranking algorithms such as KNN, normalisation of numerical variables, in particular passenger age, was performed to ensure a fair comparison between the different attributes.

## Algorithms Implemented
Several classification algorithms were tested, including:

- **ZeroR**: Used as a baseline, classifying all passengers based on the value of the most frequent class.
- **J48**: A decision tree type algorithm that showed good results after a pruning process to avoid overfitting.
- **KNN** (k-Nearest Neighbors): This classifier was based on the similarity between individuals to predict whether a passenger would be transported. Different values of K were tested, with 9 being the best performing value.
- **Naive Bayes**: An algorithm that, despite its simplicity, provided good results by assuming independence between attributes.

## Results
The best performance was obtained using the KNN algorithm with a value of K=9, achieving an accuracy of 74.3%. In comparison, the other algorithms showed slightly lower performances. The experiments performed with **cross-validation** helped to more reliably evaluate the models, ensuring that there was no over-fitting.


Project documentation: [**View documentation in pdf**](/post/weka-espacial/viaje-espacial-weka.pdf)