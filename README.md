
# 2 DOF Gimbal using Servos

This project showcases a compact two-degree-of-freedom gimbal system with independent control over each axis, built using servo motors. The primary purpose of this gimbal system is to provide a stable platform for various applications, such as camera stabilization and object tracking. For this project, we used Arduino Uno, an IMU called MPU6050, PD controller and python which enable us to interpret commands and send signals, read real-time orientation and movement, fine tune servo motor's positions and facilitate user interaction for high-level control.
## Contents
- Features
- Getting started
    - *Prerequisites*
    - *Installation*
- Workflow
- Understanding Control Theory and PID controller
- Cruise Control Task
- Servo Simulation Task
- Plotting angles based on input from MPU6050
- Implementing PD control with servo motors
- Designing the 2-DoF Gimbal
- 
## Features

- ***2 degrees-of-freedom***: This gimbal system offers movement along 2 axes providing stability against both pitch and yaw.
- ***Versatile Applications***: Provides stability against unintended rotations caused due to external factors and has variety of use cases.
- ***Open Source***: The project is open source, encouraging collaboration and improvements from the community.


## Getting Started
### Prerequisites
- A microcontroller (*Preferably Arduino uno*)
- MPU6050 (*A 6-Axis IMU*)
- Servo Motors x2 (*For 2 DoF*)
- Jumper wires
- Breadboard
- Access to fasteners and Tools
- Access to 3-D printer 
### Installation
#### For Arduino IDE
Arduino IDE Version 1.8.19 download guide [here](https://youtu.be/Steg-prCR4w?si=ljDTVF_hDhRWvyfr).

*This version is recommended to avoid facing compatability issues if you are using any other microcontroller*.

##### Download and install the following libraries in your IDE:
    - Adafruit_MPU6050
    - Adafruit_Unified_Sensor
    - Adafruit_BusIO
    - Adafruit_GFX_Library
    - Adafruit_SSD1306
*Some of these libraries are automatically installled when installing above libraries in order but do make sure you have all these installed.*
#### For Python (3.11.5)
- For Windows 11, download guide is [here](https://youtu.be/y7yo30d0n98?si=innD8FkUmFC5zx4i).
- For Windows 10, download guide is [here](https://youtu.be/dAZb_6s_JIE?si=ELFfmbRVrL7WighO).
###### Make sure to have 'numpy', 'serial' and 'matplotlib' libraries installed. For new installations, paste the below code snippet command in the terminal of IDLE or Windows command prompt.

    pip install numpy
    pip install matplotlib
    pip install pyserial

## Workflow
- Understanding PID control system in classical control theory.
- Completing tasks while applying concepts of PID controller to achieve desirable outcomes, which also include simulating ideal hardware scenarios.
- Reading angles from MPU using Arduino IDE and implementing PID controller by setting up a serial communication with arduino using python to plot that angle with help of matplotlib.
- Using hardware and performing the above task such that the servo motors rotate to stabilize the angle read from mpu and using PID control for smooth movement.
- Designing 2 DoF Gimbal using CAD software and 3-D printers.
- Adding a camera to the platform along with MPU6050 IMU to stabilise the footage recorded along 2 axes.

### 1. Understanding Control Theory and PID controller
- Learn basics of classical control theory from youtube lectures to gain a better understanding of PID controllers and their practical use case in real world scenarios.
- Links to playlists of these lectures are attached below:
    - [Classical Control Theory](https://youtube.com/playlist?list=PLUMWjy5jgHK1NC52DXXrriwihVrYZKqjk&si=NnChcHvDlMk0XuMP). (*Watching first 16 videos is recommended*)
    - [Understanding PID Control](https://youtube.com/playlist?list=PLn8PRpmsu08pQBgjxYFXSsODEF3Jqmm-y&si=GtxQewBUW3iwGR39). (*To gain knowlegede about PID, it's parameters and filters*)
### 2. Cruise Control Task
**Aim:** Use Python to develop a Cruise Control for a car for a fixed set-point velocity.

The Problem statement can be viewed [here](https://drive.google.com/file/d/13-e7mE6L7H6tf8J_iWNPkJWwlDUzuDqa/view?usp=drive_link).

Try to complete all the tasks mentioned in the above pdf. After plotting a graph using matplotlib, Your plot should look similar to the image below.

**Result:** This task gives an idea about how PID parameters influence the rise-time, overshoot, stability, steady state error and settling time of our plot.
### 3. Servo Simulation Task

**Aim:** To simulate an mpu6050 and map the change in angles onto two servos using PID.
You can use [Wokwi](https://wokwi.com/) for simulation.

Here, we aim to simulate an ideal hardware environment, use the IMU to detect the change in angle and map those changes onto 2 servos. (We dont have to use PID here as we will have smooth rotation from software simulation itself. Recommened to use PID on hardware).

***Example:** If MPU6050 detects an angular velocity of 'x' rad/s, we make the servo rotate by that angle. (Convert rad into deg before mapping).*

For better understanding the task, you can view [My Project](https://wokwi.com/projects/371588311755111425) for reference.
### 4. Plotting angles based on input from MPU6050.

**Aim:** To plot angles with polar plot using python matplotlib library based on input form our IMU.

Following components/installations are required:

    Microcontroller (Preferably Arduino Uno)
    MPU6050
    Breadboard
    Jumper Wires
    Python 3
    Arduino IDE

Watch some youtube tutorials on how to set up a serial communication between arduino and python [here](https://www.youtube.com/watch?v=z14l33paZGU).

To achieve this task, it's recommended to learn the basics of ***matplotlib*** and how you can use it to plot graphs. We will be using polar plot for this part. (*You can also do this using a normal plot and changing the orientation of the line using simple trigonometry*).

The jumper wire connections are the same as that of last task. This is the process followed to achieve this task:
1. Read  the angle values and print them on the serial monitor of arduino IDE.
2. Set up serial communication between arduino and python, and import data from arduino to get angles from MPU6050.
3. Refer to code for reference.
### 5. Implementing PD control with servo motors 

**Aim:** To use servo motors and rotate them smoothly using PD control to counter the rotation based on input angles from IMU.

Following components are required to complete this task:

    Microcontroller (Preferably Arduino Uno)
    MPU6050
    Breadboard
    Jumper Wires
    Servo Motors (x2)
Servo motors can only take input between **'0'** to **'180'** (Range for most servos). Here, our main aim is to calibrate and map the angles from the MPU so that the highest reading from the serial monitor is mapped to 180 and lowest is mapped to 0. This ensures that the servo angle doesnt go above or below **'180'** or **'0'** respectively (Refer to IDE code for more information). Once calibration and mapping is completed, set the proportional and derivative gain terms through trial and error.

**Note:** *Our IMU lacks a magnetometer due to which, it will pick up drift error as it changes it's angle and orientation. Using the **'I'** gain term would combine with this drift and  over time, in many cases will result in enormous fluctuating changes in the data obtained in serial monitor. Hence, it isn't optimal to use the integral gain as our system already had a built-in error that does the same thing (sort of).*
### 6. Designing the 2-DoF Gimbal

**Aim:** To make a 3-D model of the gimbal with 2-DoF.

We will be using a 3-D printer to achieve this task. Firstly, we create a 3-D model of our gimbal in a CAD software (We used Fusion 360 from autodesk but other CAD-M softwares can also be used like Siemen's NX, SOLIDWORKS, etc). Make sure to make the model as realistic as possible and also the dimensions should be accurate. The model should include 2 axis of rotation and a platform where the camera would be mounted, which would be taken as reference and be stabilised. Refer to the CAD model for more clarity.
### 7. Adding a camera onto the platform

**Aim:** To add a camera along with MPU6050 onto the platform to stabilize the footage recorded in real time.

We can either use a phone to record the footage or use any other camera depending on the model design. It is necessary to keep the MPU6050 in the same orientation as the camera and as close as possible to it to prevent error and get optimal results.

**Note:** *As this design only stabilizes the camera along 2 axes, it is recommended to only rotate the gimbal along those 2 axes to check its performance / efficiency. Nevertheless, due to minor rotations along the other axis, the gimbal will eventually accumulate error and tilt in one direction more, swaying away from initial position.*