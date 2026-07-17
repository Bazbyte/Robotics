# 🌡️ Automated Temperature Control System (PLC)

**Status:** Completed | **Category:** Industrial Automation | **Tech Stack:** PLC Ladder Logic, Analog Sensor Integration

### 📝 Overview

Developed a robust Programmable Logic Controller (PLC) application designed to monitor ambient conditions and execute automated temperature regulation. The system manages dual-stage climate control via a closed-loop feedback mechanism, integrating analog sensor scaling, digital output control, and an intelligent, multi-state fault detection and alarm system.

### 🛠 Key Features

- **Analog Data Scaling:** Processed raw analog signals from a temperature sensor into calibrated engineering units (°C).
- **Dual-Stage Climate Control:** Implemented hysteresis logic to prevent actuator "chattering":
    - **Fan:** Activation at > 30°C | Deactivation at < 25°C.
    - **Heater:** Activation at < 15°C | Deactivation at > 20°C.
- **Intelligent Visual Telemetry:** Single-output visual warnings using PLC timers:
    - **Operational Status:** 2-second interval flash when active.
    - **Fault/Critical State:** 0.5-second fast flash when < 10°C or > 35°C.
- **Safety Interlocks:** Dedicated buzzer alarm output for critical temperature breach events.

### 💻 Technical Skills

- **Programming Logic:** Ladder Logic design, Hysteresis, Signal Scaling, Timer/Counter programming.
- **Diagnostic Design:** Fault detection logic and critical safety alarm systems.
- **Hardware Interaction:** Sensor integration, Relay control, Digital I/O management.

### 📂 Implementation Highlights

| Logic Type | Logic Condition | Actuator State |
| --- | --- | --- |
| **Cooling** | Temp > 30°C | ON |
| **Cooling** | Temp < 25°C | OFF |
| **Heating** | Temp < 15°C | ON |
| **Heating** | Temp > 20°C | OFF |
| **Alarm** | Temp < 10°C or > 35°C | High-Frequency Flash + Buzzer |

![Temperature Control_LDCode_ZC.png](Temperature_Control_LDCode_ZC.png)

### 💡 Engineering Approach

- **Hysteresis Implementation:** By creating a "gap" between activation and deactivation temperatures, the system preserves actuator longevity by avoiding unnecessary rapid cycling near the threshold.
- **Diagnostic Efficiency:** Utilized a single digital output channel to signal multiple machine states (Normal vs. Fault) by leveraging time-frequency modulation rather than consuming additional I/O hardware.

### 📄 [**Click to View Ladder Logic & HMI Configuration (PDF)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/Temperature%20Control_ZC.pdf)

### 📥 [**Click to Download PLC Source Archive (.pcwex)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/TemperatureControl_ZC.pcwex)