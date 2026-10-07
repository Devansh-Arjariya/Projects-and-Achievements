# 🚗 EV Guardian — Embedded Telemetry & Smart Battery Management Node

> **Real-time IoT Battery Diagnostics, Geolocation Tracking, Range Forecasting, and Cloud Telemetry for Electric Vehicles.**

[![Project Status](https://img.shields.io/badge/Status-Complete%20%26%20Field%20Tested-success.svg)](#)
[![Hardware](https://img.shields.io/badge/MCU-ESP32%20Dual--Core-blue.svg)](#)
[![Internship](https://img.shields.io/badge/Developed%20At-IdeaLab%20Internship-orange.svg)](#)
[![Cloud](https://img.shields.io/badge/Backend-Firebase%20Realtime%20DB-yellow.svg)](#)

---

## 📌 Executive Overview

**EV Guardian** is an automotive-grade embedded IoT telemetry module designed to solve the critical visibility and reliability gaps in light electric vehicles (2-wheelers, 3-wheelers, and custom EV prototypes). By combining high-precision analog sensing, multi-constellation GPS geolocation, and high-frequency cloud synchronization, EV Guardian transforms a passive battery pack into an intelligent, connected energy system.

Developed during an engineering internship at **AICTE IdeaLab**, the prototype interfaces with physical battery cells, computes dynamic State-of-Charge (SoC), estimates real-time driving range based on instantaneous power consumption, and streams time-series data to a cloud dashboard.

---

## 🎯 Core Engineering Objectives

* **Battery State Diagnostics:** Continuous tracking of terminal voltage, instantaneous discharge/regeneration current, and ambient pack temperatures.
* **Dynamic Range Estimation:** Real-time distance-to-empty calculations based on moving average energy consumption ($Wh/km$) rather than static voltage lookup tables.
* **Asset Tracking & Anti-Theft:** Integrated satellite positioning providing live latitude, longitude, vehicle speed, and geofencing coordinates.
* **Cloud Telemetry Pipeline:** Transmission of formatted JSON telemetry packets over Wi-Fi/GSM to Firebase Realtime Database.
* **Emergency Alerting:** Real-time triggers for deep discharge warnings, overcurrent surges, and overheating conditions.

---

## 🏗️ Hardware Architecture & System Topology

```mermaid
flowchart TD
    subgraph SENSING["Sensory Inputs"]
        V_SENSE["Precision Voltage Divider (Pack V)"]
        I_SENSE["ACS712 / Hall Current Sensor (Pack I)"]
        T_SENSE["NTC Thermistor / DS18B20 (Pack Temp)"]
        GPS["Neo-6M GPS Module (UART)"]
    end

    subgraph PROCESSING["Core Processing Unit"]
        ESP32["ESP32 Dual-Core Microcontroller<br/>(240 MHz, FreeRTOS Tasks)"]
        FLASH["Non-Volatile SPIFFS / EEPROM Log"]
    end

    subgraph DISPLAY["Local Diagnostics"]
        OLED["0.96 inch I2C OLED / LCD"]
        LED_IND["RGB Status Indicators"]
        BUZZER["Acoustic Fault Alarm"]
    end

    subgraph TELEMETRY["Cloud & End User"]
        WIFI["Wi-Fi 802.11 b/g/n / GSM"]
        FIREBASE["Firebase Realtime Database"]
        WEB_APP["EV Guardian Web Dashboard"]
    end

    V_SENSE -->|Analog ADC1| ESP32
    I_SENSE -->|Analog ADC1| ESP32
    T_SENSE -->|Analog / 1-Wire| ESP32
    GPS -->|UART RX/TX (Pins 16/17)| ESP32

    ESP32 <--> FLASH
    ESP32 --> OLED
    ESP32 --> LED_IND
    ESP32 --> BUZZER

    ESP32 -->|TLS Encrypted JSON| WIFI
    WIFI --> FIREBASE
    FIREBASE --> WEB_APP
```

---

## ⚡ Technical Specifications & Pin Mapping

| Component / Subsystem | Interface | ESP32 Pin Mapping | Functional Description |
|---|---|---|---|
| **Voltage Sensor** | Analog ADC | `GPIO 34 (ADC1_CH6)` | Reads scaled-down battery pack voltage (0–3.3V mapped to 0–60V) |
| **Current Sensor (ACS712)** | Analog ADC | `GPIO 35 (ADC1_CH7)` | Bi-directional Hall current sensing (measures up to ±30A) |
| **Neo-6M GPS Module** | Hardware UART2 | `GPIO 16 (RX2), GPIO 17 (TX2)` | 9600 baud NMEA sentence streamer ($GPRMC, $GPGGA) |
| **I2C Status Display** | I2C Bus | `GPIO 21 (SDA), GPIO 22 (SCL)` | Shows live voltage, current, SoC %, and IP/Cloud status |
| **Warning Buzzer** | Digital Output | `GPIO 25` | PWM alert for low battery (<15%) or overtemperature (>55°C) |
| **Status LEDs** | Digital Output | `GPIO 26 (Green), GPIO 27 (Red)` | System health and cloud connectivity indicator |

---

## 🧮 Embedded Mathematical Algorithms

### 1. State of Charge (SoC) Calculation
The firmware implements Coulomb Counting supplemented by Open Circuit Voltage (OCV) calibration:
$$SoC(t) = SoC(t_0) - \frac{1}{C_{nominal}} \int_{t_0}^{t} I(\tau) \, d\tau$$
Where:
* $C_{nominal}$ is the total rated capacity in Ampere-hours ($Ah$).
* $I(\tau)$ is the instantaneous current (positive during discharge, negative during regen).

### 2. Dynamic Remaining Range ($R_{remaining}$)
$$R_{remaining} = \frac{E_{available}}{E_{consumption\_rate}} = \frac{V_{pack} \times Capacity_{remaining} \times \eta}{P_{avg} / v_{avg}}$$
Where $P_{avg}$ is average power in Watts and $v_{avg}$ is vehicle ground speed in $km/h$.

---

## 📁 Repository Directory Assets

* 📄 [**Presentation.pdf**](./Presentation.pdf) — Complete engineering slide deck detailing project design, problem formulation, and testing.
* 📁 [**Contol/**](./Contol/) — Hardware controller assembly, sub-chassis photos, and full operational demo video (`WhatsApp Video 2026-10-05 at 20.53.35.mp4`).
* 🖼️ Prototype Photographs:
  * `WhatsApp Image 2026-08-01 at 07.13.55.jpeg` — Benchtop hardware circuit testing.
  * `WhatsApp Image 2026-08-01 at 07.13.56.jpeg` — Sensor calibration and ESP32 breadboard wiring.
  * `WhatsApp Image 2026-08-01 at 07.13.58.jpeg` — Integration with display and power rails.
  * `WhatsApp Image 2026-08-01 at 07.13.59.jpeg` — Pack enclosure and field assembly view.

---

## 🌐 Companion Software & Edge AI Extensions

* 💻 **Web Dashboard:** See [`2_SOFTWARE_FULLSTACK/2. EV Guardian`](../../../2_SOFTWARE_FULLSTACK/2.%20EV%20Guardian/README.md) for the live telemetry portal.
* 🤖 **Edge AI Inference:** See [`3_MACHINE_LEARNING_EDGE_AI/A_BATTERY_MODELS`](../../../3_MACHINE_LEARNING_EDGE_AI/A_BATTERY_MODELS/README.md) for on-chip machine learning State-of-Health models.
