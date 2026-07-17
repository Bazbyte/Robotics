# 1. 🚗 Automated Garage Door Control System (PLC)

**Status:** Completed | **Category:** Industrial Automation & Systems Integration | **Tech Stack:** PLC Ladder Logic, Sensor Interlocking, Counter/Timer Logic
****

### **📝 Overview**

Engineered an automated control system for a residential or commercial garage door utilizing a Programmable Logic Controller (PLC). The system integrates intelligent vehicle detection, sequential control logic, and strict physical safety interlocks to manage automated entry/exit sequences alongside manual user overrides.

![Garage Door Control.png](Garage_Door_Control.png)

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

![Garage Door Control_Code_ZC.png](Garage_Door_Control_Code_ZC.png)

### 💡 Engineering Approach

- **Time-Bounded Pulse Counting:** The headlight trigger utilizes a fast-acting upward counter coupled with a non-retentive off-delay timer (5s). If 3 pulses are not recorded within the time envelope, the counter resets automatically, filtering out environmental noise or random light fluctuations.
- **Fail-Safe Interlocking Architecture:** To absolute-proof the motor contactors against cross-conduction, the software passes the activation coil of each direction through the Normally Closed (NC) auxiliary contacts/bits of the opposing direction.

### 📄 [**Click to View Ladder Logic & HMI Configuration (PDF)**](https://github.com/Bazbyte/Robotics/blob/main/PLC/Garage%20Door%20Control_ZC.pdf)

### 📥 [**Click to Download PLC Source Archive (.pcwex)**](https://github.com/Bazbyte/Robotics/blob/977ecc580e18a022490b780ad2c1edc0b48fc8f6/PLC/GarageDoor_ZC.pcwex)

2. 
