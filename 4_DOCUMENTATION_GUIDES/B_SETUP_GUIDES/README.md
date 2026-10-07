# 🛠️ Guide B: Firmware Toolchain & Development Environment Setup

> **Step-by-Step Installation Walkthrough for Compilers, Board Packages, Drivers, and Core Libraries.**

---

## 📌 Development Environments

The firmware across this portfolio is developed and flashed using two primary environments:
1. **Arduino IDE (v2.x) / VS Code with PlatformIO**
2. **Espressif ESP-IDF (v5.x)**

---

## 💻 1. USB-to-UART Bridge Drivers

Ensure the appropriate USB serial driver is installed to establish communication with microcontrollers:
* **Silicon Labs CP2102 / CP2104:** Standard on NodeMCU ESP32 DevKit boards.
* **WCH CH340G / CH341:** Common on budget clone boards and Arduino Nanos.
* *Verification:* Open Windows Device Manager -> `Ports (COM & LPT)` and confirm your board mounts as a recognized COM port (e.g., `COM3`, `COM7`).

---

## 📦 2. ESP32 Board Package Configuration

In Arduino IDE:
1. Go to **File -> Preferences -> Additional Board Manager URLs**.
2. Add:
   ```text
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
3. Open **Boards Manager**, search for `esp32` by Espressif Systems, and install version **2.0.14+**.
4. Select Board: `DOIT ESP32 DEVKIT V1` or `ESP32 WROOM DA Module`.

---

## 📚 3. Core Library Dependencies

Install the following libraries via Arduino Library Manager or PlatformIO `lib_deps`:

```text
# IoT & Cloud Telemetry
Firebase ESP Client by Mobizt (v4.4.14+)
ArduinoJson by Benoit Blanchon (v6.21.3)

# Display & Busses
LiquidCrystal I2C by Frank de Brabander
Adafruit SSD1306 & Adafruit GFX Library

# Sensors & Inputs
DHT sensor library by Adafruit
MFRC522 by GithubCommunity
TinyGPSPlus by Mikal Hart
HX711 Arduino Library by Bogdan Necula
Adafruit Fingerprint Sensor Library

# Actuators & Motors
AccelStepper by Mike McCauley
Servo (ESP32Servo by Kevin Harrington)

# Timekeeping
RTClib by Adafruit (DS3231 driver)
```

---

## ⚡ 4. Recommended Flashing Settings

* **Upload Speed:** `921600` (Fast flashing) or `115200` (Fail-safe)
* **CPU Frequency:** `240 MHz (WiFi/BT)`
* **Flash Frequency:** `80 MHz`
* **Flash Mode:** `QIO`
* **Partition Scheme:** `Default 4MB with spiffs (1.2MB APP / 1.5MB SPIFFS)` or `Huge APP (3MB No OTA)` for heavy SSL/Firebase payloads.
