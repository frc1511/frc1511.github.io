---
title: ThunderAuto - Creating a Project
---

# Creating a ThunderAuto Project

When you open ThunderAuto, you will be presented with the Welcome Page. Click __Open Project__ to open an existing ThunderAuto project, or __New Project__ to create a new one.

<figure markdown="span">
![ThunderAuto Welcome Page](../../assets/thunderauto/welcome.png){width="400"}
</figure>

Upon clicking __New Project__, the New Project dialog will appear:

<figure markdown="span">
![ThunderAuto New Project Dialog](../../assets/thunderauto/new_project.png){width="320"}
</figure>

Fill out the following fields in the New Project dialog:

- __Path__: The path to save the ThunderAuto project to.
    - If you plan to use ThunderLib to read the project on the robot, provide a path to somewhere in the `src/main/deploy/` directory of your robot project.
    - Project filename must end with `.thunderauto`
- __Field__: The FRC game field to create the project for.
- __Controller Type__: The type of drivetrain controller the robot uses - only __Holonomic__ (swerve) is currently supported.
- __Robot Length__, __Robot Width__: The dimensions of the robot. These values are only used for displaying the robot in the editor, and do not affect trajectory generation.

Click __Create__ to create the project, and the ThunderAuto editor will open.