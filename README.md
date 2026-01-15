# IoT Smart Home Project
### IoT Network Simulation using Cisco Packet Tracer

![License](https://img.shields.io/badge/License-MIT-blue.svg) ![Cisco Packet Tracer](https://img.shields.io/badge/Simulation-Cisco%20Packet%20Tracer-1ba0d7) ![Status](https://img.shields.io/badge/Status-Completed-success)

## 1. Project Overview

This project simulates a fully integrated **Smart Home Ecosystem** connected to a **Cloud-based IoT Infrastructure**. Unlike simple LAN-only simulations, this project demonstrates a realistic **Hybrid Cloud Architecture** where the home network acts as a client to a remote Central Office Service Provider.

The simulation models the complete data path from local sensors, through a residential Gateway, across a simulated ISP WAN, to a centralized IoT Server and Cellular Network. It is designed to demonstrate key concepts in Wireless Communication, IoT Protocols, and Network Security.

---

## 2. Project Objectives

The primary goal is to build a scalable, secure, and fail-safe smart home environment.

*   **Secure Architecture**: Design a modular network with distinct security zones (Home, ISP, Cloud, Cellular).
*   **IoT Client-Server Model**: Implement a remote registration model where devices push data to a cloud server rather than a local controller.
*   **Safety Critical Systems**: Simulate emergency handling (Fire/Flood) using dedicated embedded systems (MCU) that function independently of network connectivity.
*   **Remote Connectivity**: Enable remote access to critical components via a simulated Cloud & ISP environment.
*   **Hybrid Networking**: Implement a mix of wired (Ethernet/Serial/Coaxial) and wireless (Wi-Fi/Cellular) connections for realistic network emulation.
*   **Full Ecosystem Simulation**: Emulate a complete ecosystem including Home Gateway, ISP Routers, DHCP Servers, DNS logic, and Mobile interactions.

---

## 3. Detailed Topology & Architecture

The network is logically and physically segmented into four distinct zones, mirroring real-world ISP architectures.

### 3.1. Home Local Network (LAN)
*   **Network Segment**: `192.168.25.0/24`
*   **Home Gateway (DLC 100)**:
    *   **Role**: Acts as the border device, NAT router, and Wi-Fi Access Point.
    *   **LAN Interface**: `192.168.25.1` (Static).
    *   **WAN Interface**: `200.0.0.10` (Dynamically assigned by `home-isp` DHCP pool).
    *   **Wi-Fi SSID**: `Home-IoT-Net` (WPA2-PSK Protected).
*   **Function**: Connects all local smart appliances (Lights, Fans, Doors) via Wi-Fi/Ethernet.
*   **Data Flow**: Devices generate telemetry -> Gateway (NAT) -> ISP -> Remote Server.

### 3.2. ISP Access Network (WAN)
*   **Network Segment**: `200.0.0.0/24`
*   **Backbone Router (ISP-Main-RT)**:
    *   **Interface**: `GigabitEthernet0/0` (`200.0.0.1`).
    *   **Connectivity**: Connects to the ISP Cloud via a high-speed coaxial bridge (`Cable-Modem-PT`).
*   **Routing**: Handles static routing between the residential block (`200.x`) and the Central Office (`203.x`).

### 3.3. Central Office / Cloud Services
*   **Network Segment**: `203.0.0.0/24`
*   **Key Infrastructure**:
    *   **IoT Registration Server**: `203.0.0.3` (The "Brain" of the operation).
    *   **DNS/HTTP Server**: `203.0.0.2` (Resolves `iot.server.com` and handles web requests).
    *   **Central Office Server**: `203.0.0.10` (Management).
*   **Function**: Hosts the centralization platform where all home devices register and store data. It acts as the "Cloud" for the smart home.

### 3.4. Cellular Network (Mobile)
*   **Network Segment**: `172.16.1.0/24`
*   **Provider Name**: `ptcellular`
*   **Cell Tower**: Connected to `ISP-Cloud` via the Backbone.
*   **Smartphone Configuration**:
    *   **Interface**: `3G/4G Cell1`.
    *   **IP Address**: `172.16.1.100` (Dynamic).
*   **Function**: Allows external remote control of the home. The smartphone is **not** on the home Wi-Fi; it accesses the home securely via the WAN.

---

## 4. Technical Configuration Reference

### 4.1. IoT Server Credentials
The centralized registration server is pre-configured with the following authorized user accounts.

| Service Account | Username | Password | Purpose |
| :---: | :---: | :---: | :---: |
| **Admin** | `admin` | `admin` | Full System Access |
| **Monitoring** | `camera` | `123456` | Read-Only (Video) |
| **Security** | `lock` | `123456` | Door/Gate Authorization |

### 4.2. DHCP & Addressing Hierarchy
The network relies on a complex DHCP hierarchy managed by the **DNS-HTTP-Server**.

*   **Pool `home-isp`**:
    *   **Gateway**: `200.0.0.1`
    *   **DNS**: `203.0.0.2`
    *   **Range**: `200.0.0.10` to `200.0.0.254`
*   **Pool `co server`**:
    *   **Gateway**: `202.0.0.1`
    *   **DNS**: `203.0.0.2`
*   **Pool `serverPool`**:
    *   **Gateway**: `203.0.0.1`
    *   **DNS**: `203.0.0.2`
    *   **Range**: `203.0.0.10+`
*   **Pool `LAN` (GW)**:
    *   **Gateway**: `192.168.25.1`
    *   **Range**: `192.168.25.100+`

### 4.3. Link Layer & Connectivity
*   **ISP Backhaul**: High-speed Serial links at **2Mbps Clock Rate** (`204.0.0.0/30`, `205.0.0.0/30`).
*   **Last Mile**: Coaxial Cable via `CoaxialSplitter-PT` and `Cable-Modem-PT`.
*   **Wireless**: 802.11n (2.4GHz) WPA2-PSK.

---

## 5. Detailed Device Inventory & Map

The simulation is spatially organized. Each device is explicitly named and mapped to a specific Zone.

### Zone 1: Living Area
| Device Name | Device ID | Connection | Primary Function |
| :---: | :---: | :---: | :--- |
| **Thermostat** | `Thermostat iot26` | Wi-Fi | Monitors temp; triggers HVAC |
| **Webcam** | `Webcam living` | Wi-Fi | Streams video; records motion |
| **Ceiling Fan** | `Fan living fan` | Wi-Fi | 3-Speed fan (Auto-mode) |
| **Main Window** | `Window living` | Wi-Fi | Motorized window actuator |
| **Smoke Sensor** | `Fire Monitor` | Wired | Analog fire detection input |

### Zone 2: Kitchen & Utility
| Device Name | Device ID | Connection | Primary Function |
| :---: | :---: | :---: | :--- |
| **Smart Appliance** | `Appliance ioT10` | Wi-Fi | Generic load simulation |
| **Security Door** | `Door Kitchen` | Wi-Fi | Remote status reporting |
| **Water Sensor** | `Water Level` | Wired | Detects leaks/floods |

### Zone 3: Bedrooms (Master, #1, #2)
| Device Name | Device ID | Connection | Primary Function |
| :---: | :---: | :---: | :--- |
| **Master Window** | `Window Master` | Wi-Fi | Automated ventilation |
| **Master Cam** | `Webcam Master` | Wi-Fi | Security monitoring |
| **Bedroom 1 Fan** | `Fan BR#1 fan` | Wi-Fi | Local comfort control |
| **Bedroom 1 Door** | `Door BR#1 door` | Wi-Fi | Privacy lock |
| **Bedroom 2 Fan** | `Fan BR#2 fan` | Wi-Fi | Local comfort control |

### Zone 4: Outdoor & Safety
| Device Name | Device ID | Connection | Primary Function |
| :---: | :---: | :---: | :--- |
| **Garage Sensor** | `Motion Detector` | Wired | Triggers garage lights |
| **Garage Door** | `Garage Door` | Wired | Motorized entry |
| **Lawn Sprinkler** | `Lawn Sprinkler` | Wired | Activates on Fire/Schedule |
| **Siren** | `Siren` | Wired | High-decibel audible alarm |

---

## 6. Automation Logic & Scripts (Pseudo-Code)

### 6.1. Safety Critical (Local MCU)
*Logic running on the CustomMCU chip (Fail-safe).*

**Rule: Fire Emergency**
```python
IF (analogRead(Smoke_Sensor) > 10.0):
    digitalWrite(Fire_Sprinkler, HIGH)
    digitalWrite(Siren, HIGH)
    print("CRITICAL: Fire Detected!")
ELSE:
    digitalWrite(Fire_Sprinkler, LOW)
    digitalWrite(Siren, LOW)
```

**Rule: Flood Prevention**
```python
IF (analogRead(Water_Level) > 15):
    digitalWrite(Drain_Pump, HIGH)
    print("WARNING: High Water Level.")
ELSE:
    digitalWrite(Drain_Pump, LOW)
```

### 6.2. Comfort & Security (Cloud Engine)
*Logic running on the IoT Server (Orchestration).*

**Rule: Intelligent Climate Control**
```javascript
IF (Thermostat.Temperature > 25):
    Set(CeilingFan.Status, "High")
    Set(AirConditioner.Status, "On")
ELSE IF (Thermostat.Temperature > 22):
    Set(CeilingFan.Status, "Low")
    Set(AirConditioner.Status, "Off")
ELSE:
    Set(CeilingFan.Status, "Off")
```

**Rule: Intrusion Detection**
```javascript
IF (MotionDetector.State == "Active" AND Home.Mode == "Away"):
    Set(Webcam.Record, "True")
    Set(Siren.State, "On")
    SendNotification("Intruder in Garage!")
```

---

## 7. Simulation User Guide

Follow these steps to explore the simulation features in Cisco Packet Tracer.

### 7.1. Accessing the IoT Dashboard
1.  Click on the **Smartphone** located above the house.
2.  Navigate to the **Desktop** tab.
3.  Click the **IoT Monitor** icon (blue graphic).
4.  Click **Login** (Server `203.0.0.3` / `admin` are pre-filled).
5.  **Result**: You will see all connected devices. Click to toggle.

### 7.2. Triggering a Fire Simulation
1.  Hold the `Alt` key locally.
2.  Move cursor over any **Smoke Detector**.
3.  **Click** to stimulate the sensor.
4.  **Observation**: Siren sounds, Sprinklers activate.

### 7.3. Testing Remote Access
1.  Disconnect the link between **Home Gateway** and **ISP Cloud**.
2.  Observe that the **Smartphone** (via Cell Tower) loses control.
3.  Observe that **Fire Sprinklers** STILL work (Fail-Safe).

---

## 8. Contributors & Team

| Member | Role | GitHub Profile |
| :---: | :---: | :---: |
| **Abdelhamid** | Project Lead | [@Abdelhamid108](https://github.com/Abdelhamid108) |
| **Marwan** | Automation | [@marwan779](https://github.com/marwan779) |
| **Fady Ashraf** | Sensors | [fady1559](https://github.com/fady1559) |
| **Ahmed Kandil** | Design | [@Ahmed-Kandil11](https://github.com/Ahmed-Kandil11) |
| **Nadin Hisham** | Testing | [@nadin54](https://github.com/nadin54) |

---
_Project created for the Wireless Communication Course_
