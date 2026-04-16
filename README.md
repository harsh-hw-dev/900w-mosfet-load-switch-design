# 🔌 FR120N MOSFET PWM Driver (Up to 900W)

A high-power PWM-controlled MOSFET driver circuit designed to switch loads up to **900W** using the **FR120N MOSFET module**. This project combines hardware design with ESP32-based PWM control for real-world power electronics applications.

---

## 📷 Schematic Overview

![Schematic](./assets/schematic.png)

> Designed with proper gate control, resistor network, and protection elements for stable switching operation.

---

## ⚡ Key Features

* 🔥 Supports **high-power loads (up to 900W)**
* 🎛️ **PWM control** using microcontroller (ESP32)
* ⚙️ Optimized **gate drive resistor network**
* 💡 LED indicator for switching status
* 🧱 Simple, robust, and hardware-friendly design
* 🧪 Ready for real-world prototyping

---

## 🧠 Working Principle

1. PWM signal is applied from ESP32.
2. Signal passes through resistor network (R2, R3) for conditioning.
3. Driver stage controls MOSFET gate switching.
4. MOSFET turns ON/OFF rapidly based on PWM duty cycle.
5. Load receives controlled power.
6. LED indicates switching activity.

---

## 🔧 Components Used

| Component | Value         |
| --------- | ------------- |
| R1        | 4.7K          |
| R2        | 1K            |
| R3        | 4.7K          |
| R4        | 10K           |
| R5        | 100K          |
| MOSFET    | FR120N Module |
| D1        | LED           |
| D2        | Diode         |
| Input     | PWM           |
| Supply    | +VE / -VE     |

---

## 🔌 Hardware Connection (ESP32)

| ESP32 Pin       | Circuit   |
| --------------- | --------- |
| GPIO 5          | PWM Input |
| GND             | GND       |
| External Supply | +VE / -VE |

---

## 💻 ESP32 PWM Control Code

```cpp
// ================= PWM MOSFET DRIVER =================
// Board: ESP32

#define PWM_PIN 5
#define PWM_CHANNEL 0
#define PWM_FREQ 20000
#define PWM_RESOLUTION 8

int dutyCycle = 0;

void setup() {
  Serial.begin(115200);

  ledcSetup(PWM_CHANNEL, PWM_FREQ, PWM_RESOLUTION);
  ledcAttachPin(PWM_PIN, PWM_CHANNEL);

  Serial.println("PWM Driver Started");
}

void loop() {

  // Ramp UP
  for (dutyCycle = 0; dutyCycle <= 255; dutyCycle++) {
    ledcWrite(PWM_CHANNEL, dutyCycle);
    delay(10);
  }

  delay(1000);

  // Ramp DOWN
  for (dutyCycle = 255; dutyCycle >= 0; dutyCycle--) {
    ledcWrite(PWM_CHANNEL, dutyCycle);
    delay(10);
  }

  delay(1000);
}
```

---

## 📌 Applications

* ⚡ DC Motor Speed Control
* 💡 High-power LED dimming
* 🔋 Battery load control
* 🏭 Industrial automation
* 🔌 Power switching systems

---

## ⚠️ Design Notes (IMPORTANT)

* Use proper **heat sink** for MOSFET
* Ensure **thick PCB traces** for high current
* Add **flyback diode** for inductive loads
* Keep **gate loop short** to reduce noise
* Use proper **grounding practices**

---

## 📁 Project Structure

```
├── assets/
│   └── schematic.png
├── code/
│   └── esp32_pwm_driver.ino
├── design/
│   └── schematic.SchDoc
├── README.md
```

---

## 🚀 Future Improvements

* Add **gate driver IC (like IR2110 / TC4420)**
* Include **current sensing**
* Add **overcurrent protection**
* Closed-loop control using feedback

---

## 👨‍💻 Author

**Harsh Saini**
Electronics & Communication Engineer
Focus: Power Electronics | Embedded Systems | Hardware Design

---

## 📜 License

MIT License — Free to use, modify, and distribute.

---

## ⭐ Support

If this project helped you, give it a ⭐ on GitHub!
