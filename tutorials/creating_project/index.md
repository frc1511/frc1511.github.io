---
layout: page
title: Creating a Project
nav_order: 1
parent: Tutorials
---

# Creating a Project

To create a robot project in WPILib VS Code, follow the steps listed below.

First, click the WPILib icon in the top right corner of WPILib VS Code and search for "Create a new project" in the command palette.

<img src="/assets/images/wpilib/vscode/new_project_1.webp" width=800>

Then you should see the "New Project Creator Window"

<img src="/assets/images/wpilib/vscode/new_project_2.webp" width=800>

1. __Project Type:__ This is the type of the project. Select "Template".
2. __Language:__ This is the programming language of the project. We always use "C++".
3. __Project Base:__ This is template that the project will be based on. We use "Timed Robot".
4. __Base Folder:__ The folder on the computer where the project will be stored (ex. Documents folder).
5. __Project Name:__ The name of the project (ex. Homer or thunderbot2023).
6. __Create a New Folder:__ Select this if you want it to create a new folder named `Project Name` in the `Base Folder` (You usually do).
7. __Team Number:__ The team number (1511 unless you're a traitor).
8. __Enable Desktop Support:__ This is for simulating the robot code on your computer. I've never used it, and you probably won't either, so just leave it unchecked unless you're feeling adventurous. (I've seen this break some builds because not every library works with desktop support).

Once all the fields have been configured, click "Generate Project" and the project will be created. VS Code should then prompt you to open the project.