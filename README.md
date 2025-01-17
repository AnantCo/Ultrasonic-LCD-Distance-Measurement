# Ultrasonic LCD Distance Measurement

This project demonstrates how to use an ultrasonic sensor (e.g., HC-SR04) with an Arduino to measure distance and display the readings on an LCD screen. This is a beginner-friendly project, ideal for those learning about Arduino, sensors, and basic robotics.

---

## 📜 Description

The ultrasonic sensor measures the distance of an object by sending out sound waves and timing how long it takes for the echo to return. The calculated distance is then displayed on an LCD screen and printed on the Serial Monitor for debugging purposes.

---

## 🚀 Features

- Measures distances in centimeters (CM) using the HC-SR04 ultrasonic sensor.
- Displays the distance on a 16x2 LCD screen.
- Outputs the distance data to the Serial Monitor for real-time debugging.

---

## 🛠️ Components Required

1. Arduino Board (e.g., Uno, Mega, Nano)
2. HC-SR04 Ultrasonic Sensor
3. 16x2 LCD Display
4. 10K Potentiometer (for LCD contrast adjustment)
5. Breadboard and Connecting Wires
6. Power Source (e.g., USB cable or battery)

---

## 📐 Circuit Diagram

1. Connect the **Trig** pin of the ultrasonic sensor to pin `12` of the Arduino.
2. Connect the **Echo** pin of the ultrasonic sensor to pin `11` of the Arduino.
3. Connect the **LCD RS, EN, D4, D5, D6, D7** pins to Arduino pins `10, 9, 8, 7, 6, 5` respectively.
4. Power the ultrasonic sensor and LCD with the 5V and GND pins of the Arduino.
5. Use the potentiometer to adjust the LCD contrast.

---

## 💻 Code

Here is the Arduino code used for this project:

```cpp
#include <LiquidCrystal.h>
LiquidCrystal lcd = LiquidCrystal(10,9,8,7,6,5); // Create an LCD object. Parameters: (RS, E, D4, D5, D6, D7):
const int trigPin = 12;
const int echoPin = 11;
float time, distance;

void setup() 
{
    lcd.begin(16, 2); // Specify the LCD's number of columns and rows. Change to (20, 4) for a 20x4 LCD
    pinMode(trigPin, OUTPUT);  
    pinMode(echoPin, INPUT);  
    Serial.begin(9600);
}

void loop() 
{
    digitalWrite(trigPin, LOW);  
    delayMicroseconds(2);  
    digitalWrite(trigPin, HIGH);  
    delayMicroseconds(10);  
    digitalWrite(trigPin, LOW);  

    time = pulseIn(echoPin, HIGH);
    distance = (time * 0.0343) / 2;  

    // For Serial Monitor
    Serial.print("Distance:CM ");  
    Serial.println(distance);  

    // For LCD Display
    lcd.setCursor(0, 0);
    lcd.print("Distance in CM");
    lcd.setCursor(0, 1);
    lcd.print(distance);
}
![ultrasonic with lcd](https://github.com/user-attachments/assets/abee826a-52e8-47f4-be53-8a5548ab0a89)
