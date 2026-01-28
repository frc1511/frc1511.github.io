---
title: ThunderLib - ThunderAuto Integration
---

# ThunderAuto Integration

## Example Robot Projects

See the following example robot projects that demonstrate how to use ThunderLib to load and run ThunderAuto projects on the robot:

- [ThunderAuto Example - Java](https://github.com/frc1511/ThunderLib/tree/main/examples/ThunderAuto/java)
- [ThunderAuto Example - C++](https://github.com/frc1511/ThunderLib/tree/main/examples/ThunderAuto/cpp)

These example projects were built to be functional in simulation, see the README files in each project for instructions on how to run them. 

??? note "Simulation Video"
    <figure markdown="span">
        ![](../../assets/thunderlib/thunderauto_example_project_simulation.mp4){ loading="lazy"}
        <figcaption>ThunderAuto-ThunderLib Example Project (2023) - Simulation</figcaption>
    </figure>

## Loading ThunderAuto Projects

The `ThunderAutoProject` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoProject.html)/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoProject.html)) class can be used to load ThunderAuto project files.
The `ThunderAutoProject` class provides access to the trajectories and autonomous modes defined in the ThunderAuto project.

=== "Java"

    ```java
    ThunderAutoProject autoProject = new ThunderAutoProject("ProjectName");
    ```

=== "C++"

    ```c++
    auto autoProject = std::make_shared<thunder::ThunderAutoProject>("ProjectName");
    ```

You can either provide an absolute path to the project file, or a path relative to the robot code's deploy directory. The file extension `.thunderauto` is optional and will be added automatically if not provided.

To check if the project was loaded successfully, use the `isLoaded` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoProject.html#isLoaded())/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoProject.html#a21aa1a1bf633150c6d1cfb820d6314de)) method. ThunderLib will log any errors encountered during loading to stderr.

=== "Java"

    ```java
    if (!autoProject.isLoaded()) {
        System.err.println("Failed to load ThunderAuto project: " + autoProject.getName());
        // Handle error...
    }
    ```

=== "C++"

    ```c++
    if (!autoProject->isLoaded()) {
        std::cerr << "Failed to load ThunderAuto project: " << autoProject->getName() << std::endl;
        // Handle error...
    }
    ```

### Registering Action Commands to the Project

Before running trajectories or autonomous modes from a ThunderAuto project, you must first register any [Command Actions](../thunderauto/actions.md) that are referenced in the trajectories or autonomous modes.
These commands will be executed when they are encountered during the execution of a trajectory/auto mode. If an action command does not get registered, ThunderLib will just skip it during execution.

To register action commands, use the `registerActionCommand` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoProject.html#registerActionCommand(java.lang.String,edu.wpi.first.wpilibj2.command.Command))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoProject.html#a03a91f2cab3d87ac24a01fec7e9c8b51)) method of the `ThunderAutoProject` class. 

=== "Java"

    ```java
    // Print command
    autoProject.registerActionCommand("SayHello", Commands.print("Hello, World!"));

    // Custom command
    autoProject.registerActionCommand("MyCustomCommand", new MyCustomCommand());
    ```

=== "C++"

    ```c++
    // Print command
    autoProject->registerActionCommand("SayHello", frc2::cmd::print("Hello, World!"));

    // Custom command
    autoProject->registerActionCommand("MyCustomCommand", std::make_shared<MyCustomCommand>());
    ```

### Registering Auto Mode Conditions to the Project

If an autonomous mode in the ThunderAuto project includes a boolean or switch condition step, you must register the corresponding condition functions to the project using the `registerBooleanCondition` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoProject.html#registerBooleanCondition(java.lang.String,java.util.function.BooleanSupplier))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoProject.html#a892c3eddcbe3eaf0abe02eb7b478d740)) and `registerSwitchCondition` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoProject.html#registerSwitchCondition(java.lang.String,java.util.function.IntSupplier))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoProject.html#a841c390c81b06112f4b9217ee3830be6)) methods.

=== "Java"

    ```java
    // Boolean condition
    autoProject.registerBooleanCondition("HasGamePiece", () -> gamePieceSubsystem.hasGamePiece());

    // Switch condition
    autoProject.registerSwitchCondition("NumberOfGamePieces", () -> gamePieceSubsystem.getNumberOfGamePieces());
    ```

=== "C++"

    ```c++
    // Boolean condition
    autoProject->registerBooleanCondition("HasGamePiece", [&]() {
        return gamePieceSubsystem->hasGamePiece();
    });

    // Switch condition
    autoProject->registerSwitchCondition("NumberOfGamePieces", [&]() {
        return gamePieceSubsystem->getNumberOfGamePieces();
    });
    ```

## Select Trajectories and/or Auto Modes from Dashboard

ThunderLib provides a `ThunderAutoSendableChooser` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoSendableChooser.html)/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoSendableChooser.html)) class, which is a wrapper around WPILib's `SendableChooser` class. `ThunderAutoSendableChooser` handles ThunderAuto trajectory and autonomous mode selections from one or more projects, and provides the appropriate command to run when requested.

!!! note
    `ThunderAutoSendableChooser` will always include a default "Do Nothing" option that returns a __None__ command. It is not possible to set a different default option, or to set a different command to the "Do Nothing" choice.

To create a `ThunderAutoSendableChooser`, simply provide the key to publish it as on the SmartDashboard. Whenever changes are made to the chooser (e.g. via methods or [Remote Project Updates](../thunderauto/remote-updates.md)), the SmartDashboard topic will automatically get updated.

=== "Java"

    ```java
    // Publish to SmartDashboard as "Auto_Mode".
    // The published chooser will automatically get updated whenever changes are made.
    ThunderAutoSendableChooser autoChooser = new ThunderAutoSendableChooser("Auto_Mode");
    ```

=== "C++"

    ```c++
    // Publish to SmartDashboard as "Auto_Mode".
    // The published chooser will automatically get updated whenever changes are made.
    auto autoChooser = std::make_shared<thunder::ThunderAutoSendableChooser>("Auto_Mode");
    ```

### Add Trajectories and Auto Modes to the Chooser

To add items from a ThunderAuto Project to the chooser, you must first include the project using the `includeProjectSource` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoSendableChooser.html#includeProjectSource(com.thunder.lib.auto.ThunderAutoProject))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoSendableChooser.html#a568e804f541d80829d02db18c5b80d0c)) method. Once the project is included, you can add trajectories and autonomous modes from the project to the chooser.

=== "Java"

    ```java
    // Include the project.
    autoChooser.includeProjectSource(autoProject);

    // Add a trajectory from the project to the chooser.
    autoChooser.addTrajectoryFromProject(autoProject.getName(), "MyTrajectory");

    // Add all auto modes from the project to the chooser.
    autoChooser.addAllAutoModesFromProject(autoProject.getName());
    ```

=== "C++"

    ```c++
    // Include the project.
    autoChooser->includeProjectSource(autoProject);

    // Add a trajectory from the project to the chooser.
    autoChooser->addTrajectoryFromProject(autoProject->getName(), "MyTrajectory");

    // Add all auto modes from the project to the chooser.
    autoChooser->addAllAutoModesFromProject(autoProject->getName());
    ```

In order for the chooser to construct the appropriate commands for the selected trajectories and auto modes, the robot's `TrajectoryRunnerProperties` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/trajectory/ThunderTrajectoryRunnerProperties.html)/[C++](https://frc1511.github.io/ThunderLib/api/cpp/structthunder_1_1TrajectoryRunnerProperties.html)) must be provided to the chooser using using the `setTrajectoryRunnerProperties` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoSendableChooser.html#setTrajectoryRunnerProperties(com.thunder.lib.trajectory.ThunderTrajectoryRunnerProperties))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoSendableChooser.html#a07f8a5a731817600e769410958d77ba1)) method.

=== "Java"

    ```java
    autoChooser.setTrajectoryRunnerProperties(driveSubsystem.getTrajectoryRunnerProperties());
    ```

=== "C++"

    ```c++
    autoChooser->setTrajectoryRunnerProperties(driveSubsystem->getTrajectoryRunnerProperties());
    ```

??? info "How to construct `TrajectoryRunnerProperties`"
    We recommend creating a method in your drive subsystem that returns a `TrajectoryRunnerProperties` object configured for your robot.

    See the examples below, or the example robot projects ([Java](https://github.com/frc1511/ThunderLib/blob/main/examples/ThunderAuto/java/src/main/java/frc/robot/subsystems/DriveSubsystem.java)/C++ [Header](https://github.com/frc1511/ThunderLib/blob/main/examples/ThunderAuto/cpp/src/main/include/subsystems/DriveSubsystem.h)/[Source](https://github.com/frc1511/ThunderLib/blob/main/examples/ThunderAuto/cpp/src/main/cpp/subsystems/DriveSubsystem.cpp)).

    === "Java"

        ```java
        public class DriveSubsystem extends SubsystemBase {
            private PIDController xController = new PIDController(kDriveP, kDriveI, kDriveD);
            private PIDController yController = new PIDController(kDriveP, kDriveI, kDriveD);
            private ProfiledPIDController thetaController = new ProfiledPIDController(kDriveThetaP, kDriveThetaI, kDriveThetaD,
                // This profile is not important because ThunderAuto handles angular
                // acceleration limits. You should make sure these limits are >= those in
                // ThunderAuto so they don't interfere.
                new TrapezoidProfile.Constraints(kDriveMaxAngularVelocity, kDriveMaxAngularAcceleration));

            private HolonomicDriveController holonomicDriveController = new HolonomicDriveController(
                xController, yController, thetaController);

            private ThunderTrajectoryRunnerProperties trajectoryRunnerProperties = new ThunderTrajectoryRunnerProperties(
                this::getCurrentPose,
                this::setCurrentPose,
                this::setChassisSpeeds,
                holonomicDriveController);

            // Define other members (swerve modules, gyro, kinematics, odometry, etc.)

            public ThunderTrajectoryRunnerProperties getTrajectoryRunnerProperties() {
                return trajectoryRunnerProperties;
            }

            public Pose2d getCurrentPose() {
                // Get current odometry pose
            }

            public void setCurrentPose(Pose2d pose) {
                // Reset odometry pose

                // Important - reset controllers to prevent sudden jumps. ThunderLib does not do this for you.
                xController.reset();
                yController.reset();
                thetaController.reset(pose.getRotation().getRadians());
            }

            private void setChassisSpeeds(ChassisSpeeds speeds) {
                // Set module states
            }

            // Define other drive subsystem methods
        }
        ```

    === "C++"

        ```c++
        class DriveSubsystem : public frc2::SubsystemBase {
        private:
            std::shared_ptr<frc::HolonomicDriveController> holonomicDriveController =
                std::make_shared<frc::HolonomicDriveController>(
                    frc::PIDController{kDriveP, kDriveI, kDriveD}, // X
                    frc::PIDController{kDriveP, kDriveI, kDriveD}, // Y
                    frc::ProfiledPIDController<units::radians>{    // Theta
                        kDriveThetaP, kDriveThetaI, kDriveThetaD,
                        // This profile is not important because ThunderAuto handles angular acceleration limits. You
                        // should make sure these limits are >= those in ThunderAuto so they don't interfere.
                        {kDriveMaxAngularVelocity, kDriveMaxAngularAcceleration}
                    });

            const thunder::TrajectoryRunnerProperties trajectoryRunnerProperties{
                std::bind(&DriveSubsystem::GetCurrentPose, this),
                std::bind(&DriveSubsystem::SetCurrentPose, this, std::placeholders::_1),
                std::bind(&DriveSubsystem::SetChassisSpeeds, this, std::placeholders::_1),
                holonomicDriveController};

            // Define other members (swerve modules, gyro, kinematics, odometry, etc.)

        public:
            const thunder::TrajectoryRunnerProperties& getTrajectoryRunnerProperties() {
                return trajectoryRunnerProperties;
            }

            frc::Pose2d GetCurrentPose() const {
                // Get current odometry pose
            }

            void SetCurrentPose(const frc::Pose2d& pose) {
                // Reset odometry pose

                // Important - reset controllers to prevent sudden jumps. ThunderLib does not do this for you.
                holonomicDriveController->GetXController().Reset();
                holonomicDriveController->GetYController().Reset();
                holonomicDriveController->GetThetaController().Reset(pose.Rotation().Radians());
            }

            void SetChassisSpeeds(const frc::ChassisSpeeds& speeds) {
                // Set module states
            }

            // Define other drive subsystem methods
        };
        ```


### Add Custom Commands to the Chooser

You can add custom commands to the chooser using the `addCustomCommand` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoSendableChooser.html#addCustomCommand(java.lang.String,edu.wpi.first.wpilibj2.command.Command))/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoSendableChooser.html#a62a0cad2acdb9f85a10e1f4f823b5950)) method.

=== "Java"

    ```java
    autoChooser.addCustomCommand("Custom Command", new MyCustomCommand());
    ```

=== "C++"

    ```c++
    autoChooser->addCustomCommand("Custom Command", std::make_shared<MyCustomCommand>());
    ```

## Get Selected Command

To get the command for the currently selected chooser item, use the `getSelectedCommand` ([Java](https://frc1511.github.io/ThunderLib/api/java/com/thunder/lib/auto/ThunderAutoSendableChooser.html#getSelectedCommand())/[C++](https://frc1511.github.io/ThunderLib/api/cpp/classthunder_1_1ThunderAutoSendableChooser.html#accbe8a7827c10c8874b93e7b027d3e1d)) method. If no item is selected, this method will return a __None__ command.

=== "Java"

    ```java
    Command selectedCommand = autoChooser.getSelectedCommand();
    ```

=== "C++"

    ```c++
    frc2::CommandPtr selectedCommand = autoChooser->getSelectedCommand();
    ```

Get this command during the robot's `autonomousInit` method and schedule it to run.