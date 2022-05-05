# Status
Work-in-progress

# Bief
Adaptive object detection, and obstacle avoidance robot using a Jetson Nano 2GB, OpenCV, Lidar, OpenCR and ROS.
A [ROBOTIS TurtleBot3 waffle](https://emanual.robotis.com/docs/en/platform/turtlebot3/features/#specifications) is used as a hardware platform starting point. A Jetson Nano 2GB will be used instead of the included Raspberry Pi 3B+ to enable potential of GPGPU use in upcoming iterations of the robot.

# Components
## Hardware:
1. JetsonNano 2GB
2. ROBOTIS TurtleBot3 waffle kit, including:
    1. LDS-001 Lidar sensor + USB2LDS interface board
    2. OpenCR v1.0
    3. 2x servo motors
    4. RPi camera v2.1 + CSI ribbon cable
    5. Battery Pack/power supply.

## Software:
1. [JetPack v4.6.1](https://developer.nvidia.com/jetpack-sdk-461), which includes:
    1. [OpenCV v4.1.1](https://opencv.org/opencv-4-1-1/)
2. [ROS Melodic Morenia](http://wiki.ros.org/melodic)
<!-- 3. []()
4. []()
5. []()
6. []()
7. []() -->

# Demo
- Robot, up and running with a Jetson Nano.
![robot](https://user-images.githubusercontent.com/72912013/166982449-94f8bd30-a76f-4b47-b273-4e46f4b256a9.jpg)

- Robot's POV of the scene ahead via camera stream as-is, and with yaw adjustment based on centeroid calculations.
![image](https://user-images.githubusercontent.com/72912013/166972908-56effa3d-bc24-4c42-9891-4a79feef7271.png)

- Experimenting with different color spaces using basic color masking and a [bitwise_and](https://docs.opencv.org/4.1.1/d2/de8/group__core__array.html#ga60b4d04b251ba5eb1392c34425497e14) operator on each pixel to isolate the object of interest.
    - Absolute red mask (RGB mask  = (255, 0, 0)) with a threshold tolareance of +/- 40 intesity levels in each channel.
    ![image](https://user-images.githubusercontent.com/72912013/166975095-b67face5-053e-4c1d-bfda-fb54bae0a17c.png)

    - Absolute green mask (RGB mask = (0, 255, 0)) with a threshold tolareance of +/- 40 intesity levels in each channel.
    ![image](https://user-images.githubusercontent.com/72912013/166975150-7d994eb4-e454-4f96-a10d-9ae71943096d.png)

    - Absolute yellow mask (RGB mask = (255, 255, 0)) with a threshold tolareance of +/- 40 intesity levels in each channel.
    ![image](https://user-images.githubusercontent.com/72912013/166975041-757b5af2-4d16-49b8-9f57-9f8258fdeaaa.png)

- x

# Design
## Software block diagram
![image](https://user-images.githubusercontent.com/72912013/166981489-cb52c727-c3d3-42e1-ad7e-e69b4c675cf3.png)

## Software statemachine flow diagram
![image](https://user-images.githubusercontent.com/72912013/166981323-42147c25-6f91-49ee-8d8f-0197dc36eb69.png)

# Future work
## Imageg processing
1. Implment an ambient light sensor (e.g., [TCS34725](https://www.adafruit.com/product/1334) to enable dynamic threshold adjustment (consider `V` channel in HSV color space).
2. Implment active learning model (consider TensorRT+CUDA), and compare accuracy and performance to other iterations of this project.

## Motion Control
1. Design and implment a state-space PID controller model to effeciently navigate with yaw adjustment in mind concurrently. 
