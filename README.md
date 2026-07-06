# Multi-Peripheral STM32 & ESP32 Dual-MCU Controller Board

This repository contains the complete hardware design for an industrial-grade, multi-layer development platform utilizing a **Dual-MCU Architecture (STM32F4 + ESP32)**. Designed hierarchically using **Altium Designer**, this board serves as a robust gateway and controller capable of high-speed industrial routing, sensor data logging, and wireless bridging.

<!-- 📸 Master Sheet Schematic Render -->
<!-- امسح السطر التالي وضع مكانه لقطة الشاشة الخاصة بالـ Master Sheet بسحبها وإفلاتها هنا -->
<img width="1000" alt="Hierarchical Master Sheet Schematic" src="<img width="1236" height="756" alt="image" src="https://github.com/user-attachments/assets/3139ca4b-b365-42aa-8e68-deb0d8017a18" />
" />

---

## 🧠 System Architecture Overview

The board splits computational and connectivity workloads between two powerhouses via a dedicated **UART Communication Bridge**:
1. **ESP32 Core Subsystem:** Acts as the wireless transceiver and localized sensor hub, managing low-power sensor networks and state telemetry.
2. **STM32F4 Subsystem:** Serves as the main heavy-duty industrial controller, handling hardware-level timing, high-speed external storage, and industrial communication buses (Ethernet, CAN, RS485).

---

## 🔌 Detailed Block & Interface Breakdown

Based on the hierarchical schematic layout, the system integrates the following specialized modules:

### 1. Central Controllers & Inter-MCU Communication
* **STM32F4 High-Performance Core:** Manages the heavy protocol stacks and critical subsystems.
* **ESP32 Connectivity Core:** Handles peripheral polling and native wireless capabilities.
* **Cross-MCU Bridge:** Direct hardware UART (`TX/RX` cross-routing) enables low-latency inter-processor command communication.

### 2. Industrial Communication Interfaces (Managed by STM32)
* **10/100 Mbps Ethernet Module:** Fully broken out via an **RMII (Reduced Media Independent Interface)** using essential lines (`PA1`, `TX_EN`, `TXD_0`, `TXD_1`, `RXD_0`, `RXD_1`, `MDC`, `MDIO`, `CRS/DV`, `RESET_N`) for network connectivity.
* **CAN Bus Module:** Equipped with a standard transceiver connection (`CAN_TX`, `CAN_RX`) and hardware standby mode configuration (`STBY`) for automotive and automotive automation networking.
* **RS485 Industrial Serial:** Features differential serial communication capabilities via standard `TX_1` and `RX_1` lines, coupled with a dedicated direction gating control pin (`PD7`) to switch seamlessly between transmission and reception modes.

### 3. Sensor Arrays & Hardware Interfaces (Managed by ESP32)
* **Multi-Axis Accelerometer:** Interfaced using high-speed **SPI** protocol (`SDO`, `SDI`, `CLK_ACC`, `CS`) alongside two hardware interrupt lines (`INT1`, `INT2`) for instant motion/vibration wake-up tracking.
* **Humidity + LDR Sensor Suite:** Utilizes a shared hardware **I2C Bus** (`SDA`, `SCL`) for digital environmental analysis, backed by a dedicated analog line (`LDR_SENSE`) for ambient light intensity calculations.

### 4. Storage & Actuation Subsystems
* **External Storage Matrix:** SPI-driven external memory module (`CS_memory`, `CLK_memory`, `MOSI`, `MISO`) connected to the STM32 for localized data logging, firmware backups, and heavy caching.
* **DC Motor Driving Stage:** Dedicated hardware interface controlled via the STM32 (`Motor` pin) tied to a high-voltage input channel.
* **Analog Voltage Monitoring:** Built-in hardware protection network feeding into the STM32 (`Voltage Sense`) to dynamically track power rail health.

### 5. Multi-Rail Power Management System
* **Input Isolation:** Features a specialized `+12V_Protect` line ensuring robust surge safety before supplying power to the actuation circuits.
* **Onboard Regulation:** Efficient multi-rail step-down topology generating stable low-ripple **+5V** and **3V3** outputs to safely feed the digital logic cores and sensitive sensor electronics.

---

## 🛠️ Repository Content Structure
* 📂 **Hardware-Design/**: Hierarchical Altium Designer multi-sheet project files (Schematics, Netlists, Layer Stackup definitions).
* 📂 **Manufacturing-Outputs/**: Production-ready Gerber X2 profiles, Drill files, Pick-and-Place matrices, and Bill of Materials (BOM).
* 📂 **Hardware-Documentation/**: High-resolution PDF versions of individual schematics sub-sheets and 3D top/bottom PCB renders.
