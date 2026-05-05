# Simple-CW-Keyer

A professional-grade Morse code iambic keyer based on the Arduino platform. This project features a 600Hz hardware PWM sidetone with a logarithmic volume curve, an intuitive OLED interface, and persistent settings storage.

## 🚀 Key Features

*   **Three Operating Modes:**
    *   **Iambic A:** Standard iambic timing.
    *   **Iambic B:** Added dot/dash memory for high-speed efficiency.
    *   **Straight Key:** Manual mode for traditional keys or external controllers.
*   **Logarithmic Volume Control:** 11 levels (0-10) mapped to an exponential curve to match human hearing perception. Level 0 is full mute.
*   **Hardware PWM Sidetone:** Generates a clean 600Hz tone using Arduino's Timer 1 (Pin 9) for low-latency audio.
*   **Smart OLED Interface:** High-contrast display for WPM speed, mode selection, and TX status.
*   **Practice Mode (Bypass):** Toggle the radio output to practice your timing without keying your transmitter.
*   **EEPROM Persistence:** Saves WPM, Mode, and Volume settings permanently.
*   **Power Management:** Auto-dims the display after 15 seconds of inactivity to prevent burn-in and save power.

## 🛠 Hardware Setup

### Component List
*   **MCU:** Arduino Nano/Uno (ATmega328P).
*   **Display:** SSD1306 OLED (128x64) via I2C.
*   **Audio:** Passive Piezo Buzzer.
*   **Input:** CW Paddle (Stereo jack) + 4 Tactile buttons.
*   **Output:** Transistor or Optocoupler circuit to trigger your Radio's Key line.

### Pinout Mapping
| Pin | Function | Description |
|:---:|:---|:---|
| **D2** | Dot Paddle | Input (Internal Pull-up) |
| **D3** | Dash Paddle | Input (Internal Pull-up) |
| **D4** | WPM Up | Increases speed |
| **D5** | WPM Down | Decreases speed |
| **D6** | Mode / Shift | Changes mode / Modifier for Volume |
| **D8** | Bypass / Save | Toggle TX / Long press to Save to EEPROM |
| **D9** | Buzzer | **PWM Output** (Hardcoded for Timer 1) |
| **D12**| Radio Out | Digital Output to Transmitter |
| **A4** | SDA | OLED Data |
| **A5** | SCL | OLED Clock |

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

1.  **Libraries:** Install the **U8g2** library via the Arduino Library Manager.
2.  **Board:** Select **Arduino Nano** (or Uno). 
3.  **Note:** This code utilizes direct register access for **Timer 1** to ensure a precise 600Hz tone. Do not move the Buzzer from Pin 9, as it is hardware-dependent.

## 📜 License
Open Source. Developed for the Ham Radio community. 73!
