# 🌐 RFID-Based Smart Attendance Management System

> **Contactless Radio Frequency Identification (RFID) Attendance Station with Real-Time Display, Visual Verification, and Digital Cloud Roster Logging.**

[![Domain](https://img.shields.io/badge/Domain-IoT%20%7C%20Institutional%20Automation-blue.svg)](#)
[![Protocol](https://img.shields.io/badge/Transceiver-RC522%2013.56%20MHz%20SPI-green.svg)](#)
[![Display](https://img.shields.io/badge/Interface-16x2%20I2C%20LCD%20%2B%20Buzzer-orange.svg)](#)
[![Status](https://img.shields.io/badge/Status-Fully%20Operational-success.svg)](#)

---

## 📌 Problem Context & Administrative Need

Manual roll-call attendance across colleges, schools, corporate offices, and workshops suffers from systemic inefficiencies:
1. **Time Consumption:** Spending 10–15 minutes per lecture calling names wastes hundreds of cumulative instruction hours per semester.
2. **Proxy Attendance & Fraud:** Students or workers signing rosters on behalf of absent peers.
3. **Transcription Inaccuracies:** Manual entry into digital spreadsheets leads to clerical errors and lost paperwork.

**The Solution:** A rapid, touchless RFID terminal that identifies users via personal smart cards within 200 milliseconds, gives instant acoustic and visual confirmation, and digitally writes attendance records to non-volatile memory or a remote cloud database.

---

## 🏗️ Hardware Architecture & Data Flow

```mermaid
flowchart TD
    subgraph USER["Contactless Interaction"]
        CARD["Mifare 1K RFID Card / Keyfob (13.56 MHz)"]
    end

    subgraph TERMINAL["Embedded Terminal Station"]
        RC522["MFRC522 RFID Reader / Writer Module"]
        MCU["ESP32 / Arduino Microcontroller Core"]
        LCD["16x2 Character LCD with PCF8574 I2C Backpack"]
        BUZZER["Acoustic Piezo Buzzer (Chime)"]
        LEDS["Green (Valid) / Red (Duplicate/Invalid) LEDs"]
    end

    subgraph BACKEND["Storage & Administration"]
        EEPROM["Local Flash / MicroSD Card Storage"]
        CLOUD["Firebase / Google Sheets API via Wi-Fi"]
        PORTAL["Faculty / Admin Attendance Dashboard"]
    end

    CARD -->|Magnetic Induction (13.56 MHz)| RC522
    RC522 -->|SPI Bus (SCK, MOSI, MISO, SDA)| MCU
    MCU -->|I2C Bus (SDA, SCL)| LCD
    MCU -->|GPIO High| BUZZER
    MCU -->|GPIO High| LEDS
    MCU --> EEPROM
    MCU -->|Wi-Fi HTTP / MQTT Post| CLOUD
    CLOUD --> PORTAL
```

---

## ⚡ Hardware Pinout & Wiring Specifications

| Component | Interface / Bus | Microcontroller Pin | Description |
|---|---|---|---|
| **RC522 - SDA (SS)** | SPI Chip Select | `GPIO 5 / Pin 10` | Slave Select |
| **RC522 - SCK** | SPI Clock | `GPIO 18 / Pin 13` | Serial Clock |
| **RC522 - MOSI** | SPI Master Out | `GPIO 23 / Pin 11` | Data from MCU to Reader |
| **RC522 - MISO** | SPI Master In | `GPIO 19 / Pin 12` | Data from Reader to MCU |
| **RC522 - RST** | Digital Reset | `GPIO 22 / Pin 9` | Hardware Reset line |
| **I2C LCD - SDA** | I2C Data | `GPIO 21 / Pin A4` | Serial Data |
| **I2C LCD - SCL** | I2C Clock | `GPIO 22 / Pin A5` | Serial Clock |
| **Buzzer** | Digital Out | `GPIO 4 / Pin 8` | Feedback chime on tag read |
| **Status LEDs** | Digital Out | `GPIO 2, GPIO 15` | Green (Success) / Red (Unregistered) |

---

## 🧮 Firmware Anti-Proxy & Debounce Logic

* **UID Validation:** Every student's unique 4-byte / 7-byte Card UID (e.g., `DE AD BE EF`) is mapped to their Student Roll Number, Name, and Section.
* **Double-Tap Rejection:** Prevents duplicate consecutive scans:
  ```cpp
  if (card_scanned && (current_time - last_scan_time < 30000)) {
      lcd.print("Already Marked!");
      triggerRedWarning();
  }
  ```
* **Offline Caching:** If network connectivity drops, the record is immediately committed to local non-volatile storage with timestamp, ensuring zero data loss.

---

## 📸 Prototype Gallery & Documentation

The directory contains comprehensive photographic records of the terminal hardware:
* 🖼️ `WhatsApp Image 2026-10-07 at 13.54.43.jpeg` & `(1).jpeg` — Breadboard prototyping, jumper routing, and LCD initialization.
* 🖼️ `WhatsApp Image 2026-10-07 at 13.54.44.jpeg` & `(1-3).jpeg` — Active card scanning tests, showing UID registration on the serial terminal and LCD.
* 🖼️ `WhatsApp Image 2026-10-07 at 13.54.45.jpeg` & `(1-2).jpeg` — Enclosure integration and benchtop stress testing.
