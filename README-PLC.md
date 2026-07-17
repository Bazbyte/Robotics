# 1. 🚗 Automated Garage Door Control System (PLC)

**Status:** Completed | **Category:** Industrial Automation & Systems Integration | **Tech Stack:** PLC Ladder Logic, Sensor Interlocking, Counter/Timer Logic
****

### **📝 Overview**

Engineered an automated control system for a residential or commercial garage door utilizing a Programmable Logic Controller (PLC). The system integrates intelligent vehicle detection, sequential control logic, and strict physical safety interlocks to manage automated entry/exit sequences alongside manual user overrides.

![Garage Door Control.png](PLC/Garage_Door_Control.png)

**🛠 Key Features**

- **Intelligent Vehicle Authentication (Pulse-Count Trigger):** Programmed advanced sensor telemetry via an exterior light switch sensor (`Sen 1`). The system detects a unique "keyless" credential—flashing high beams exactly 3 times within a rolling 5-second window—to initiate the door-open sequence.
- **Dual-Direction Safety Interlocking:** Designed robust mutual exclusion logic (electrical/software interlocks) ensuring the Door Opening Contactor and Door Closing Contactor can never be energized simultaneously, mitigating the risk of motor burnout or mechanical failure.
- **Automated Close-on-Entry Sequence:** Utilized an interior vehicle detection sensor (`Sen 2`) to identify when a vehicle has safely cleared the threshold, automatically triggering the closing contactor until the lower limit switch is engaged.
- **Manual Operator Stations:** Integrated momentary tactile control interface pushbuttons (Open, Close, and Emergency Stop) to allow manual operational override for users outside the vehicle.

### **💻 Technical Skills**

- **Advanced Logic Design:** High-frequency pulse counting, time-window constraints, and latching/unlatching control circuits.
- **System Protection:** Interlocking state machines and limit-switch end-travel isolation.
- **Hardware Mapping:** Integration of photoelectric retroreflective sensors, mechanical limit switches, and motor contactors.

### **📂 System Component & I/O MappingTag NameDevice TypeFunction**

| **Tag Name** | **Device Type** | **Function Description** |
| --- | --- | --- |
| `I_Upper_Limit` | Input (NC/NO Switch) | Detects fully open door state; cuts opening contactor power |
| `I_Lower_Limit` | Input (NC/NO Switch) | Detects fully closed door state; cuts closing contactor power |
| `I_Sen_1` | Input (Photoelectric) | External light sensor; counts headlight pulses (3 pulses / 5s) |
| `I_Sen_2` | Input (Proximity/Loop) | Internal vehicle detection sensor; triggers auto-close |
| `I_PB_Open` | Input (Momentary NO) | External green pushbutton; initiates manual opening sequence |
| `I_PB_Close` | Input (Momentary NO) | External blue pushbutton; initiates manual closing sequence |
| `O_Contactor_Open` | Output (Actuator) | Drives motor upward (Interlocked against Closing output) |
| `O_Contactor_Close` | Output (Actuator) | Drives motor downward (Interlocked against Opening output) |

![Garage Door Control_Code_ZC.png](PLC/Garage_Door_Control_Code_ZC.png)

### 💡 Engineering Approach

- **Time-Bounded Pulse Counting:** The headlight trigger utilizes a fast-acting upward counter coupled with a non-retentive off-delay timer (5s). If 3 pulses are not recorded within the time envelope, the counter resets automatically, filtering out environmental noise or random light fluctuations.
- **Fail-Safe Interlocking Architecture:** To absolute-proof the motor contactors against cross-conduction, the software passes the activation coil of each direction through the Normally Closed (NC) auxiliary contacts/bits of the opposing direction.

### 📄 [**Click to View Ladder Logic & HMI Configuration (PDF)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/Garage%20Door%20Control_ZC.pdf)

### 📥 [**Click to Download PLC Source Archive (.pcwex)**](https://github.com/Bazbyte/Robotics/blob/977ecc580e18a022490b780ad2c1edc0b48fc8f6/PLC/GarageDoor_ZC.pcwex)

# 2. 🌡️ Automated Temperature Control System (PLC)

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

![Temperature Control_LDCode_ZC.png](PLC/Temperature_Control_LDCode_ZC.png)

### 💡 Engineering Approach

- **Hysteresis Implementation:** By creating a "gap" between activation and deactivation temperatures, the system preserves actuator longevity by avoiding unnecessary rapid cycling near the threshold.
- **Diagnostic Efficiency:** Utilized a single digital output channel to signal multiple machine states (Normal vs. Fault) by leveraging time-frequency modulation rather than consuming additional I/O hardware.

### 📄 [**Click to View Ladder Logic & HMI Configuration (PDF)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/Temperature%20Control_ZC.pdf)

### 📥 [**Click to Download PLC Source Archive (.pcwex)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/TemperatureControl_ZC.pcwex)
