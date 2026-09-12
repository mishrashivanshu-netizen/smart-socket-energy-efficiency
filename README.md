# Smart Socket for Energy Efficiency ⚡

> **Hardware & Prototype Implementation**

A smart electrical socket prototype designed to improve energy efficiency through **automatic power control, load detection, overcharging prevention, status indication, and IoT-based remote monitoring**.

This repository documents the **hardware/prototype side of the project** and organizes the system architecture, components, prototype images, and operating logic in one place.

---

## 📌 Project Overview

The Smart Socket for Energy Efficiency addresses unnecessary power consumption associated with idle chargers and continued charging after a device is fully charged.

The prototype combines an **ESP32 microcontroller**, current and voltage sensing, a relay-based switching stage, temperature/humidity sensing, RGB status LEDs, and a **Blynk IoT** interface.

The system can operate in **manual and automatic modes** and can provide remote ON/OFF control and real-time status monitoring through the mobile application.

---

## 🎯 Objectives

- Reduce unnecessary standby/phantom power consumption.
- Automatically disconnect power when an idle charger is detected.
- Prevent continued charging after the connected device reaches full charge.
- Provide remote socket control through Wi-Fi/Bluetooth connectivity.
- Monitor electrical parameters such as voltage and current.
- Provide clear visual status indication using RGB LEDs.
- Add temperature-based protection against overheating conditions.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| Automatic Power Cut-off | Disconnects the supply when preset charging/idle conditions are detected. |
| Idle Charger Detection | Detects a charger connected without an active device and disconnects power after a delay. |
| Overcharging Prevention | Cuts power when charging is considered complete based on current behavior. |
| Remote Control | Allows ON/OFF control through the Blynk IoT application. |
| Wi-Fi & Bluetooth | ESP32 provides wireless connectivity. |
| Energy Monitoring | Current and voltage sensors support real-time electrical monitoring. |
| Temperature Monitoring | DHT11 is used for temperature/humidity sensing and overheating protection logic. |
| RGB Status Indication | LEDs indicate standby, charging, and fully charged states. |

---

## 🧩 Hardware Components

### 1. ESP32 Microcontroller
Acts as the central processing unit and manages communication between the sensors, relay, and Blynk IoT platform.

![ESP32 Microcontroller](images/esp32-microcontroller.jpg)

### 2. Relay Module
A **10A/250V electromechanical relay** is used as the switching mechanism for controlling the connected AC load.

![Relay Module](images/relay-module.jpg)

### 3. ACS712 Current Sensor
The **ACS712** Hall-effect current sensor is used to measure current draw and help determine the charging/load condition.

![ACS712 Current Sensor](images/acs712-current-sensor.jpg)

### 4. ZMPT101B Voltage Sensor
The voltage sensing stage monitors AC voltage and supports voltage/power monitoring.

![ZMPT101B Voltage Sensor](images/zmpt101b-voltage-sensor.jpg)

### 5. TJA1050 CAN Bus Module
The TJA1050 module provides an interface between the ESP32 and CAN-based networks.

![TJA1050 CAN Bus Module](images/can-bus-module-tja1050.jpg)

### 6. DHT11 Sensor
The DHT11 provides temperature and humidity measurements. The prototype uses temperature information as part of its overheating protection strategy.

![DHT11 Sensor](images/dht11-temperature-humidity-sensor.jpg)

### 7. RGB Status LEDs

Three status indications are used:

- **Red** — Standby
- **Blue** — Charging
- **Green** — Fully charged

---

## 🏗️ System Architecture

The major functional blocks of the prototype are:

```text
                 AC INPUT
                    │
                    ▼
          ┌───────────────────┐
          │   Power Supply    │
          └─────────┬─────────┘
                    │
                    ▼
        ┌────────────────────────┐
        │     ESP32 Controller   │
        └───┬──────┬──────┬──────┘
            │      │      │
            ▼      ▼      ▼
       Current   Voltage  Temperature
       Sensor    Sensor   / Humidity
            │      │      │
            └──────┴──────┘
                    │
                    ▼
             Decision Logic
                    │
                    ▼
              ┌──────────┐
              │  Relay   │
              └────┬─────┘
                   │
                   ▼
              AC SOCKET
                   │
                   ▼
             Charging Load

        ESP32  ←→  Wi-Fi / Bluetooth
                   │
                   ▼
              Blynk IoT App
```

---

## 🔌 Hardware Connection

The research paper's connection diagram shows the interconnection of the **ESP32, current sensor, voltage sensor, temperature sensor, and relay**.

![Connection Diagram](images/connection-diagram.jpg)

### Prototype Hardware

![Hardware Connection](images/hardware-connection.jpg)

---

## ⚙️ Working Principle

### Automatic Mode

1. The system monitors the charger/load through the sensing circuitry.
2. If a charger is connected without a device, the system waits for **15 seconds**.
3. If the condition remains unchanged, the relay disconnects the power supply to reduce unnecessary standby consumption.
4. When a device is charging, the current sensor monitors the charging current.
5. When the measured current is **above 0.5 A**, the system identifies the charging condition and activates the **blue LED**.
6. When current remains **equal to or below 0.5 A for more than 10 seconds**, the system considers charging complete.
7. The relay disconnects the power supply and the **green LED** indicates completion.

### Manual Mode

In manual mode, the user can control the socket directly through the Blynk application.

When the socket is switched OFF manually, the system enters standby mode and the **red LED** indicates the status.

---

## 📱 Blynk IoT Application

The prototype uses the **Blynk IoT platform** for remote monitoring and control.

The application provides:

- Remote ON/OFF control
- Manual/automatic operation
- Voltage monitoring
- Current monitoring
- Device status
- Charging status
- Notifications for relevant conditions

![Blynk App](images/blynk-app.jpg)

### Power Control

**Power ON**

![Blynk Power ON](images/blynk-power-on.jpg)

**Power OFF**

![Blynk Power OFF](images/blynk-power-off.jpg)

---

## 💡 Status Indication

| LED | Status |
|---|---|
| 🔴 Red | Standby |
| 🔵 Blue | Device charging |
| 🟢 Green | Fully charged |

### Charging Indication

![Blue LED Charging](images/blue-led-charging.jpg)

### Standby Indication

![Red LED Standby](images/red-led-standby.jpg)

---

## 🧪 Prototype

The final prototype uses a rectangular enclosure containing the controller, relay, sensors, and associated circuitry. A standard electrical outlet is provided on the front for connecting devices.

![Final Prototype](images/final-prototype.jpg)

---

## 📊 Prototype Features vs. Conventional Socket

| Feature | Conventional Socket | Smart Socket |
|---|:---:|:---:|
| Remote ON/OFF | ❌ | ✅ |
| Automatic Power Cut-off | ❌ | ✅ |
| Real-time Energy Monitoring | ❌ | ✅ |
| Wi-Fi & Bluetooth Connectivity | ❌ | ✅ |
| Automatic Idle-Charger Cut-off | ❌ | ✅ |
| Overcharging Protection | ❌ | ✅ |

---

## 📈 Reported Outcomes

According to the accompanying research paper, the proposed smart socket was designed to reduce energy waste associated with standby/idle charging and unnecessary continued charging.

The paper reports an estimated **around 30% contribution to energy savings** and discusses automatic cutoff, remote monitoring, and device protection as key benefits.

> Note: The figures and performance claims in this section are reported in the associated research paper and are not presented here as independent measurements from this repository.

---

## 🚀 Applications

Potential applications include:

- Smart homes
- Mobile charging stations
- Energy-efficient charging systems
- Residential power management
- Smart electrical outlets
- IoT-based energy management systems

---

## 🔮 Future Scope

Potential future improvements identified in the associated work include:

- Machine-learning-based intelligent power optimization
- Integration with renewable energy sources such as solar power
- Improved cybersecurity and encryption
- More advanced energy monitoring
- Enhanced smart-home integration

---

## 👨‍🔧 Project Contribution

**Role: Hardware & Prototype Development**

Contribution focused on the **hardware/prototype implementation** of the project, including practical system assembly, component integration, circuit implementation, and prototype-level testing.

This repository is intended to document the **engineering prototype and hardware implementation**, not to claim authorship of the associated research paper.

---

## 📚 Research Reference

The technical background and prototype documentation are based on the associated IEEE conference paper:

**“Smart Socket for Energy Efficiency”**

Published in the **2025 IEEE International Conference on Recent Advances in Computing and Systems (REACS)**.

DOI: `10.1109/REACS67479.2025.11413567`

---

## ⚠️ Safety Notice

This project involves **AC mains voltage**. Working with 220–250 V AC can cause serious injury, electric shock, fire, or death.

Do not reproduce or modify the mains-side circuit without appropriate electrical safety knowledge, isolation, protection, supervision, and testing equipment.

---

## 📁 Repository Structure

```text
smart-socket-energy-efficiency/
│
├── README.md
│
└── images/
    ├── esp32-microcontroller.jpg
    ├── relay-module.jpg
    ├── acs712-current-sensor.jpg
    ├── zmpt101b-voltage-sensor.jpg
    ├── can-bus-module-tja1050.jpg
    ├── dht11-temperature-humidity-sensor.jpg
    ├── connection-diagram.jpg
    ├── hardware-connection.jpg
    ├── blynk-app.jpg
    ├── final-prototype.jpg
    ├── blue-led-charging.jpg
    ├── red-led-standby.jpg
    ├── blynk-power-on.jpg
    └── blynk-power-off.jpg
```

---

## ⭐ Project Highlights

**Smart Socket for Energy Efficiency**

**Core Areas:**  
`Electrical Systems` · `IoT` · `Energy Efficiency` · `Embedded Hardware` · `Sensors` · `Automatic Power Control`

**Prototype Focus:**  
`ESP32` · `ACS712` · `ZMPT101B` · `Relay` · `DHT11` · `Blynk IoT`
