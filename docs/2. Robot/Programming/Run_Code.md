# Intro
To be able to test code, it has to either be simulated or sent to the robot. Here is a simple tutorial of how to test code on the robot and some tips and tricks to help debug problems.
# Programming the Radio

# Connecting to the Robot
Once the robot has been started a wifi will appear with the robot's name. When connected it is possible to deploy code using *f1* in VS Code and running `WPILib Deploy Code`. 
It will first build the code, and then attempt to send it. If everything is successful and no errors appear a RioLog window should pop up in VS Code. At this point it is possible to open [**INSERT DIFFERENT APPS**] and control the robot.
# Useful Features
- Using Pheonix Tuner it is possible to easily test PID variables instead of having to constantly slightly adjust and then redeploy code repeatedly. Open up the correct motor, change values, click flash, and test. Don't forget to write adjusted values into the code, otherwise they are gone.
