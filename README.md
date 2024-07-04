# Robot Leg Movement Control using SG90 Servo Motors

This document explains the algorithm used to control the movement of a two-legged robot using 8 SG90 servo motors. The robot has 4 joints in each leg, with each joint controlled by a single servo motor, and additional servos for rotating the feet left and right.

## Contents

1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Movement Control Functions](#movement-control-functions)
4. [Main Loop](#main-loop)
5. [3D Design](#3d-design)
6. [Technical Details](#technical-details)
   
## Introduction

The goal of this project is to program a two-legged robot to perform forward and backward walking, as well as left and right turning movements using SG90 servo motors. The algorithm includes all the technical details related to joint movements and foot rotations to achieve balanced and smooth motion.

## Setup

In this phase, the servo motors are initialized and connected to the appropriate pins on the microcontroller. Each leg has 4 joints, each controlled by a single servo motor.

## Movement Control Functions

1. **`moveJoint`**: Move a specific joint in a specific leg to a given angle.
2. **`moveFoot`**: Rotate the foot in a specific leg to a given angle.
3. **`moveLeg`**: Move all joints in a leg to specific angles.
4. **`walkForward`**: Execute forward walking steps by lifting and moving the leg forward, then balancing the other leg.
5. **`walkBackward`**: Execute backward walking steps in a similar manner.
6. **`turnLeft`**: Rotate both feet to achieve a left turn.
7. **`turnRight`**: Rotate both feet to achieve a right turn.

## Main Loop

The main loop continuously checks for user input or sensor data to determine the required movement (forward, backward, left, right) and calls the appropriate function to execute it.

## 3D Design
The 3D design of the robot can be found at the following link: [3D Design File](https://github.com/xd7fx/3D.design.robot.leg)

## Technical Details

```pseudo
Initialize the servo motors
Define servo pins for each joint (4 joints per leg, 8 servos total)
Set initial positions for each servo motor

Function setup():
    Attach each servo to its corresponding pin
    Set each servo to its initial position

Function moveJoint(legNumber, jointNumber, angle):
    Check if legNumber is valid (1 to 2)
    Check if jointNumber is valid (1 to 4)
    Set the specified servo to the desired angle (0 to 180)

Function moveFoot(legNumber, angle):
    Check if legNumber is valid (1 to 2)
    Set the foot rotation servos to the desired angle (0 to 180)

Function moveLeg(legNumber, angles):
    Move joint 1 of legNumber to angles[0]
    Move joint 2 of legNumber to angles[1]
    Move joint 3 of legNumber to angles[2]
    Move joint 4 of legNumber to angles[3]
    Pause for a short duration

Function walkForward():
    // Step 1: Lift right leg and move forward
    moveLeg(1, [60, 100, 120, 90]) 
    // Adjust left leg for balance
    moveLeg(2, [90, 90, 90, 90])
    Pause for a short duration

    // Step 2: Lower right leg
    moveLeg(1, [90, 90, 90, 90])
    Pause for a short duration

    // Step 3: Lift left leg and move forward
    moveLeg(2, [60, 100, 120, 90])
    // Adjust right leg for balance
    moveLeg(1, [90, 90, 90, 90])
    Pause for a short duration

    // Step 4: Lower left leg
    moveLeg(2, [90, 90, 90, 90])
    Pause for a short duration

Function walkBackward():
    // Step 1: Lift right leg and move backward
    moveLeg(1, [120, 80, 60, 90]) 
    // Adjust left leg for balance
    moveLeg(2, [90, 90, 90, 90])
    Pause for a short duration

    // Step 2: Lower right leg
    moveLeg(1, [90, 90, 90, 90])
    Pause for a short duration

    // Step 3: Lift left leg and move backward
    moveLeg(2, [120, 80, 60, 90])
    // Adjust right leg for balance
    moveLeg(1, [90, 90, 90, 90])
    Pause for a short duration

    // Step 4: Lower left leg
    moveLeg(2, [90, 90, 90, 90])
    Pause for a short duration

Function turnLeft():
    // Rotate foot of leg 1 left
    moveFoot(1, 45)
    // Rotate foot of leg 2 right
    moveFoot(2, 135)
    Pause for a short duration
    Return feet to initial position

Function turnRight():
    // Rotate foot of leg 1 right
    moveFoot(1, 135)
    // Rotate foot of leg 2 left
    moveFoot(2, 45)
    Pause for a short duration
    Return feet to initial position

Function loop():
    Check for user input or sensor data
    If forward command received:
        Call walkForward()
    If backward command received:
        Call walkBackward()
    If left turn command received:
        Call turnLeft()
    If right turn command received:
        Call turnRight()

Start program:
    Call setup()
    Continuously call loop()
