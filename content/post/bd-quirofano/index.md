---
title: Relational database for the management of operating room equipment.
description: Academic project | Relational database for the management of facilities and electromedical equipment for operating theatres.
slug: bd-quirofano
date: 2021-04-01 00:00:00+0000
image: bd.png
categories:
    - Databases
tags:
    - SQL
    - MariaDB
    - HeidiSQL
weight: 50       # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed during the Database (DB) course during my second year of my degree. The main objective was to design, model and develop a SQL database to manage and store the information of the electromedical facilities and equipment of an operating theatre. The database would allow not only to manage the equipment and its maintenance, but also to ensure compliance with health regulations, to control the value of the equipment, to supervise periodic revisions...

Some of the tasks performed include:

- **Design and modelling of the database**: Based on an exhaustive analysis of the requirements, a relational model was developed representing the different elements of the operating theatre, the electro-medical equipment, the air conditioning and electrical installations, and the profiles of the users managing this information (biomedical engineers, maintenance engineers and general services managers).

- **Equipment lifecycle management**: The database stores key information about the equipment, such as its acquisition date, useful life, supplier, purchase value and technical parameters that must be kept within certain ranges to ensure its correct functioning. This allows maintenance schedules to be controlled and replacements to be planned in a timely manner.

- **Automation of overhauls**: Through **triggers** and **stored procedures**, the database is able to generate alerts when overhaul dates are approaching or when a piece of equipment is close to exceeding its useful life. This ensures that the OR is maintained to the required standards without unplanned interruptions.

- **Advanced queries and reporting**: Implementation of a series of **views** and **queries** to provide easy access to relevant information, such as overhaul status, total equipment cost and engineers' maintenance history. This allows users to obtain customised reports that can be used for strategic decision making within the hospital.

Project documentation: [**View documentation in pdf**](/post/bd-quirofano/bd-quirofano.pdf)