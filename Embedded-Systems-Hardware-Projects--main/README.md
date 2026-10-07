# ⚡ Division 1: Embedded Systems & Hardware Engineering

> **Low-level firmware, circuit schematics, sensor fusion, power electronics, and real-time actuation systems.**

---

## 🧭 Overview

This division contains physical hardware projects designed, assembled, and validated across a three-year engineering timeline. The focus spans microcontrollers, sensor transducers, power semiconductors, motor drivers, communication interfaces, and embedded telemetry.

```text
1_EMBEDDED_SYSTEMS_HARDWARE/
│
├── 📁 A_BATTERY_MANAGEMENT/        # Electric vehicle energy telemetry & high-current protection
│   ├── 📁 EV_Guardian/             # Real-time IoT BMS & GPS vehicle tracker (IdeaLab Internship)
│   └── 📁 EV_Short_Circuit_Prevention/ # Ultrafast solid-state isolation & thermal protection
│
├── 📁 B_SENSOR_IOT/                # Sensor telemetry, environmental control & bio-medical dispensing
│   ├── 📁 Onion_Shelf_Life/        # AgriTech post-harvest atmospheric regulator (SIH Finalist)
│   ├── 📁 Safety_Helmet/           # Industrial hazard & toxic gas detector with fall alert
│   ├── 📁 Smart_Medicine_Box/      # 12-slot biometric dispenser (Patent Application #202621087716)
│   └── 📁 Solar_Tree/              # Biomimetic multi-panel solar harvester (Vigyan Mela 2025)
│
├── 📁 C_INDUSTRIAL_AUTOMATION/     # Factory floor & institutional automation
│   ├── 📁 Clap_Based_Switching/    # Sound-activated solid-state switching (Sem 1 foundational)
│   └── 📁 RFID_Attendance/         # Digital contactless logging with I2C display & cloud sync
│
└── 📁 D_TRANSPORTATION_SAFETY/     # Rail and road smart infrastructure
    ├── 📁 Railway_Obstacle_Avoidance/ # Track hazard detection (SIH 2025 Finalist & Vigyan Mela Offer)
    └── 📁 Smart_Parking_System/    # Bay-occupancy detection & entry guidance (Internship project)
```

---

## 🛠️ Hardware Engineering Competencies Demonstrated

### 1. Power Distribution & Protection
* **High-Current Shunting:** Hall-effect isolation (ACS712) and low-side shunt resistance monitoring.
* **Switching Elements:** Dual-channel power relays, N-channel power MOSFET gates, optocouplers (PC817) for galvanic isolation between high-voltage battery lines and 3.3V/5V microcontroller logic.
* **Thermal Mitigation:** Overcurrent trip protection circuits preventing catastrophic thermal runaway in lithium-ion chemistries.

### 2. Communication Interfaces & Busses
* **I2C (Inter-Integrated Circuit):** 16x2 / 20x4 LCD drivers (PCF8574), RTC DS3231 real-time clocks, OLED diagnostics.
* **SPI (Serial Peripheral Interface):** High-speed MFRC522 RFID reader communications, SD card data logging.
* **UART:** SIM800L GSM/GPRS modem serial commands, Neo-6M GPS NMEA stream parsing, optical biometric sensors.
* **Analog-to-Digital Conversion (ADC):** Multichannel voltage dividers, gas sensor analog output reading, wheatstone bridge amplification (HX711 24-bit ADC for load cells).

### 3. Firmware Architecture & Fail-Safe Design
* **Real-Time Clock (RTC) Scheduling:** Independent battery-backed timekeeping ensuring accurate dispensing even during total power outages.
* **Offline-First Resilience:** Local EEPROM/SD card non-volatile caching to ensure physical devices never freeze or fail to actuate when Wi-Fi is disconnected.
* **Debouncing & Interrupt Handling:** Hardware and software debouncing for pushbuttons, optical encoders, and vibration triggers.

---

## 📂 Sub-Category Quick Links

| Category | Description | Featured Accolade | Sub-README Link |
|---|---|---|---|
| **A. Battery Management** | EV state monitoring, battery pack safety, short-circuit shutdown | IdeaLab Industry Internship | [View Battery Management](./A_BATTERY_MANAGEMENT/README.md) |
| **B. Sensor & IoT** | Smart agriculture, worker safety, patented medicine dispenser, solar tree | **Patent #202621087716** / **SIH Finalist** | [View Sensor & IoT](./B_SENSOR_IOT/README.md) |
| **C. Industrial Automation** | Contactless attendance, hands-free acoustic relays | Early foundational engineering | [View Industrial Automation](./C_INDUSTRIAL_AUTOMATION/README.md) |
| **D. Transportation Safety** | Railway collision avoidance, ultrasonic smart parking guidance | **SIH 2025 Finalist** / **Vigyan Mela Offer** | [View Transportation Safety](./D_TRANSPORTATION_SAFETY/README.md) |

---

*Navigate into any folder above to review specific circuit schematics, hardware prototypes, media demonstrations, and firmware code.*
