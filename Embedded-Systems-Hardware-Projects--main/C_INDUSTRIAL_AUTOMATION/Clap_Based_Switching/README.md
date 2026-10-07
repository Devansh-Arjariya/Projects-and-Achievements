# 👏 Clap-Based Switching System

> **Acoustic Pattern Detection, Analog Signal Conditioning, and Solid-State Mains Relay Actuation.**

[![Semester](https://img.shields.io/badge/Milestone-Semester%201%20Foundational-blue.svg)](#)
[![Domain](https://img.shields.io/badge/Domain-Home%20Automation%20%7C%20Analog%20Circuits-brightgreen.svg)](#)
[![Status](https://img.shields.io/badge/Status-Completed%20%26%20Verified-success.svg)](#)

---

## 📌 Context & Engineering Significance

Developed during the **first semester of B.Tech**, this foundational project marked the essential transition from theoretical circuit theory to practical physical hardware assembly.

The objective was to create a hands-free, sound-activated home automation system that allows individuals with mobility limitations or users in dark rooms to toggle electrical appliances (lamps, fans, AC appliances) using a distinct acoustic signature (sharp handclap).

---

## ⚙️ Operating Principle & Circuit Workflow

```mermaid
flowchart LR
    A["Handclap / Sound Impulse"] --> B["Electret Condenser Microphone"]
    B --> C["Transistor Pre-Amp / Op-Amp Stage"]
    C --> D["Bandpass / Noise Decoupling Stage"]
    D --> E["555 Timer Monostable Multivibrator"]
    E --> F["CD4017 Decade Counter (Bistable Toggle)"]
    F --> G["NPN Transistor Driver (BC547)"]
    G --> H["Electromechanical Relay (10A 230V AC)"]
    H --> I["AC Mains Appliance (Lamp / Fan)"]
```

---

## 🔬 Subsystem Breakdown

### 1. Transducer & Preamplifier Stage
* An **electret condenser microphone** biased through a $10 \, k\Omega$ resistor converts sound pressure fluctuations into tiny millivolt AC signals ($1 - 10 \, mV$).
* A low-noise **BC547 NPN transistor** in common-emitter configuration amplifies the weak signal with a voltage gain ($A_v \approx 100$).

### 2. Signal Shaping & Pulse Stretching
* Normal background conversation creates low-level continuous noise. A clap creates a high-amplitude, short-duration transient ($< 20 \, ms$).
* An **NE555 timer** configured in monostable mode acts as a pulse stretcher, converting the fast acoustic spike into a clean, debounced square-wave digital pulse of fixed duration ($~100 \, ms$).

### 3. Digital State Latching
* A **CD4017 CMOS decade counter** receives the clean clock pulse at Pin 14.
* On each successive pulse, the active high output toggles between Pin 3 (Output 0) and Pin 2 (Output 1), converting momentary sound pulses into a sustained ON/OFF latch.

### 4. Galvanic Mains Isolation & Switching
* The active high output saturates a switching transistor (BC547), energizing the $5V$ or $12V$ coil of an SPDT relay.
* A freewheeling **1N4007 flyback diode** across the relay coil absorbs inductive back-EMF spikes when de-energizing, protecting the semiconductor stages.

---

## 📊 Technical Component Matrix

| Stage | Component | Specific Model / Value | Key Role |
|---|---|---|---|
| **Acoustic Transducer** | Condenser Mic | 2-pin Electret (High Sensitivity) | Sound pressure to electrical AC conversion |
| **Preamplifier** | BJT Transistor | BC547 (General Purpose NPN) | Small signal amplification |
| **Pulse Shaper** | IC Timer | NE555 Precision Timer | Glitch elimination and pulse stretching |
| **Logic Toggle** | CMOS IC | CD4017 Decade Counter / Divider | Bistable ON/OFF toggle state machine |
| **Driver & Protection** | Diode & Driver | 1N4007 + BC547 | Coil actuation and back-EMF suppression |
| **Mains Switch** | Power Relay | Sugar Cube 5V/12V SPDT Relay | 230V AC / 10A galvanic load isolation |

---

## 🖼️ Hardware Photographic Verification

* 📸 [**Clap Based Switch.webp**](./Clap%20Based%20Switch.webp) — High-resolution view of the assembled PCB circuit board demonstrating the microphone pickup, integrated IC sockets, relay block, and screw terminal mains interface.
