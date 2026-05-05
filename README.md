# Simple-CW-Keyer

A simple and efficient Iambic keyer based on **Arduino Nano**. This project allows you to send Morse code using a dual-lever paddle, featuring adjustable speed and audio feedback.

## 🛠️ Features
- Iambic Mode (Type B).
- Adjustable speed (WPM) via potentiometer.
- Audio output via buzzer or speaker.
- Compact design optimized for Arduino Nano.

## 🔌 Pinout / Wiring Diagram

| Component        | Arduino Nano Pin | Notes                        |
| :--------------- | :--------------- | :--------------------------- |
| **Paddle DIT**   | D2               | Connects to GND when pressed |
| **Paddle DAH**   | D3               | Connects to GND when pressed |
| **Potentiometer**| A0               | Speed control (WPM)          |
| **Buzzer/Audio** | D5               | Audio signal output          |
| **Status LED**   | D13              | Built-in LED (optional)      |

## 🚀 Getting Started
1. Ensure you have the **Arduino IDE** installed on your computer.
2. Download the `.ino` file from this repository.
3. Connect your Arduino Nano to your PC.
4. Upload the sketch by clicking the "Upload" button.
5. Wire the components according to the table above.

## ⚙️ Configuration (Optional)
You can customize settings directly in the code, such as:
- Tone frequency (Hz).
- Speed range (Minimum and Maximum WPM).

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
*Developed for the love of Amateur Radio.*
