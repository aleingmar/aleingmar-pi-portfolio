---
title: PowerShell Scripting 
description: Academic project | Programming PowerShell scripts for task automation in Windows environments
slug: powershell-scripting
date: 2025-02-17 00:00:00+0000
image: powershell-logo.png
categories:
    - SysAdmin

tags:
    - PowerShell
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

This project was developed for the Cloud Systems Administration subject as part of the official university master's degree in Development and Operations (DevOps).

The main objective of the project was to develop scripts in Powershell to automate common tasks in Windows environments, streamlining processes that would normally require manual intervention.

## PowerShell conceptual snapshots
PowerShell is Microsoft's command interpreter and scripting language, designed specifically for Windows system administration. It is based on an object-oriented language, which means that the output of commands is not simply text, but structured objects with properties and methods that can be easily manipulated.

For example, in Bash, inter-process communication in pipes (|) is in plain text, which forces the use of additional tools such as grep, awk or sed to process the output. In PowerShell, on the other hand, pipelines exchange objects, allowing you to work directly with their attributes without the need to pause and restart the pipeline.

### Example Comparison of PowerShell vs. Bash
**PowerShell (working with objects):**

`Get-Process | Where-Object { $_.CPU -gt 10 } | Select-Object Name, CPU`

Here, `Get-Process` returns a list of processes as objects, and we filter out those whose CPU usage (`$_ .CPU`) is greater than 10. Then, we select only the Name and CPU properties.

**Bash (working with text):**

`ps aux | awk '$3 > 10 {print $11, $3}'`

`ps aux` returns the list of processes as plain text, so it is necessary to use awk to extract and compare the third column (CPU usage).

## Tasks automated by means of scripts:
Specifically the four tasks to be automated are as follows:

1. **Listing files by size** 

Write a script that displays a list of files in the current directory that are larger than 1024 bytes.

2. **Rename JPG files by date** 

Write a script that renames all files with a JPG extension in the current directory, adding a date prefix in year, month, day format. For example, a file named "image1.jpg" would be renamed to "20240413-image1.jpg", if the script is run on 13 April 2024.

3. **Hard disk space monitoring**

Program a PowerShell script that displays hard disks with a percentage of free space below a given parameter. The script should print the drive letter and the values in GB of free space and size without decimals. The expression Get-WmiObject Win32_LogicalDisk retrieves the information of the system disks.

4. **Creating an interactive menu**

Program a script that displays a menu with the following options, so that the option associated with the number entered by the user is executed:
- List the services started.
- Display the system date.
- Execute the Notepad.
- Run the Calculator.
- Exit.

**GitHub repository:** 
https://github.com/aleingmar/Powershell-Scripting


## Experimentation video and project report:
Project documentation: [**View documentation in pdf**](/post/powershell-scripting/PowershellScripting.pdf)

{{< youtube "trwkbmmlKwY" >}}