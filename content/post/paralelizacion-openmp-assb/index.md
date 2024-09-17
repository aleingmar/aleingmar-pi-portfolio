---
title: Parallel computing on multicore processors with OpenMP.
description: Academic project | Program written in parallel in C with OpenMP that calculates the value of the number Pi by means of the Monte Carlo method taking advantage of the multiple cores of the multicore processor of the machine where it is executed.  
slug: openmp-assb
date: 2023-10-01 00:00:00+0000
image: openmp-logo.png
categories:
    - Parallel Programming
tags:
    - C
    - OpenMP
    - WSL
    - Bash
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed during the Systems and Software Architecture and Basis (ASSB) course during my fourth year of studies. The main objective was to implement an algorithm for calculating the Pi number using the MonteCarlo method by programming in C both sequentially and using parallel programming techniques to take full advantage of the resources of multicore processors using the OpenMP library, which allows code to be executed in multiple threads efficiently.

The main tasks performed were the following:

- **Development of the sequential and parallel version of the algorithm**: I implemented a program that simulates the throwing of random ‘darts’ inside a square inscribed in a circle. The ratio between the hits inside the circle and the total throws is used to calculate the value of Pi. In the parallel version, I used OpenMP to divide the work among several threads, taking full advantage of the resources of multi-core processors.

- **Time measurements and performance analysis**: After developing the two versions of the program, I performed time measurements to evaluate the performance of the parallel version compared to the sequential version. I used different thread configurations, from a single thread to more than twice the physical cores of the processor, in order to analyse the speedup and scalability of the algorithm. The speedup was calculated as the ratio between the single-threaded execution time and the multi-threaded execution time.

- **Optimisation and management of shared resources**: During development, it was necessary to solve common problems in parallel programming, such as race conditions. In this case, I used OpenMP directives to define private variables on a per-thread basis, preventing multiple threads from simultaneously accessing the same global variables and affecting the final result.

- **Generating performance graphs**: After collecting runtime and speedup data, I generated graphs to visualise the performance of the program as the number of threads increased. These graphs demonstrated how the application scaled with increased thread count, highlighting the advantages and limitations of parallelisation in a shared-memory environment. 

Project documentation: [**View documentation in pdf**](ASSB-openmp.pdf)