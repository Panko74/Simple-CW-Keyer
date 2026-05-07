# Simple-CW-Keyer

A professional-grade Morse code iambic keyer based on the Arduino platform. This project features a 600Hz hardware PWM sidetone with a logarithmic volume curve, an intuitive OLED interface, and persistent settings storage.

## 🚀 Key Features

*   **Three Operating Modes:**
    *   **Iambic A:** Standard iambic timing.
    *   **Iambic B:** Added dot/dash memory for high-speed efficiency.
    *   **BUG-SIM:** A smart Bug simulator for single and dual paddles and sideswipers.
    *   **Straight Key:** Manual mode for traditional keys or external controllers.
*   **Logarithmic Volume Control:** 11 levels (0-10) mapped to an exponential curve to match human hearing perception. Level 0 is full mute.
*   **Hardware PWM Sidetone:** Generates a clean 600Hz tone using Arduino's Timer 1 (Pin 9) for low-latency audio.
*   **Smart OLED Interface:** High-contrast display for WPM speed, mode selection, and TX status.
*   **Practice Mode (Bypass):** Toggle the radio output to practice your timing without keying your transmitter.
*   **EEPROM Persistence:** Saves WPM, Mode, and Volume settings permanently.
*   **Power Management:** Auto-dims the display after 15 seconds of inactivity to prevent burn-in and save power.

# 🛠 Hardware Specifications & Wiring Guide

This document describes the electrical connections and the circuit design for the Arduino CW Iambic Keyer.

## 1. Connection Table (Netlist)

| Component | Pin | Arduino Pin | Description |
| :--- | :--- | :--- | :--- |
| **OLED Display** | VCC | 5V | Power supply |
| **OLED Display** | GND | GND | Ground |
| **OLED Display** | SCL | A5 | I2C Clock |
| **OLED Display** | SDA | A4 | I2C Data |
| **Buzzer** | + | **D9** | **Must be D9** (Timer 1 PWM) |
| **Buzzer** | - | GND | Ground |
| **Paddle Dot** | Tip | D2 | Active LOW (Internal Pull-up) |
| **Paddle Dash** | Ring | D3 | Active LOW (Internal Pull-up) |
| **Button WPM Up**| Pin A | D4 | Active LOW (Internal Pull-up) |
| **Button WPM Down**| Pin A | D5 | Active LOW (Internal Pull-up) |
| **Button Mode** | Pin A | D6 | Active LOW (Internal Pull-up) |
| **Button Bypass**| Pin A | D8 | Active LOW (Internal Pull-up) |
| **Radio Out** | Signal| D12 | To Isolation Circuit |

*Note: All buttons and paddles should connect to **GND** when pressed.*

---

## 2. Recommended Radio Interface (Opto-Isolation)

To protect your Arduino from high voltages or transients on the radio's keying line, use an optoisolator circuit.

### Components:
*   **U1:** PC817 or 4N35 Optocoupler
*   **R1:** 470Ω Resistor

### Schematic Logic:
1.  **Arduino D12** ⮕ **R1 (470Ω)** ⮕ **Anode (Pin 1)** of U1.
2.  **Arduino GND** ⮕ **Cathode (Pin 2)** of U1.
3.  **Radio Key Line (+)** ⮕ **Collector (Pin 4)** of U1.
4.  **Radio Ground/Shield** ⮕ **Emitter (Pin 3)** of U1.

---

## 3. Logarithmic Volume Rationale

The volume is controlled via **Phase Correct PWM** on **Timer 1**. The duty cycle follows this lookup table for a natural auditory increase:

| Level | Duty Cycle (OCR1A value) | Perception |
| :---: | :---: | :--- |
| 0 | 0 | Muted / Off |
| 1 | 2 | Very Faint |
| 5 | 60 | Comfortable Room Volume |
| 10| 833 | Max Volume (50% Square Wave) |

*The ICR1 register is set to 1666 to achieve a ~600Hz frequency with an 8MHz/16MHz clock and prescaler 8.*

## 🕹 Operation Guide

### Basic Controls
*   **Adjust Speed:** Tap **WPM Up** or **WPM Down**.
*   **Change Mode:** Tap the **Mode** button to cycle through Straight -> Iambic A -> Iambic B.
*   **Bypass TX:** Tap the **Bypass** button. The screen will toggle between `[ONLINE]` and `[PRACTICE]`.

### Advanced Functions
*   **Logarithmic Volume Adjustment:** 
    1.  Hold the **Mode** button (keep it pressed).
    2.  Tap **WPM Up** to increase or **WPM Down** to decrease volume.
    3.  Release **Mode**. (The mode will not change if a volume adjustment was detected).
*   **Save Settings:** Long press the **Bypass** button for 1 second. The screen will flash `>> SAVED! <<`. Your settings will now load automatically on the next boot.

## ⚙️ Installation & Requirements

1.  **Arduino Sketch:** Download the latest release from https://github.com/Panko74/Simple-CW-Keyer/releases
2.  **Libraries:** Install the **U8g2** library via the Arduino Library Manager.
3.  **Board:** Select **Arduino Nano** (or Uno). 
4.  **Note:** This code utilizes direct register access for **Timer 1** to ensure a precise 600Hz tone. Do not move the Buzzer from Pin 9, as it is hardware-dependent.

## 📜 License
Open Source. Developed for the Ham Radio community. 73!
