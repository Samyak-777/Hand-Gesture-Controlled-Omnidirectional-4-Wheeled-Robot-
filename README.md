# Hand Gesture Controlled Omnidirectional-4-Wheeled-Robot

This is the official repository for the omni directional hand gesture robot project at IvLabs, VNIT Nagpur.

# Description 
This project aims to develop an omnidirectional 4-wheeled robot controlled using hand gestures via a glove worn by the operator. The glove will feature buttons and sensors to enable remote control of the robot.

# Objectives
 Our Objective is to build and control robots using tiny computers, wireless communication, and 3D printing. Experiment with different ways to command robots, including hand gestures, and test designs in a virtual world before building them.

# Methodology 
## Software Implementation
### 1. Connection oF MPU6050 with ESP32 
It is a crucial step in creating an omni-directional hand gesture bot. The MPU6050 is an inertial measurement unit (IMU) that combines a 3-axis gyroscope and a 3-axis accelerometer, which can detect the orientation, movement, and acceleration of the hand. We then connect this sensor to a small computer called ESP32. 1  This computer understands the sensor's information and tells the robot to move in the same way as your hand. So, when you wave your hand, the robot waves its arm.

![Screenshot 2024-07-28 001241](https://github.com/user-attachments/assets/c462af01-8c69-4a36-a888-2618374db28e)

### 2. Simulation of MPU3050 
The result of the simulation of the MPU3050 is shown below.MPU6050 track each movement and send its value to ESP32.
![Screenshot 2024-07-28 002333](https://github.com/user-attachments/assets/fa09435e-beb3-4f6c-aed8-1f83a332407b)






