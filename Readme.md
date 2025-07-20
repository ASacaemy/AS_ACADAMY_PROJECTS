🔧 Obstacle-Aware Servo Motor using PIR Sensor (Arduino Project)
This project demonstrates how to use a PIR (Passive Infrared) motion sensor to control a servo motor using an Arduino Uno. When motion is detected, the servo motor rotates to a specific angle (90°), simulating an automatic response such as a door opening, camera movement, or light activation.

📷 Project Overview

🎯 Purpose
The goal of this project is to detect human motion using a PIR sensor and actuate a servo motor accordingly. This setup can be applied in automated systems like security cameras, automatic doors, and home automation.

🛠️ Components Required
Component	Quantity
Arduino Uno	1
PIR Motion Sensor	1
Servo Motor	1
Jumper Wires	As needed
Breadboard	1 (optional)

🔌 Circuit Connections
Component	Arduino Pin
PIR Sensor VCC	5V
PIR Sensor GND	GND
PIR Sensor OUT	D2
Servo Motor VCC	5V
Servo Motor GND	GND
Servo Motor SIG	D9

💻 Arduino Code
c
#include <Servo.h>

Servo myServo;
int pirPin = 2;         // PIR sensor output pin
int servoPin = 9;       // Servo motor control pin
int pirValue = 0;       // Variable to store PIR status

void setup() {
  pinMode(pirPin, INPUT);
  myServo.attach(servoPin);
  myServo.write(0);     // Initial position
  Serial.begin(9600);
}

void loop() {
  pirValue = digitalRead(pirPin);

  if (pirValue == HIGH) {
    Serial.println("Motion Detected: ");
    myServo.write(90);  // Rotate to 90°
    delay(500);         // Wait for 0.5 sec
  } else {
    Serial.println("No Motion");
    myServo.write(0);   // Return to 0°
  }

  delay(50);            // Short delay to avoid flickering
}
📚 Working Principle
The PIR sensor detects infrared radiation from moving bodies.

When motion is detected, the Arduino receives a HIGH signal.

The servo motor is triggered to rotate to 90°.

When no motion is detected, the servo returns to 0°.

💡 Applications
Automatic door opening

Motion-triggered surveillance cameras

Touchless sanitization systems

Smart lighting systems

Security alarms

✅ Justification
This project helps beginners learn:

Interfacing of digital sensors

Servo motor control

Real-time decision-making using sensors and actuators

🧾 Conclusion
The Motion-Activated Servo System is a simple yet effective demonstration of automation using basic electronic components. It introduces key concepts in embedded systems, including sensor interfacing and actuator control, making it a perfect project for beginners.