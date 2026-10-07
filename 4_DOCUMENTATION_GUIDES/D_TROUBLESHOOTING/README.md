# 🔧 Guide D: Hardware Troubleshooting & Debugging Playbook

> **Field-Tested Solutions for Common Embedded Errors, Power Spikes, Bus Freezes, and Signal Noise.**

---

## ⚠️ 1. "Brownout detector was triggered" (ESP32 Infinite Reboot Loop)

### Root Cause
When the ESP32 initiates Wi-Fi radio transmission (`WiFi.begin()`), the internal RF power amplifier draws brief surge currents up to **$350 - 500 \, mA$**. If powered from a weak USB laptop port or poor jumper cables, the 3.3V rail dips below $2.7V$, causing the hardware brownout reset circuit to reboot the chip.

### Field Solution
1. Place a **$470 \, \mu F$ to $1000 \, \mu F$ low-ESR electrolytic capacitor** directly across `3V3` and `GND` of the development board.
2. Power the module using an external regulated power supply capable of supplying at least **$1.0A$ continuous**.
3. (Emergency test only) Disable software brownout detection in `setup()`:
   ```c
   #include "soc/soc.h"
   #include "soc/rtc_cntl_reg.h"
   WRITE_PERI_REG(RTC_CNTL_BROWN_OUT_REG, 0); // Disable brownout detector
   ```

---

## 📶 2. SIM800L GSM Module Restarts During Network Registration

### Root Cause
The SIM800L requires **up to $2.0A$ peak current** during GSM network handshakes. Standard 5V USB supplies cannot deliver this instantaneous inrush, causing the module to shut down.

### Field Solution
* Use a dedicated **LM2596 step-down buck converter** tuned to **$4.0V - 4.2V$**.
* Solder a **$1000 \, \mu F$ capacitor** directly across the SIM800L `VCC` and `GND` pins as close as physically possible to the chip.

---

## 🔄 3. I2C Bus Hangs / Freezes (`Wire.endTransmission()` Blocks Forever)

### Root Cause
If an I2C slave (e.g., LCD, RTC, or sensor) loses power momentarily or suffers line noise, it can pull `SDA` low and get stuck in a clock-stretching loop. The standard Arduino `Wire` library blocks infinitely waiting for acknowledgment.

### Field Solution
1. Ensure external **$4.7 \, k\Omega$ pull-up resistors** are installed on both `SDA` and `SCL`.
2. Enable hardware I2C timeouts (available in ESP32 Arduino Core):
   ```cpp
   Wire.setTimeOut(50); // Timeout in milliseconds
   ```
3. Implement a bus recovery routine that toggles `SCL` 9 times manually on boot to flush stuck slave registers.

---

## ⚡ 4. SPI Bus Conflict (RC522 RFID + MicroSD Card Reader)

### Root Cause
Both devices share `SCK`, `MISO`, and `MOSI`. Certain cheap MicroSD card breakout modules fail to release the `MISO` line into high-impedance (tri-state) when their Slave Select (`CS`) is pulled high, effectively jamming the RFID reader.

### Field Solution
* Verify that the MicroSD card module has proper bi-directional buffer circuitry (such as a 74LVC125) rather than cheap passive resistor dividers.
* Ensure both devices have dedicated, non-overlapping `CS` (Chip Select) pins and pull unselected CS lines HIGH before initiating SPI transfers.
