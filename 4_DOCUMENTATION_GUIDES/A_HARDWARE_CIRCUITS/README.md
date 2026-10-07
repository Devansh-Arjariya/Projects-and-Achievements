# 📐 Guide A: Hardware Circuits, Schematics & Interfacing Rules

> **Standardized Circuit Design Rules, Bus Topologies, Power Isolation, and Electrical Best Practices.**

---

## 📌 Standard Voltage Domains & Logic Level Translation

Modern embedded systems interface 3.3V CMOS microcontrollers (ESP32) with legacy 5V TTL sensors (MQ gas sensors, 5V relays, ultrasonic HC-SR04). Failing to respect logic level boundaries destroys MCU input pins or leads to unreliable floating inputs.

### 1. 5V to 3.3V Voltage Divider (e.g., HC-SR04 Echo Pin to ESP32 GPIO)
$$V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2} = 5.0V \times \frac{2.2\,k\Omega}{1.0\,k\Omega + 2.2\,k\Omega} \approx 3.43V$$

```text
5V Signal Pin (Echo) ----[ 1.0 kΩ ]----+---- GPIO Pin (ESP32 3.3V Input)
                                       |
                                  [ 2.2 kΩ ]
                                       |
                                      GND
```

---

## ⚡ Inductive Load Protection (Relays & Solenoid Motors)

When an inductive coil (relay, motor, solenoid) is de-energized, its magnetic field collapses instantly, inducing a high-voltage reverse EMF spike ($\mathcal{E} = -L \frac{dI}{dt}$) exceeding hundreds of volts.

**Mandatory Rule:** Always place a high-speed diode (**1N4007** or **1N4148**) in reverse-parallel across coil terminals:

```text
 +Vcc (5V / 12V) --------------+-----------------+
                               |                 |
                             [COIL]            [▲ DIODE (1N4007 cathode to +Vcc)]
                               |                 |
 Transistor Collector ---------+-----------------+
```

---

## 🔌 I2C Bus Pull-Up Resistors

Both SDA and SCL lines are open-drain. While internal MCU weak pull-ups exist (~30–50 kΩ), long jumper leads introduce parasite capacitance, rounding clock edges and causing I2C communication hangs (`ESP_ERR_TIMEOUT`).

* **Rule:** Place external **$4.7 \, k\Omega$ pull-up resistors** on both `SDA` and `SCL` to the 3.3V rail when multiple I2C peripherals are shared on the bus.

---

## 🛡️ Decoupling Capacitors & Ground Planes

* Place a **$100 \, nF$ ceramic capacitor** immediately adjacent to the VCC/GND pins of each digital IC (MFRC522, DS3231, ESP32) to absorb high-frequency digital switching transients.
* Place a **$100 \, \mu F$ to $470 \, \mu F$ electrolytic bulk capacitor** across the power supply rails near high-current actuators (GSM SIM800L, Stepper motor drivers).
