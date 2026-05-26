# Smart_gate_project
# 🚗 Smart Gate System — Arduino + Ultrasonic Sensor

An automated vehicle gate controller built with Arduino UNO that uses an HC-SR04 ultrasonic sensor to detect approaching vehicles, triggers a servo motor to open/close the gate, and blinks an LED as a visual indicator.

📺 **[Watch Demo on YouTube](https://youtu.be/zDtyfH2O-VQ)**

---

## 📸 Circuit Preview

> Simulated in [Wokwi](https://wokwi.com) — Arduino UNO with HC-SR04 sensor, servo motor, LED + resistor.

---

## 🧰 Components

| Component | Quantity |
|---|---|
| Arduino UNO | 1 |
| HC-SR04 Ultrasonic Sensor | 1 |
| Servo Motor (SG90 or similar) | 1 |
| LED (Red) | 1 |
| 220Ω Resistor | 1 |
| Jumper Wires | As needed |
| Breadboard | 1 |

---

## 🔌 Pin Connections

| Arduino Pin | Connected To |
|---|---|
| Pin 9 | HC-SR04 TRIG |
| Pin 10 | HC-SR04 ECHO |
| Pin 7 | LED (via 220Ω resistor) |
| Pin 6 | Servo Signal Wire |
| 5V | HC-SR04 VCC, Servo VCC |
| GND | HC-SR04 GND, Servo GND, LED GND |

---

## ⚙️ How It Works

1. The HC-SR04 sensor continuously measures distance to detect any object or vehicle within **20 cm**.
2. When a vehicle is detected:
   - The gate servo sweeps from **0° → 90°** (opens).
   - The LED blinks during the sweep.
   - A `"Vehicle Detected!"` message is printed to Serial Monitor.
3. The gate stays open for **5 seconds**.
4. After 5 seconds, the sensor rechecks:
   - If the path is **clear** (distance > 20 cm) → gate closes (90° → 0°).
   - If the vehicle is **still present** → gate remains open and a warning is shown.
5. The loop repeats every 200 ms.

---

## 📁 Project Files

```
├── Arduino_code.txt         # Main Arduino sketch
├── blockly_gate_control.txt # Custom Blockly block definition for gate speed
├── preview.html             # Interactive browser dashboard (simulated UI)
└── wokwi_project.png        # Wokwi circuit simulation screenshot
```

### `preview.html` — Web Dashboard
A standalone HTML dashboard that simulates the gate system visually in a browser. Features:
- Animated gate bar (open/close)
- Sensor status indicator (CLEAR / DETECTED)
- 5-second countdown timer
- Live activity log

Open `preview.html` in any browser — no server required.

### `blockly_gate_control.txt` — Custom Blockly Block
Defines a drag-and-drop **"Open Gate With Speed"** block for use in block-based programming environments (e.g., Wokwi's Blockly editor). Speed (1–10) maps to a servo angle for intuitive control.

---

## 🚀 Getting Started

### 1. Upload the Code
- Open `Arduino_code.txt` in the [Arduino IDE](https://www.arduino.cc/en/software).
- Select **Board:** Arduino UNO and the correct **Port**.
- Click **Upload**.

### 2. Open Serial Monitor
- Set baud rate to **9600**.
- Watch distance readings and gate events in real time.

### 3. Test It
- Move your hand or an object within 20 cm of the sensor.
- The gate (servo) should open, wait 5 seconds, and close.

### 4. Try the Web Dashboard
- Open `preview.html` in your browser.
- Click **"Simulate Vehicle Detection"** to see the animated gate and log.

---

## 🖥️ Try It Online (Wokwi)

You can simulate this project without any hardware on [Wokwi](https://wokwi.com). Import the circuit from the screenshot and paste the Arduino code.

---

## 📐 Distance Formula

The HC-SR04 measures distance using the time-of-flight of an ultrasonic pulse:

```
distance (cm) = duration (µs) × 0.034 / 2
```

`0.034` is the speed of sound in cm/µs. Dividing by 2 accounts for the round trip.

---

## 🛠️ Customization

| Parameter | Location | Default |
|---|---|---|
| Detection threshold | `loop()` — `distance < 20` | 20 cm |
| Gate open duration | `loop()` — `delay(5000)` | 5 seconds |
| Servo open angle | `openGate()` — `pos <= 90` | 90° |
| Sweep speed | `openGate/closeGate()` — `pos += 2` | 2°/step |

---

## 📄 License

This project is open source and free to use for educational purposes.
