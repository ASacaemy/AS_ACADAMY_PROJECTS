# 🔐 Security Alert System with LCD Display using Arduino

This project is a **Motion Detection Security Alert System** using an Arduino Uno. It features a PIR motion sensor, LEDs for visual alerts, a buzzer for audio alerts, and an LCD display to show system status. It is ideal for beginner Arduino enthusiasts who want to learn interfacing multiple components like sensors, buzzers, LCDs, and switches.

## 🧰 Components Used

| Component           | Quantity |
|---------------------|----------|
| Arduino Uno         | 1        |
| PIR Motion Sensor   | 1        |
| 16x2 LCD Display     | 1        |
| Breadboard          | 1        |
| Push Buttons        | 2        |
| Red LED             | 2        |
| Buzzer              | 1        |
| 220Ω Resistor       | 4        |
| 10kΩ Potentiometer  | 1        |
| Jumper Wires        | As needed |


## 📋 How It Works

- The **sensor** (e.g., gas or PIR) reads analog values.
- If the sensor reading is above a threshold:
  - **Red LED and buzzer activate**
  - LCD alternates messages: "ALERT" and "EVACUATE"
- If the reading is below the threshold:
  - **Green LED stays on**
  - LCD alternates: "SAFE" and "ALL CLEAR"

## 📟 Arduino Code

```cpp
#include <LiquidCrystal.h>    // Include the LCD Library

// Initialize LCD: (rs, enable, d4, d5, d6, d7)
LiquidCrystal lcd(5, 6, 8, 9, 10, 11);

// Define pins for output devices
int redled = 2;   // Red LED pin (danger indicator)
int greenled = 3;  // Green LED pin (Safe indicator)
int buzzer = 4;    // Buzzer pin for alarm

// Define analog input for sensor
int sensor = A0;         // Sensor connected to analog pin A0
int sensorThresh = 400;  // Threshold value for danger detection 

void setup()
{
  pinMode(redled, OUTPUT);
  pinMode(greenled, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(sensor, INPUT);

  Serial.begin(9600);
  lcd.begin(16, 2);
}

void loop()
{
  int analogValue = analogRead(sensor);
  Serial.println(analogValue);

  if (analogValue > sensorThresh)
  {
    digitalWrite(redled, HIGH);
    digitalWrite(greenled, LOW);
    tone(buzzer, 1000, 10000);

    lcd.clear();
    lcd.setCursor(0, 1);
    lcd.print("ALERT");
    delay(1000);

    lcd.clear();
    lcd.setCursor(0, 1);
    lcd.print("EVACUATE");
    delay(1000);
  }
  else
  {
    digitalWrite(greenled, HIGH);
    digitalWrite(redled, LOW);
    noTone(buzzer);

    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("SAFE");
    delay(1000);

    lcd.clear();
    lcd.setCursor(0, 1);
    lcd.print("ALL CLEAR");
    delay(1000);
  }
}
