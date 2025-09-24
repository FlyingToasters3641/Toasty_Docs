# Intro
We use several different classes to run our subsystems. These are all initialized in `RobotContainer.java`, which also handles loops and the controller input.
`RobotContainer.java`'s methods are initialized in `Robot.java`, though we usually don't change too much there.
# Subsystems
the normal subsystem contains 6 classes; Main, IO, IO TalonFX, IO Simulation (Sim), Constants, and Commands.

- Main is the function used to initialize and access all methods of the subsystem.
- IO is a base of the required methods, and a base of which main can access.
- Both IO TalonFX and IO Sim are what have the actual calculations for moving the robot, or indicating movement. They both implement the IO class.
- Constants contain any variables that could be changed to adjust the subsystem. By having them in a separate class they are much more centralized and easier to change.
- Commands has the methods for setting a setpoint and such, which is used by the controllers in `RobotContainer.java` and by the `ScoreCommands.java` class.
# Other Major Classes
`Constants.java` contains variables that are used across the code. Things such as scoring positions for auto-align, or PID variables not in subsystem Constants class.
We also use separate classes for auto-align and multiple commands run in sequence. These are `AutoAlign.java` and `ScoreCommands.java`. 
