# 🔋 Sub-Division: Battery Management Systems (BMS) & EV Telemetry

> **High-current sensing, voltage monitoring, short-circuit protection, thermal runaway prevention, and cloud-connected vehicle telemetry.**

---

## 🎯 Domain Overview

The electrification of mobility hinges fundamentally on battery safety, operational longevity, and real-time state estimation. Lithium-based chemistries deliver exceptional energy density but are susceptible to thermal runaway, overcurrent degradation, cell imbalance, and cataclysmic damage under short-circuit faults.

This sub-division addresses the two most critical facets of electric vehicle battery engineering:
1. **Intelligent State Telemetry (EV Guardian):** Real-time monitoring of cell voltages, pack discharge currents, thermal levels, geolocation, and dynamic remaining range calculation with cloud streaming.
2. **Sub-Millisecond Fault Isolation (EV Short-Circuit Prevention):** Dedicated analog/digital protection circuitry designed to detect sudden dead-short surges and physically isolate battery terminals before catastrophic thermal destruction occurs.

---

## 🗂️ Projects in this Directory

```text
A_BATTERY_MANAGEMENT/
│
├── 📁 EV_Guardian/
│   │   # Complete IoT BMS & Telemetry Node
│   ├── 📄 Presentation.pdf
│   ├── 📁 Contol/ (Hardware controllers, enclosure photos & operational video)
│   └── 🖼️ High-resolution hardware prototype photographs
│
└── 📁 EV_Short_Circuit_Prevention/
        # Ultra-fast overcurrent trip & galvanic isolation circuit
    └── 🖼️ Short Circuit.jpeg
```

---

## 📊 Comparative Technical Matrix

| Metric / Parameter | EV Guardian | EV Short-Circuit Prevention |
|---|---|---|
| **Primary Objective** | Continuous operational monitoring, health diagnostics, cloud sync | Emergency circuit breaker, hardware protection, arc suppression |
| **Response Horizon** | Periodic polling (100 ms – 1 s intervals) | Sub-millisecond interrupt-driven hardware trip (< 5 ms) |
| **Microcontroller / Core** | ESP32 32-bit Dual-Core MCU (Wi-Fi + BLE) | Dedicated analog comparator / high-speed logic controller |
| **Sensing Modality** | Hall effect current sensor (ACS712), calibrated voltage divider, NTC thermistor, Neo-6M GPS | High-speed differential shunt / Hall sensor with threshold trigger |
| **Output / Actuation** | Firebase cloud telemetry, OLED display, dynamic web dashboard | High-current relay / power MOSFET isolation gate, visual warning LED |
| **Origin / Context** | Developed during Industry Internship at AICTE IdeaLab | Hardware safety prototype for lithium battery packs |

---

## 🔗 Project Documentation Links

* 👉 [**EV Guardian Detailed Documentation**](./EV_Guardian/README.md)
* 👉 [**EV Short-Circuit Prevention Detailed Documentation**](./EV_Short_Circuit_Prevention/README.md)
