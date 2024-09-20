---
title: Parallel computing in distributed systems with MPI.
description: Academic project | Programs developed in parallel in C with MPI to calculate the vector product of vectors and to calculate integrals with the method of trapezoids taking advantage of the multiple machines in the cluster where it is executed. 
slug: mpi-assb
date: 2023-11-01 00:00:00+0000
image: mpi-logo.png
categories:
    - Parallel Programming
tags:
    - C
    - MPI
    - WSL
    - Bash
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the course Architecture of Systems and Software Basis (ASSB), during my fourth year of studies. The main objective was to become familiar with parallel programming on distributed memory computers using the **MPI** library in **C** (Message-Passing Interface). A widely used technique for distributed computing on multiple machines, commonly used in high performance clusters. In the case of this project everything was executed in my own computer, understanding my computer as a kind of cluster and its different cores as machines that form it.

The main tasks of this project are:

- **Development of the ‘Hello World’ program with MPI**: As a first step, I programmed a basic program so that **each process would print a message with its rank and the name of the processor it was running on**. In addition, I experimented with the possibility of launching more processes than the number of physical cores available, observing how MPI handles this scenario even though it loses performance.

- **Scalar product of vectors in parallel**: I implemented a program with MPI that **computes the scalar product of two large vectors**, distributing the work among several processes. Each process calculated a part of the scalar product, and then the results were brought together in the process of rank 0, which displayed the total result. A runtime measurement was also added, allowing analysis of how performance varied as the number of processes changed.

- **Solving integrals using the trapezoid method**: I then **implemented a program to calculate integrals using the trapezoid method**, parallelising the program so that each process calculated the sum of the trapezoids in a specific sub-interval. As before, the process at rank 0 was responsible for summing the results of all the processes and displaying the final value of the integral.

- **Performance and scalability analysis**: To evaluate the performance of the parallel program, I measured execution times and speedup when using different numbers of processes, from 1 to more than twice the number of available physical cores. The results were visualised in graphs showing how speedup improved as the number of processes increased, but also how efficiency decreased at certain points due to overhead in inter-process communication.

Project documentation: [**View documentation in pdf**](/post/paralelizacion-mpi-assb/ASSB-mpi.pdf)