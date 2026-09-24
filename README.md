# Distributed Disaster Monitoring Network

A distributed, self-verifying disaster monitoring system using ESP32 sensor nodes, ESP-MESH, Raspberry Pi edge intelligence, cooperative 2-of-3 verification, resilient warning, and disaster-flow analysis.

## Project Status

🟡 **Early Development / Simulation Stage**

This repository is being developed step-by-step for SIH 2026.

The physical multi-node prototype and field validation are not completed yet.

### Status Legend

- 🟢 IMPLEMENTED — Working software/component
- 🟡 SIMULATED — Software or conceptual simulation
- 🔵 PLANNED — Designed but not implemented
- 🔴 NOT VALIDATED — Implemented but real-world testing is pending

---

# 1. Problem

Disaster monitoring systems can face challenges such as:

- Individual sensor failure
- False alarms
- Communication link failure
- Internet/network outage
- Node failure
- Delayed centralized decision-making
- Difficulty identifying how a disaster is propagating
- Loss of monitoring coverage in remote areas

A reliable monitoring system should continue operating even when individual components or communication paths fail.

---

# 2. Proposed Solution

We propose a distributed disaster-monitoring network consisting of:

**ESP32 sensor nodes → ESP-MESH → Raspberry Pi edge gateway → Warning system / Central monitoring**

Each ESP32 node collects environmental information and communicates with nearby nodes.

When one node detects an abnormal condition, nearby nodes are requested to verify the event.

The system uses cooperative **2-of-3 verification** before treating an abnormal event as confirmed.

The Raspberry Pi gateway performs local validation, event processing, warning decisions, and disaster-flow analysis.

---

# 3. Core Workflow


SENSE
  ↓
LOCAL SENSOR CHECK
  ↓
ABNORMALITY DETECTED
  ↓
NEIGHBOR VERIFICATION
  ↓
2-OF-3 COOPERATIVE DECISION
  ↓
RASPBERRY PI EDGE PROCESSING
  ↓
LOCAL WARNING
  ↓
DISASTER FLOW ANALYSIS
  ↓
CENTRAL DASHBOARD / STORE-AND-FORWARD

# 4. Cooperative 2-of-3 Verification

The system uses nearby sensor nodes to verify abnormal events.

When one node detects an abnormal condition, it requests fresh measurements from neighboring nodes.

The system uses a **2-of-3 cooperative verification approach** before treating an abnormal event as confirmed.

## Example


Node A → Abnormal
Node B → Abnormal
Node C → Normal

        ↓

2 / 3 Nodes Agree

        ↓

CONFIRMED EVENT


#5. Distributed System Architecture
┌──────────────────────────────────────────┐
│             ESP32 SENSOR NODES           │
│                                          │
│ Water • Temperature • Smoke              │
│ Humidity • Pressure • Vibration          │
└────────────────────┬─────────────────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │      ESP-MESH       │
          │                     │
          │ Cooperative         │
          │ Communication       │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ RASPBERRY PI        │
          │ EDGE GATEWAY        │
          │                     │
          │ Packet Validation   │
          │ Deduplication       │
          │ Sensor Fusion       │
          │ Event Decision      │
          │ Fault Detection     │
          │ Warning Engine      │
          └──────────┬──────────┘
                     │
              ┌──────┴──────┐
              ▼             ▼
       LOCAL WARNING   CENTRAL SERVER
              │             │
       Siren / SMS       Dashboard
       / Voice           Analytics
              │             │
              └──────┬──────┘
                     ▼
              DISASTER FLOW
                 ANALYSIS
Main System Layers
Layer 1 — Sensor Layer

ESP32 nodes collect environmental measurements such as:

Water level
Temperature
Humidity
Smoke/gas
Pressure
Vibration
Layer 2 — Communication Layer

ESP-MESH enables communication between nearby ESP32 nodes.

Layer 3 — Cooperative Verification Layer

Neighboring nodes provide additional measurements to verify abnormal events.

Layer 4 — Edge Intelligence Layer

The Raspberry Pi performs:

Packet validation
Deduplication
Sensor fusion
Event classification
Fault detection
Warning decisions
Layer 5 — Warning and Monitoring Layer

The system provides:

Local warning
Central dashboard
Event monitoring
Disaster-flow visualization

#6. Emergency Communication

Emergency traffic is prioritized over normal telemetry.

Packet Priority
P0 → Emergency Event
P1 → Verification
P2 → Node Health
P3 → Normal Telemetry
P4 → Bulk / Historical Data

Emergency packets should bypass normal telemetry queues.

Communication Reliability Mechanisms

The system will investigate:

Short emergency packets
Timestamping
Sequence numbers
ACK / retry
Randomized backoff
Priority queues
Duplicate suppression
Alternate mesh routes
Local buffering
Store-and-forward communication
Example Emergency Flow
Normal Sensor Data
        ↓
Emergency Condition Detected
        ↓
Emergency Packet Generated
        ↓
Priority Queue
        ↓
Neighbor Verification
        ↓
Edge Gateway
        ↓
Local Warning
#7. Internet-Outage Operation

The central server is not the emergency path.

The intended emergency path is:

ESP32 Mesh
     ↓
Raspberry Pi
     ↓
Local Decision
     ↓
Local Warning

If internet connectivity is unavailable:

Local monitoring continues.
Cooperative verification continues.
Local warning decisions continue.
Events are stored locally.
Data is synchronized after connectivity returns.
Store-and-Forward
NORMAL CONNECTION
       ↓
EVENT GENERATED
       ↓
LOCAL STORAGE
       ↓
INTERNET OUTAGE
       ↓
LOCAL OPERATION CONTINUES
       ↓
CONNECTION RESTORED
       ↓
STORED DATA SYNCHRONIZED

This behaviour will be validated through simulation and later hardware testing.

#8. Disaster Flow Analysis

The system is intended to estimate disaster propagation using information such as:

Node locations
Event timestamps
Node activation order
Sensor gradients
Rate of change
Network topology
Terrain/context information
Weather information where available
Example
Zone A
  ↓
Zone B
  ↓
Zone C
  ↓
Zone D

The system can then estimate:

Direction of propagation
Next potentially affected zone
Relative propagation speed
Possible arrival time when sufficient validated data is available
Event Sequence
Node A Activated
      ↓
Node B Activated
      ↓
Node C Activated
      ↓
Node D Activated

The system can use the activation sequence and timestamps to analyze the apparent direction of propagation.

These capabilities require testing and validation before real-world use.

#9. Node and Event States

Possible node/event states include:

NORMAL
   ↓
SUSPECT
   ↓
VERIFYING
   ↓
CONFIRMED
   ↓
PROPAGATING
   ↓
AFFECTED
   ↓
PASSED / RECOVERING

An additional state may be used when monitoring coverage is uncertain:

UNKNOWN
State Meaning
NORMAL — No abnormal condition detected
SUSPECT — Initial abnormal reading detected
VERIFYING — Nearby nodes are checking the event
CONFIRMED — Cooperative verification supports the event
PROPAGATING — Event appears to be moving toward another zone
AFFECTED — Zone is currently affected
PASSED / RECOVERING — Event has moved away or conditions are recovering
UNKNOWN — Reliable monitoring information is unavailable
#10. Fault Tolerance

The system is designed to detect, isolate, and tolerate failures such as:

Sensor failure
ESP32 node failure
Mesh-link failure
Internet outage
Duplicate packets
Stale packets
Temporary communication loss
Gateway problems
Failure Handling Approach
Failure	Planned Response
Sensor abnormal reading	Neighbor verification
Sensor failure	Node health monitoring
ESP32 node offline	Detect missing node
Mesh link failure	Alternate communication route where available
Internet outage	Local operation + local storage
Duplicate packet	Duplicate suppression
Old packet	Timestamp / sequence validation
Multiple alerts	Event deduplication and escalation
Gateway issue	Local buffering and future redundancy

The project will include dedicated failure simulations and tests.

#11. Warning System

The warning engine is planned around the following states:

NORMAL
   ↓
WATCH
   ↓
WARNING
   ↓
CRITICAL

An additional state can represent loss of reliable monitoring coverage:

UNKNOWN
Planned Warning Mechanisms

Critical events may trigger:

Local siren
SMS
Voice alert
Dashboard alert
Warning Flow
SENSOR EVENT
     ↓
COOPERATIVE VERIFICATION
     ↓
EDGE DECISION
     ↓
SEVERITY CLASSIFICATION
     ↓
WATCH / WARNING / CRITICAL
     ↓
LOCAL ALERT
     ↓
CENTRAL DASHBOARD

Actual hardware alerting will be validated during prototype development.

#12. Dashboard

The planned dashboard will provide several monitoring views.

Network Overview
Node status
Connectivity
Sensor health
Gateway status
Monitoring coverage
Event Monitoring
Active events
Verification status
Event severity
Timestamp
Event source
Number of verifying nodes
Disaster Flow
Activated zones
Propagation direction
Next potentially affected zone
Historical event sequence
Event timeline
Infrastructure Health
Node failures
Communication failures
Internet connectivity
Gateway status
Stored unsynchronized events
#13. Simulation and Demonstration

The project will include software simulations for:

2-of-3 cooperative verification
Sensor failure
Node failure
Mesh-link failure
Internet outage
Store-and-forward recovery
Duplicate event suppression
Stale packet rejection
Warning-state transitions
Disaster propagation
3D / AI Technical Demonstration

A 3D/AI technical demonstration may be created to visually demonstrate the proposed architecture.

The demonstration may show:

SENSE
  ↓
VERIFY
  ↓
2/3 CONFIRMED
  ↓
EDGE DECISION
  ↓
WARNING
  ↓
DISASTER FLOW
  ↓
INTERNET OUTAGE
  ↓
LOCAL OPERATION
  ↓
CONNECTION RESTORED
  ↓
DATA SYNCHRONIZATION

Any simulated or conceptual demonstration will be clearly identified as a simulation and will not be presented as a physical prototype.

#14. Planned Hardware Prototype

Initial prototype plan:

3 × ESP32 Sensor Nodes
        +
Environmental Sensors
        +
1 × Raspberry Pi Gateway
        +
Local Warning Device
        +
Optional Cellular / LTE Communication
Possible Sensors

Depending on the selected disaster scenario, the prototype may use:

Water-level sensor
Temperature sensor
Humidity sensor
Smoke/gas sensor
Pressure sensor
Vibration sensor

The final sensor configuration will depend on the selected deployment scenario.

Prototype Status

The physical multi-node prototype is currently planned and has not yet been fully validated.

No physical deployment results are claimed at this stage.

#15. Technology Stack

Hardware:
ESP32
Raspberry Pi
Environmental sensors
Optional GPS / location module
Optional cellular / LTE modem
Local warning device

Communication:
ESP-MESH
MQTT / HTTP
Wi-Fi
Optional cellular communication

Programming:
C / C++
Python
Data Storage
Local database
Central database
Store-and-forward event storage

Dashboard:
Web-based dashboard
Network monitoring
Event monitoring
Disaster-flow visualization

Data and Analysis:
Sensor data processing
Cooperative verification
Multi-sensor data fusion
Event classification
Disaster-flow analysis
