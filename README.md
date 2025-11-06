# 📬 Electronic Letter Box

### 🧠 Overview

The **Electronic Letter Box** is a smart mailbox system designed to notify the user when a physical letter is received.
It uses an **IR sensor**, **Arduino**, **buzzer**, **LED**, and **HC-05 Bluetooth module** to detect incoming mail and send instant notifications to a user’s smartphone.

---

## ⚙️ Features

* 🔔 **Buzzer and LED alerts** when a letter is detected.
* 📱 **Bluetooth notification** sent to the user’s phone using the “Serial Bluetooth Terminal” app.
* 🧠 **Arduino-based automation** for simple and reliable control.
* 💡 **Low-cost and easily extendable** prototype for smart home integration.

---

## 🧩 Components Used

| Component              | Description                                  |
| ---------------------- | -------------------------------------------- |
| Arduino Uno            | Microcontroller board for processing signals |
| IR Sensor              | Detects the presence of a letter             |
| HC-05 Bluetooth Module | Sends notification to smartphone             |
| LED                    | Visual indication of mail received           |
| Buzzer                 | Audible indication of mail received          |
| Breadboard & Jumpers   | For circuit connections                      |
| Resistors (270Ω)       | To limit current for LED & buzzer            |

---

## 🔌 Circuit Connections

**Buzzer**

* +ve → 270Ω resistor → Arduino Pin 7
* -ve → GND

**LED**

* +ve → 270Ω resistor → Arduino Pin 6
* -ve → GND

**IR Sensor**

* VCC → 5V
* GND → GND
* OUT → Arduino Pin 2

**HC-05 Bluetooth Module**

* VCC → 5V
* GND → GND
* TXD → Arduino RX (Pin 0)
* RXD → Arduino TX (Pin 1)

---

## 🧠 Working Principle

* When a letter is dropped into the box, the **IR sensor detects** its presence.
* The Arduino triggers both **LED** and **buzzer** for notification.
* Simultaneously, a **Bluetooth message** (“You have got a mail”) is sent to the user’s smartphone.
* Once the letter is removed, the sensor resets the notification state.

---

## 💻 Arduino Code

```cpp
#include <SoftwareSerial.h>

#define RxD 1
#define TxD 0
SoftwareSerial BTserial(RxD, TxD);

const int irSensorPin = 2;
const int ledPin = 6;
const int buzzerPin = 7;

void setup() {
  Serial.begin(9600);
  BTserial.begin(9600);
  pinMode(irSensorPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  int sensorValue = digitalRead(irSensorPin);
  if (sensorValue == HIGH) {
    digitalWrite(ledPin, LOW);
    noTone(buzzerPin);
  } else {
    digitalWrite(ledPin, HIGH);
    tone(buzzerPin, 10000);
    BTserial.println("You have got a mail!");
    delay(100);
  }
}
```

---

## 📊 Results

* The system successfully detects letters and triggers both visual (LED) and audible (buzzer) alerts.
* Notifications are received on the **Serial Bluetooth Terminal** app in real-time.

---

## 🚀 Future Improvements

1. **IoT Integration** – Connect to Wi-Fi for cloud-based notifications.
2. **Power Optimization** – Use low-power components or solar panels.
3. **Advanced Sensors** – Add ultrasonic or PIR sensors for better accuracy.
4. **Weatherproof Design** – Make it suitable for outdoor use.

---

## 📚 References

* [Arduino Official Documentation](https://www.arduino.cc/en/Guide)
* [HC-05 Bluetooth Module Guide](https://www.geeksforgeeks.org/all-about-hc-05-bluetooth-module-connection-with-android/)
* [Wikipedia: Arduino](https://en.wikipedia.org/wiki/Arduino)

---

## 👩‍💻 Authors

**Sai Rupesh S** – 1CR22EC193
**Vidhya Sri A** – 1CR22EC239
**Department of Electronics and Communication Engineering**
Under the guidance of **Dr. Niranjan L**
📅 *Project Date: 12-01-2024*

---


