# 📡 Guide C: Telemetry API References & Cloud Data Contracts

> **Standardized JSON Packet Schemas, Firebase Realtime Database Hierarchies, and REST Payload Definitions.**

---

## 📌 Cloud Architecture Principles

Across the IoT platforms (**EV Guardian**, **Smart Medicine Box**, **Onion Shelf-Life Extender**), devices synchronize using lightweight JSON documents over TLS/SSL WebSockets and HTTPS REST APIs via Firebase Realtime Database.

---

## 🚗 1. EV Guardian Telemetry Schema

* **Target Path:** `/ev_guardian/{vehicle_id}/live`
* **Sync Interval:** 1000 ms (1 Hz while driving)

```json
{
  "timestamp": 1728302400,
  "battery": {
    "voltage": 52.4,
    "current": 14.8,
    "power_watts": 775.5,
    "soc_percent": 78.5,
    "temp_celsius": 34.2
  },
  "dynamics": {
    "speed_kmh": 42.6,
    "predicted_range_km": 68.4,
    "energy_wh_per_km": 32.1
  },
  "gps": {
    "latitude": 23.259933,
    "longitude": 77.412615,
    "altitude_m": 498.2,
    "satellites": 9
  },
  "status_flags": {
    "overcurrent_warning": false,
    "thermal_warning": false,
    "emergency_cutoff_active": false
  }
}
```

---

## 💊 2. Smart Medicine Box Adherence Schema

* **Target Path:** `/smart_medicine_box/{device_id}/slots/{slot_id}`
* **Sync Trigger:** On scheduled dispense event & physical intake confirmation

```json
{
  "slot_id": 1,
  "medication": "Metformin 500mg",
  "scheduled_hour": 8,
  "scheduled_minute": 30,
  "pills_count": 14,
  "event_log": {
    "dispense_timestamp": "2026-10-07T08:30:02Z",
    "verified_by_ir": true,
    "verified_by_weight": true,
    "weight_delta_grams": 0.65,
    "patient_auth_type": "FINGERPRINT",
    "status": "COMPLETED"
  }
}
```

---

## 🧅 3. Onion Storage Chamber Climate Schema

* **Target Path:** `/storage_chambers/{chamber_id}/telemetry`
* **Sync Interval:** 30 seconds

```json
{
  "chamber_id": "CHAMBER_NORTH_02",
  "temperature_c": 24.8,
  "humidity_rh": 58.2,
  "air_quality_ppm": 320,
  "exhaust_fan_active": false,
  "intake_fan_active": true,
  "warning_status": "NORMAL"
}
```
