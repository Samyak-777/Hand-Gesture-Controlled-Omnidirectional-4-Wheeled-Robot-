># Hand Gesture Controlled OmniDirectional Robot 

This is the official repository for the Omni Directional Hand Gesture-Controlled Robot project at IvLabs, VNIT Nagpur.

## Contents

- [Objectives](#objectives)
- [Methodology](#methodology)
 - [Components Used](#components-used)
- [System Architecture](#system-architecture)
   - [Gesture Control Unit (Sender)](#1-gesture-control-unit-sender)
   - [Robot Chassis (Receiver)](#2-robot-chassis-receiver)
- [Software Implementation](#software-implementation)
   - [MPU6050 and ESP32 Connection](#1-connection-of-mpu6050-with-esp32)
   - [Simulation Result of MPU6050](#2-simulation-result-of-mpu6050)
   - [Robot Motion Demonstrations](#3-motion-of-omnidirectional-robot)
   - [Kinematics](#4-kinematics)
   - [PCB Design Using KiCad](#7-pcb-design-using-kicad)
- [Hardware Implementation](#hardware-implementation)
   - [IMU Simulation](#1-hardware-simulation-of-imu)
   - [Mecanum Wheels Integration](#2-fitting-mecanum-wheels)
   - [Motor Driver Integration](#3-motor-driver-integration)
   - [Speed Control with PWM](#4-speed-control-with-pwm-pins)
   - [Wireless Data Transfer](#5-wireless-data-transfer-using-wifi-esp-now-protocol)
- [Final Outcome](#final-outcome)
 

## Objectives
The objectives of the Summer Intership were to create a Omni Directional Robot which moves in all 8 direction, clockwise and anticlockwise using transmitter receiver with hand gestures.

## Methodology

## Components used :
*MPU6050 , Two EPS32 , Two Motor Driver L298N , Four DC Motor , One stepdown MOSFET , TWO- 9V battery , 24V lithium ion battery , One Switch , Four Mecanum Wheels.*
## System Architecture

The robot system consists of two main parts :

### 1. Gesture Control Unit (Sender) :
-  Contains the MPU6050 and one ESP32.
- Detects hand movements and transmits the corresponding control signals via ESP-NOW.
- **MPU6050**: It captures hand movements in terms of acceleration and angular velocity.
- **ESP32 (Sender)**: Processes the MPU6050 data and transmits it wirelessly to the receiving ESP32 module on the robot via ESP-NOW.
### 2. Robot Chassis (Receiver) :
- Contains the ESP32, L298N motor drivers, DC motors, and the power sources.
- Receives the control signals from the gesture control unit and moves the robot accordingly.
- **ESP32 (Receiver)**: Receives the transmitted data from the gesture control unit and converts it into motor control commands.
- **Motor Drivers (L298N)**: The received signals are used to control the speed and direction of the motors.
- **DC Motors and Mecanum Wheels**: The motors drive the Mecanum wheels to achieve omnidirectional movement based on the received control data.

## Software Implementation :

### 1. Connection of MPU6050 with ESP32
Connecting an MPU6050 to an ESP32 is a crucial step in creating an omni-directional hand gesture bot. The MPU6050 is an inertial measurement unit (IMU) that combines a 3-axis gyroscope and a 3-axis accelerometer, which can detect the orientation, movement, and acceleration of the hand.
![58259a94-7d6a-4abb-9f88-bdb8f0470ed3](https://github.com/user-attachments/assets/11e2e5cd-1c9e-49ca-9938-fa96b7e0eb20)


### 2. Simulation result of MPU6050
The integration of the MPU6050 with the ESP32 results in precise real-time tracking of hand gestures, enabling smooth and responsive control of the omni-directional bot. This enhances user interaction by translating natural hand movements into accurate bot movements.

![Screenshot (76)](https://hackmd.io/_uploads/SkzNjsSvC.png)

### 3. Motion of Omnidirectional robot

|                    1]   Forward Motion                     |                     2] Backward Motion                      |
|:----------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Forward (2)](https://github.com/user-attachments/assets/33ce022c-c7c0-48a4-b24f-bf72bedbe949) | ![Backward (1)](https://github.com/user-attachments/assets/8c13606c-27da-4976-ad22-a669e5629559) |


|                    3]   Leftward Motion                     |                     4] Rightward Motion                      |
|:----------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Leftward (1)](https://github.com/user-attachments/assets/9a93484b-398b-4a3d-bd4b-25e87bc53280) | ![Rightward (1)](https://github.com/user-attachments/assets/79f461e3-6150-4ca6-a64d-413a4b40eeed) |

|                    5]   Clockwise Motion                     |                     6] Anti-Clockwise Motion                      |
|:----------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Clockwise Rotation](https://github.com/user-attachments/assets/069a9576-2dce-40b2-96cc-a67faed60443) | ![Anti-Clockwise Rotation](https://github.com/user-attachments/assets/e848d204-8c8e-4b9e-8ba4-376dd46fe39d) |

|                    7]   Forward-Left Motion                     |                     8] Forward-Right Motion                      |
|:----------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Forward-Left (2)](https://github.com/user-attachments/assets/4b2a652f-1d47-4f1a-b2ec-712ed6c28ec1) | ![Forward-Right (3)](https://github.com/user-attachments/assets/228d17e8-4a55-4af1-926b-afb0da9f8b2f) |

|                    9]   Backward-Left Motion                     |                     10] Backward-Right Motion                      |
|:----------------------------------------------------------:|:-----------------------------------------------------------:|
| ![Backward-Left (3)](https://github.com/user-attachments/assets/a6666f3d-6864-4166-a0ec-178aaaf5138f) | ![Backward-Right (2)](https://github.com/user-attachments/assets/db77f664-ebb9-4526-a628-50debf7923d1) | 

### 4. Kinematics

#### 1] Variables :
- **\( Vx \)**: Forward velocity (m/s)
- **\( Vy \)**: Lateral velocity (m/s)
- **\( ω \)**: Angular velocity (rad/s)

#### 2] Wheel Velocity Equations :
For a robot with four omnidirectional wheels, the velocity of each wheel can be expressed as:

-  ### **`Vi = Vx.r.cos(θi)+Vy​⋅r⋅sin(θi​)+L​⋅ω/2`**
where \( i = 1, 2, 3, 4 \).

#### 3] Parameters :
- **\( Vi \)**: Velocity of wheel \( i \)
- **\( r \)**: Radius of the wheel
- **\( L \)**: Distance from the center of the robot to the wheel
- **\( θi \)**: Angle of the wheel with respect to the robot
    
![{B64F84E5-FEB2-4465-80E1-0769934445B6}](https://github.com/user-attachments/assets/07466d6c-a2cf-45f5-8140-48553d7e46dd)



### 5. Error Minimization
During the development, one challenge was minimizing errors in the gesture control. To overcome this challenge we used :


- **`Calibration`** : Calibrated the MPU6050 sensor to reduce drift and improve accuracy in detecting gestures.

### 6. Power Management
The system requires proper power management to ensure smooth operation. We have used :

- **24V Lithium-ion Battery** : Which Powers the motors for the robot’s movement.
- **9V Batteries** :They Power the ESP32 modules and the MPU6050 sensor.
- **Step-Down MOSFET** : Was used to ensure voltage regulation for motor drivers.

### 7. PCB design using KiCad
    
#### 1] Gesture-Glove (Transmitter) Circuit :
The circuit in the gesture-glove is responsible for capturing hand movements and transmitting the corresponding data wirelessly to the robot.
- The PCB ensures a compact layout to fit inside the glove.
- Integrated connections for MPU6050 via I2C interface.
- Voltage Regulator for stable power supply.
- ESP32 for wireless communication.

#### Circuit of Hand-Gesture IMU :
![Screenshot (131)](https://hackmd.io/_uploads/ryevkZnJke.png)

### 2] Robot (Receiver) Circuit :
The robot's circuit interprets the transmitted gestures and controls the Mecanum wheels for omnidirectional movement. 
- Each motor driver channel is connected to an individual motor, enabling precise control for omnidirectional movement.
- Power Input for motor drivers and ESP32.
- Motor Outputs for Mecanum wheels.

#### Circuit of Omni-Directional Robot:
![Screenshot (132)](https://hackmd.io/_uploads/B1jEy-n1Je.png)
 
## Hardware Implementation 

### 1. Hardware Simulation of IMU
- **Purpose** : To test the accuracy and responsiveness of the MPU6050 IMU sensor before integrating it into the gesture-glove.
![{230553F7-A3DF-415F-88FD-99939C7C419F}](https://github.com/user-attachments/assets/39b960eb-910a-488e-956f-3a6e65370d87)

### 2. Fitting Mecanum Wheels
- **Purpose** : To enable omnidirectional movement of the robot.
### 3. Motor Driver Integration
- **Purpose** : To control the speed and direction of the Mecanum wheels.
    
![{AFA077DD-452F-4927-AD80-8D3DFB2C7AF3}](https://github.com/user-attachments/assets/c349ac55-cb0a-4cfd-aab0-07ea94a8a8b0)


### 4. Speed Control with PWM Pins
- **Purpose** : To control the speed of the motors driving the Mecanum wheels, we employed Pulse Width Modulation (PWM). This technique allows us to simulate varying levels of voltage by rapidly switching a digital signal between high (on) and low (off) states.
- **How PWM Pins Works** :
  - ***Duty Cycle*** : The ratio of time the signal is high to the total cycle time determines the effective voltage seen by the motor. A higher duty cycle results in higher average voltage and thus greater speed.
  -  The PWM signals are sent to the L298N motor driver through its enable pins (ENA and ENB). By adjusting these signals, we can finely control the speed of each motor based on user gestures.

### 5. Wireless Data Transfer using WiFi (ESP-NOW Protocol)

- **Challenges** :
  - First we tried using bluetooth , reciever was not able to connect to transmitter.
  - Then we tried with only Wifi , there was problem of connection loss.
  - At last we used ESP-NOW Protocol for Wireless Data Transfer.
![{CE0C36F2-A4CF-4322-A9DC-C9EE25361060}](https://github.com/user-attachments/assets/ea606d09-f10b-4c7a-b370-b75266253330)



## Final Outcome

   ### 1] Forward Motion and Gesture

| - ![clideo_editor_8e83dd40fa0f4ebcab7235a1aa08f386-ezgif com-crop](https://github.com/user-attachments/assets/dcdc0ea1-091e-4163-9c62-aa2dcb4eb3a1)| - ![clideo_editor_3f7a37148ee74914ac6dc855c9c3842a (1) (2)-min](https://github.com/user-attachments/assets/f767f146-4518-491c-8637-bf89e7b2cf24) |
| --- | --- |
  ### 2] Backward Motion and Gesture 
| - ![Pi7_GIF_CMP (6)](https://github.com/user-attachments/assets/3302445e-6e1c-4946-a1be-cfaa9ff64c22) | - ![clideo_editor_7c57bf5448664c95bda64f7a741899bf-ezgif com-crop](https://github.com/user-attachments/assets/0b269719-b6eb-49b5-8226-d9cd31fa591b) |
| --- | --- |
### 3] Leftward motion and Gesture
| - ![clideo_editor_26a2e212c2b54b35ba1fd6984c673099-ezgif com-crop](https://github.com/user-attachments/assets/9f0bf2b0-c71c-4492-8834-f873d30dc9a1) | -![clideo_editor_07811adebee047a9bbbf781a2be16687-ezgif com-crop](https://github.com/user-attachments/assets/a7ac58ce-808c-49cc-92ae-c585140ed44c)  |
| --- | --- |
  ### 4] Rightward motion and Gesture
| - ![Pi7_GIF_CMP (1)](https://github.com/user-attachments/assets/d847da56-3a11-4ea1-9f69-cfe9b9330ad8)  | - ![clideo_editor_9175009f7c7d473eb05568c76f44c064-ezgif com-crop](https://github.com/user-attachments/assets/d90dbae0-d864-4afb-8119-6b556d022297) |
| --- | --- |
### 5] Backward-Right motion and Gesture
| - ![clideo_editor_5a3ad0e03f3043ff84b6a699fbdf23be-ezgif com-crop (1)](https://github.com/user-attachments/assets/3ddd52a4-9386-4a57-8c89-63e5316c41ef)  | - ![clideo_editor_fe2618fd643147c095c18a07dda61f7b-ezgif com-crop](https://github.com/user-attachments/assets/ecb7fcde-61c7-4b7a-b27e-376f7ab2940d) |
| --- | --- |
### 6] Forward-Right motion and Gesture
| - ![Pi7_GIF_CMP (5)](https://github.com/user-attachments/assets/03b2455d-8432-4125-9302-a43f035bb791) | - ![clideo_editor_633a92f379c24180a07db826e5f1bcea-ezgif com-crop](https://github.com/user-attachments/assets/07988dca-1a86-4be4-918d-59d345a43e7f) |
|--- | --- |
### 7] Backward-Left motion and Gesture
|  - ![Pi7_GIF_CMP3-ezgif com-crop](https://github.com/user-attachments/assets/fd5938be-6e89-44e3-9db3-b31bf982b3db)| - ![clideo_editor_d8819fd0e9b94bb38e92f6850f763152-ezgif com-crop](https://github.com/user-attachments/assets/b8f04796-6901-49a1-b309-46a3690daf05) |
|--- | --- |
### 8] Forward-Left motion and Gesture
| - ![Pi7_GIF_CMP (4)](https://github.com/user-attachments/assets/f78dbb50-cbcb-4ab6-a69b-db0a697b35e8) |- ![clideo_editor_ad40d1f323354baa8fd13192614ff335-ezgif com-crop](https://github.com/user-attachments/assets/94aed21a-bada-49b5-ad97-4e399190ba6b) |
| --- | --- |
### 9] Clockwise motion and Gesture
| - ![clideo_editor_39199e4fdac24a4f8f52c2f8cf530ea6-ezgif com-crop](https://github.com/user-attachments/assets/26a6d1e9-65b4-4bae-80cb-5803528361d8) | -![clideo_editor_5a0b61c32c484bbca4e911fb65e3c2f5-ezgif com-crop](https://github.com/user-attachments/assets/644d8df3-3674-4715-97c2-557ab87ad65b) |
| --- | --- |
### 10] Anti-Clockwise motion and Gesture
| - ![clideo_editor_e59d6d1f68f544a0a9bbf8be52ae7675-ezgif com-optimize](https://github.com/user-attachments/assets/62fdf41f-d721-4abd-a9ba-c68ce942ec09)| - ![clideo_editor_d649c38f290442c6bbf4d307a6760cc3-ezgif com-crop (1)](https://github.com/user-attachments/assets/e0ef3237-a08a-4db3-98f9-bfc384c440aa)  |
| --- | --- |

---





