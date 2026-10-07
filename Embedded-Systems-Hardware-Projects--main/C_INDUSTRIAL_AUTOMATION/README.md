# 🏭 Sub-Division: Industrial Automation & Control

> **Solid-state acoustic switching circuits, contactless RFID identification nodes, and institutional automation systems.**

---

## 🎯 Overview

The **Industrial Automation & Control** sub-division captures the evolution from analog signal conditioning and hardware state machines to microcontroller-driven digital authentication:
1. **Acoustic Signal Processing & Relay Actuation (Clap-Based Switching):** Developed during Semester 1, this project built foundational competence in microphone pre-amplification, comparator thresholding, digital flip-flop latching, and AC mains relay isolation.
2. **Contactless Identity Tracking (RFID Smart Attendance):** Transitioning to digital transceivers, this system utilizes high-frequency radio frequency identification (RFID) to digitize classroom and industrial attendance workflows.

---

## 🗂️ Projects in this Directory

```text
C_INDUSTRIAL_AUTOMATION/
│
├── 📁 Clap_Based_Switching/  # Hands-free acoustic pattern relay controller (Semester 1)
│   └── 🖼️ Clap Based Switch.webp
│
└── 📁 RFID_Attendance/       # Contactless smart attendance station with LCD & cloud sync
    └── 🖼️ Complete suite of hardware prototype and diagnostic photographs
```

---

## 📊 Technical Comparison

| Dimension | Clap-Based Switching | RFID Attendance System |
|---|---|---|
| **Underlying Principle** | Acoustic sound wave transduced into electrical pulse | 13.56 MHz Near-Field Magnetic Induction (ISO/IEC 14443A) |
| **Signal Processing** | Analog Op-Amp / Bandpass Filter / 555 Pulse Stretcher | Digital SPI Packet Parsing from RC522 Transceiver |
| **Latching & State** | CD4017 Decade Counter / JK Flip-Flop | Microcontroller State Machine & Memory Database |
| **Output Stage** | SPDT Mechanical Relay (230V AC Mains Switching) | I2C 16x2 LCD Display + Audio Buzzer + Cloud Record |
| **Academic Phase** | First Semester (Electronics Fundamentals) | Second Semester (Microcontroller Interfacing) |

---

## 🔗 Project Documentation Links

* 👉 [**Clap-Based Switching Detailed README**](./Clap_Based_Switching/README.md)
* 👉 [**RFID Attendance System Detailed README**](./RFID_Attendance/README.md)
