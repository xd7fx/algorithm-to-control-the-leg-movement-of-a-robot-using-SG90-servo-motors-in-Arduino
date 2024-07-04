# Robot Leg Movement Control

This project demonstrates how to control the leg movement of a robot using SG90 servo motors with an Arduino microcontroller. The provided code implements a basic walking cycle by coordinating the movement of hip and knee servos.

## Components

- Arduino microcontroller
- SG90 servo motors (4 per leg, total 8)
- Jumper wires
- Power supply for the servos
- Breadboard (optional, for wiring convenience)

## Installation

1. **Connect the Servos to the Arduino:**
   - Attach the SG90 servo motors to the appropriate pins on the Arduino. For this example, we use pins 9, 10, 11, and 12 for the servos controlling one leg, and pins 5, 6, 7, and 8 for the servos controlling the other leg.

2. **Set Up the Arduino Environment:**
   - Download and install the Arduino IDE from [Arduino's official website](https://www.arduino.cc/en/software).
   - Install the Servo library if it is not already installed. You can install it from the Arduino Library Manager.

3. **Upload the Code:**
   - Open the provided Arduino code (`robot_leg_movement.ino`) in the Arduino IDE.
   - Select the correct board and port from the Tools menu.
   - Upload the code to your Arduino.

## Code Overview

The Arduino code controls the movement of the robot's legs by rotating the hip and knee servos to predefined angles. The movement cycle consists of lifting the leg, swinging it forward, lowering it, and shifting the weight.

### Main Functions

- `setup()`: Initializes the servo motors and sets their initial positions to 90 degrees.
- `loop()`: Contains the main walking cycle, which includes lifting, swinging forward, lowering the leg, and shifting the weight.

### Helper Functions

- `incrementallyRotate(Servo servo, int fromAngle, int toAngle)`: Gradually rotates the servo from one angle to another.
- `decrementAngle(Servo servo, int fromAngle, int toAngle)`: Decreases the servo angle gradually.
- `incrementAngle(Servo servo, int fromAngle, int toAngle)`: Increases the servo angle gradually.
- `maintainAngle(Servo servo, int angle)`: Keeps the servo at a specified angle.

## Parameters

- `stepLength`: The length of each step in degrees (default: 30).
- `footLiftHeight`: The height of the foot lift in degrees (default: 60).
- `movementSpeed`: The speed of movement in milliseconds (default: 50).

## Usage

1. **Power the Arduino and Servos:**
   - Connect the Arduino to your computer or an appropriate power source.
   - Ensure that the servos have a sufficient power supply.

2. **Monitor the Movement:**
   - Once the code is uploaded and the Arduino is powered, the robot will start executing the walking cycle.
   - Observe the movement of the legs and make any necessary adjustments to the parameters or servo connections.

## Adjustments and Fine-Tuning

- Modify the `stepLength`, `footLiftHeight`, and `movementSpeed` parameters in the code to achieve the desired walking motion.
- Adjust the servo connections if the movement is not as expected.

## Troubleshooting

- Ensure all servo connections are secure and correct.
- Check that the power supply is adequate for the number of servos used.
- Verify that the servo library is properly installed in the Arduino IDE.


## 
