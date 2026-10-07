# 💻 Division 2: Full-Stack Software & Telemetry Platforms

> **Web dashboards, real-time IoT visualization, caretaker portals, and cloud database synchronization.**

---

## 🎯 Division Overview

Hardware achieves its true power when its streaming data is accessible, actionable, and controllable through intuitive software interfaces.

This division houses the web applications and telemetry platforms built to interface seamlessly with the physical embedded devices developed in **Division 1**:
1. **Smart Medicine Box Web Portal:** A healthcare portal enabling remote family members and physicians to configure medication schedules, monitor intake compliance in real time, and audit missed dose logs.
2. **EV Guardian Web Telemetry Platform:** A responsive electric vehicle diagnostics interface providing live speed, battery pack State-of-Charge (SoC), dynamic distance-to-empty gauges, and GPS map tracking.

---

## 🗂️ Directory Architecture

```text
2_SOFTWARE_FULLSTACK/
│
├── 📁 1.Smart Medicine Box/     # Healthcare caretaker portal & prescription schedule manager
│   └── 📄 README.md
│
└── 📁 2. EV Guardian/           # Live electric vehicle vitals, battery pack gauge & GPS mapper
    └── 📄 README.md
```

---

## 🛠️ Technology Stack & Web Architecture

* **Frontend Presentation:** HTML5 Semantic Structure, Modern Vanilla CSS3 (Glassmorphism, Dark Mode, responsive CSS Grid / Flexbox), Google Fonts (Inter, Outfit).
* **Client-Side Logic:** Modern ECMAScript (ES6+), Event-driven state management, asynchronous fetch pipelines, zero bloated third-party framework overhead.
* **Real-Time Data Pipeline:** Firebase Realtime Database Web SDK (`onValue` listeners), providing sub-second cloud synchronization without manual page refreshes.
* **Data Visualization & Mapping:**
  * **Chart.js:** Time-series line graphs for battery voltage, current discharge curves, and adherence percentages.
  * **Leaflet.js / OpenStreetMap:** Live GPS vehicle location markers with historical breadcrumb route tracking.
  * **SVG / Canvas Gauges:** Smooth animated dials for vehicle speed and battery SoC percentage.

---

## 📊 Software Platforms Overview

| Platform | Companion Hardware | Primary Users | Key Features | Sub-Folder README |
|---|---|---|---|---|
| **Smart Medicine Box Web** | Smart Medicine Box (Patent #202621087716) | Doctors, Caretakers, Family | Schedule configuration, live adherence log, missed dose alerts | [Explore Web Platform](./1.Smart%20Medicine%20Box/README.md) |
| **EV Guardian Web** | EV Guardian Embedded Node | Drivers, Fleet Managers | Real-time battery SoC, range forecasting, live GPS map | [Explore Web Platform](./2.%20EV%20Guardian/README.md) |

---

*Open the individual project folders above to review specific frontend architectures, API data contracts, and integration guides.*
