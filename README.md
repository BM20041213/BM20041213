#include <Servo.h>

// IR sensor pin
const int IR_sensorPin = 2;

// Servo motor pin
const int servoPin = 9;

Servo myServo;

void setup() {
  // Initialize the serial communication for debugging
  Serial.begin(9600);
  
  // Attach servo to the servo pin
  myServo.attach(servoPin);

  // Initialize IR sensor pin as INPUT
  pinMode(IR_sensorPin, INPUT);
}

void loop() {
  // Read the IR sensor value
  int sensorValue = digitalRead(IR_sensorPin);

  if (sensorValue == HIGH) {
    // Object detected, rotate servo motor by 180 degrees
    rotateServo();
    delay(1000); // Wait for a second before resetting the servo position
    resetServo();
  }
}

void rotateServo() {
  // Rotate the servo motor to 180 degrees
  myServo.write(180);
  Serial.println("Object detected! Servo rotated to 180 degrees.");
}

void resetServo() {
  // Reset the servo motor back to 0 degrees
  myServo.write(0);
  Serial.println("Servo reset to 0 degrees.");
}
