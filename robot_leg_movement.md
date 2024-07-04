## Initialization
1. **Initialize the Servos:**
   - Connect the servos to the microcontroller.
   - Set the initial positions of the servos to 90 degrees.

2. **Define Parameters:**'
   

-`stepLength` is the length of each step (in degrees).

-`footLiftHeight` is the height of the foot lift (in degrees).

-`movementSpeed` is the speed of movement (in milliseconds).

## Code Python

### `robot_leg_movement.ino`

```cpp
#include <Servo.h>

Servo hipServo1, hipServo2, kneeServo1, kneeServo2;

int stepLength = 30;      // Step length in degrees
int footLiftHeight = 60;  // Foot lift height in degrees
int movementSpeed = 50;   // Movement speed in milliseconds

void setup() {
  // Attach the servos
  hipServo1.attach(9);   // Attach hip servo 1 to pin 9
  hipServo2.attach(10);  // Attach hip servo 2 to pin 10
  kneeServo1.attach(11); // Attach knee servo 1 to pin 11
  kneeServo2.attach(12); // Attach knee servo 2 to pin 12

  // Set initial positions to 90 degrees
  setInitialPositions();
}

void setInitialPositions() {
  hipServo1.write(90);
  hipServo2.write(90);
  kneeServo1.write(90);
  kneeServo2.write(90);
  delay(1000);  // Delay for 1 second to stabilize the initial positions
}

void loop() {
  // Lift the leg
  incrementallyRotate(hipServo1, 90, 120);
  decrementAngle(kneeServo1, 90, 60);
  delay(movementSpeed);

  // Swing the leg forward
  incrementallyRotate(hipServo1, 120, 90);
  incrementAngle(kneeServo1, 60, 90);
  delay(movementSpeed);

  // Lower the leg
  incrementAngle(kneeServo1, 90, 120);
  maintainAngle(hipServo1, 90);

  // Shift weight
  incrementallyRotate(hipServo1, 90, 80);
  
  // Repeat for the opposite leg
  incrementallyRotate(hipServo2, 90, 120);
  decrementAngle(kneeServo2, 90, 60);
  delay(movementSpeed);

  incrementallyRotate(hipServo2, 120, 90);
  incrementAngle(kneeServo2, 60, 90);
  delay(movementSpeed);

  incrementAngle(kneeServo2, 90, 120);
  maintainAngle(hipServo2, 90);

  incrementallyRotate(hipServo2, 90, 80);
}

void incrementallyRotate(Servo servo, int fromAngle, int toAngle) {
  if (fromAngle < toAngle) {
    for (int angle = fromAngle; angle <= toAngle; angle++) {
      servo.write(angle);
      delay(movementSpeed);
    }
  } else {
    for (int angle = fromAngle; angle >= toAngle; angle--) {
      servo.write(angle);
      delay(movementSpeed);
    }
  }
}

void decrementAngle(Servo servo, int fromAngle, int toAngle) {
  for (int angle = fromAngle; angle >= toAngle; angle--) {
    servo.write(angle);
    delay(movementSpeed);
  }
}

void incrementAngle(Servo servo, int fromAngle, int toAngle) {
  for (int angle = fromAngle; angle <= toAngle; angle++) {
    servo.write(angle);
    delay(movementSpeed);
  }
}
void maintainAngle(Servo servo, int angle) {
  servo.write(angle);
}

```

#Explanation:
1. **Initialization:**
   - The servos are attached to the appropriate pins on the microcontroller.
   - Initial positions of the servos are set to 90 degrees for stability.
     
2. **Main Loop::**
   - The leg is lifted by rotating the hip servo from 90 to 120 degrees and decreasing the knee servo angle from 90 to 60 degrees.
   - The leg is swung forward by rotating the hip servo back to 90 degrees and increasing the knee servo angle back to 90 degrees.
   - The leg is lowered by increasing the knee servo angle to 120 degrees while maintaining the hip servo at 90 degrees.
   - The weight is shifted by rotating the hip servo to 80 degrees.
   - The same sequence of actions is repeated for the opposite leg.

3. **Helper Functions::**
   - `incrementallyRotate`: Gradually rotates the servo between two specified angles.
   - `decrementAngle`: Decreases the servo angle gradually between two specified angles.
   - `incrementAngle`: Increases the servo angle gradually between two specified angles.
   - `maintainAngle`: Keeps the servo at a specified angle.

By following this approach, you can control the leg movement of your robot using SG90 servo motors effectively. Adjust the parameters and angles as needed to achieve smooth and balanced movements for your robot.

