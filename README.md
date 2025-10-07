# 🔁 8-Channel Relay Module

## 📘 Project Overview
This project presents the design of an **8-Channel Relay Module**, a versatile switching interface for controlling multiple AC or DC devices using microcontrollers such as **Arduino, ESP32, STM32**, or **Raspberry Pi**.  
Each relay channel can be triggered independently to operate high-power devices safely from low-voltage logic signals.

---

## 📷 Project Images

| PCB Routing (Top View) | Schematic (KiCad) | 3D View |
|------------------------|-------------------|---------|
| ![PCB Routing](relay_routing.png) | ![Schematic](relay_schematic.png) | ![3D View](relay_3d.png) |

> 📝 Replace the above filenames with your actual image names (e.g., `Screenshot 2025-10-07 215300.png`).

---

## ⚙ Circuit Description

| Section | Components | Description |
|----------|-------------|-------------|
| **Input Interface** | Header pins (IN1–IN8, VCC, GND) | Connects logic signals from microcontroller |
| **Driver Section** | Transistor array / ULN2803 | Amplifies logic-level signals to drive relay coils |
| **Relay Section** | 8× SPDT Relays (5V or 12V type) | Switches AC or DC loads |
| **Indicator LEDs** | 8× LEDs with resistors | Displays relay ON/OFF status |
| **Power Section** | JD-VCC, VCC, GND headers | Separate power for relay coils and logic (optional isolation) |
| **Output Terminals** | 3-pin screw connectors (NO, COM, NC) | Connects external devices to be controlled |

---

## ✅ Features

- 8 independent relay control channels  
- **Opto-isolated inputs** for safety (if applicable)  
- Compatible with **3.3V or 5V logic systems**  
- **Active LOW** or **Active HIGH** configurable inputs  
- **LED indicators** for each relay  
- Supports both **AC and DC loads**  
- Compact PCB layout, ideal for automation projects  

---

## 🧾 Components List

| Component | Value / Type | Quantity |
|-----------|---------------|----------|
| Relays | 5V / 12V SPDT | 8 |
| Driver IC / Transistors | ULN2803 / BC547 | 1 / 8 |
| Diodes | 1N4007 (Flyback protection) | 8 |
| LEDs | 5mm Red / Green | 8 |
| Resistors | 1kΩ / 2.2kΩ | 8–16 |
| Screw Terminals | 3-Pin | 8 |
| Header Pins | 1×10 / 1×8 | 1 |
| Power Connector | JD-VCC, VCC, GND | 1 |

---

## 🔌 Working Principle
1. **Signal Input:** A low or high logic signal (depending on configuration) is sent from the microcontroller to each channel input (IN1–IN8).  
2. **Driver Activation:** The transistor or driver IC amplifies the signal to energize the corresponding relay coil.  
3. **Relay Operation:** Energized coils switch the contacts between **Normally Open (NO)** and **Normally Closed (NC)** terminals.  
4. **Load Switching:** The connected AC/DC devices are turned ON or OFF as per the relay state.  
5. **Indication:** Each LED glows when its respective relay is activated.

---

## 🧠 Interfacing with Arduino (Example Code)

```cpp
// Example: Sequential relay control
int relayPins[8] = {2,3,4,5,6,7,8,9};
bool activeLow = true;

void setup() {
  for (int i=0; i<8; i++) {
    pinMode(relayPins[i], OUTPUT);
    digitalWrite(relayPins[i], activeLow ? HIGH : LOW);
  }
}

void loop() {
  for (int i=0; i<8; i++) {
    digitalWrite(relayPins[i], activeLow ? LOW : HIGH);
    delay(300);
    digitalWrite(relayPins[i], activeLow ? HIGH : LOW);
    delay(200);
  }
}
