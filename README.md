🌐 Distributed Disaster Monitoring Network

Self-Verifying • Fault-Tolerant • Edge-Intelligent • Resilient

A distributed, self-verifying disaster monitoring system using ESP32 sensor nodes, ESP-MESH, Raspberry Pi edge intelligence, cooperative 2-of-3 verification, resilient warning mechanisms, and disaster-flow analysis.

<p align="center">

🚨 SIH 2026 PROJECT

Distributed Self-Verifying Disaster Monitoring Network

Sense → Verify → Decide → Warn → Predict → Synchronize

</p>

🚦 Project Status

🟡 EARLY DEVELOPMENT / SIMULATION STAGE

This project is being developed step-by-step for SIH 2026.

The repository documents the proposed system architecture, verification approach, communication strategy, fault-tolerance approach, simulation plan, testing strategy, and development roadmap.

The physical multi-node prototype and field validation are not completed yet.

Status Legend

Status

Meaning

🟢 IMPLEMENTED

Working software/component

🟡 SIMULATED

Software or conceptual simulation

🔵 PLANNED

Designed but not implemented

🔴 NOT VALIDATED

Implemented but real-world testing is pending

📌 1. Project Overview

Disaster-monitoring systems may face several practical challenges:

Individual sensor failure

False alarms

Communication-link failure

Internet/network outage

Node failure

Delayed centralized decision-making

Difficulty identifying disaster propagation

Loss of monitoring coverage in remote areas

Our proposed system addresses these challenges using a distributed and self-verifying architecture.

Instead of relying on a single sensor or continuously available internet connectivity, nearby sensor nodes cooperate to verify abnormal conditions.

The proposed system follows:

SENSE
   ↓
VERIFY
   ↓
DECIDE LOCALLY
   ↓
WARN
   ↓
ANALYZE PROPAGATION
   ↓
SYNCHRONIZE

🎯 2. Problem Statement

A disaster-monitoring system should continue providing useful local decisions even when:

A sensor produces an abnormal reading

A sensor becomes unavailable

An ESP32 node becomes unavailable

A mesh communication path fails

Internet connectivity is lost

Multiple monitoring zones are affected

Central-server communication is temporarily unavailable

The proposed architecture therefore focuses on:

Distributed sensing

Cooperative event verification

Edge-based processing

Fault detection

Local warning

Store-and-forward communication

Disaster-flow analysis

💡 3. Proposed Solution

ESP32 SENSOR NODES
        ↓
ESP-MESH
        ↓
COOPERATIVE VERIFICATION
        ↓
RASPBERRY PI EDGE GATEWAY
        ↓
LOCAL WARNING
        ↓
DISASTER FLOW ANALYSIS
        ↓
CENTRAL DASHBOARD

Each ESP32 node collects environmental measurements.

When a node detects an abnormal condition, neighboring nodes can be requested to provide fresh measurements.

The system uses 2-of-3 cooperative verification to distinguish an isolated abnormal reading from an event supported by multiple nearby nodes.

The Raspberry Pi gateway performs local processing before forwarding information to the central monitoring system.

# 🔄 4. Core Workflow

The system follows a sequential **Sense → Verify → Decide → Warn → Analyze → Synchronize** workflow.

```text
┌──────────────────────────────┐
│            SENSE             │
│      ESP32 Sensor Nodes      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      LOCAL SENSOR CHECK      │
│   Range / Health Validation  │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     ABNORMALITY DETECTED     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   NEIGHBOR VERIFICATION      │
│      ESP-MESH Network        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   2-OF-3 COOPERATIVE         │
│         DECISION             │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    RASPBERRY PI EDGE         │
│        PROCESSING            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       LOCAL WARNING          │
│    Siren / SMS / Voice      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      DISASTER FLOW           │
│          ANALYSIS            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     CENTRAL DASHBOARD        │
│   / STORE-AND-FORWARD        │
└──────────────────────────────┘
```

🤝 5. Cooperative 2-of-3 Verification

When one node detects an abnormal condition, nearby nodes can be asked to verify the event.

Example

Node A → ABNORMAL
Node B → ABNORMAL
Node C → NORMAL

       ↓

2 / 3 NODES AGREE

       ↓

CONFIRMED EVENT

Verification Logic

Node A

Node B

Node C

System State

Normal

Normal

Normal

🟢 NORMAL

Alert

Normal

Normal

🟡 SUSPECT / VERIFY

Alert

Alert

Normal

🟠 CONFIRMED

Alert

Alert

Alert

🔴 CRITICAL

Extreme sensor thresholds may generate a pre-alert while cooperative verification continues.

Purpose

Reduce isolated sensor false alarms

Verify abnormal conditions using neighboring nodes

Improve reliability of event detection

Continue verification when one node becomes unavailable

Support distributed decision-making

🏗️ 6. Distributed System Architecture

                    ┌─────────────────────────┐
                    │     SENSOR ENVIRONMENT  │
                    │                         │
                    │ Water • Smoke • Temp    │
                    │ Humidity • Pressure     │
                    │ Vibration • Other Data  │
                    └────────────┬────────────┘
                                 │
                                 ▼
              ┌──────────────────────────────────┐
              │         ESP32 SENSOR GRID        │
              │                                  │
              │  Node A     Node B     Node C    │
              └────────────────┬─────────────────┘
                               │
                               ▼
                    ┌────────────────────┐
                    │      ESP-MESH      │
                    │ Node-to-Node       │
                    │ Communication      │
                    └─────────┬──────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ COOPERATIVE VERIFICATION│
                 │                         │
                 │      2-of-3 LOGIC       │
                 └───────────┬─────────────┘
                             │
                             ▼
                 ┌─────────────────────────┐
                 │ RASPBERRY PI EDGE       │
                 │ GATEWAY                 │
                 │                         │
                 │ • Packet Validation     │
                 │ • Deduplication         │
                 │ • Sensor Fusion         │
                 │ • Event Decision        │
                 │ • Fault Detection       │
                 │ • Warning Engine        │
                 └───────────┬─────────────┘
                             │
                  ┌──────────┴──────────┐
                  ▼                     ▼
        ┌─────────────────┐   ┌─────────────────┐
        │ LOCAL WARNING   │   │ CENTRAL SERVER  │
        │ Siren / SMS /   │   │ Dashboard /     │
        │ Voice           │   │ Analytics       │
        └─────────────────┘   └────────┬────────┘
                                       ▼
                              ┌──────────────────┐
                              │ DISASTER FLOW    │
                              │ ANALYSIS         │
                              └──────────────────┘

🧩 7. System Layers

Layer 1 — Sensor Layer

ESP32 nodes collect:

Water level

Temperature

Humidity

Smoke/gas

Pressure

Vibration

Layer 2 — Communication Layer

ESP-MESH is planned for communication between nearby ESP32 nodes.

Layer 3 — Cooperative Verification

Neighboring nodes provide additional measurements to verify abnormal conditions.

Layer 4 — Edge Intelligence

The Raspberry Pi gateway is intended to perform:

Packet validation

Deduplication

Sensor fusion

Event classification

Fault detection

Warning decisions

Local storage

Store-and-forward processing

Layer 5 — Warning and Monitoring

Local warning

Central dashboard

Event monitoring

Disaster-flow visualization

Infrastructure health monitoring

🚨 8. Emergency Communication

Emergency traffic receives higher priority than normal telemetry.

P0 → EMERGENCY EVENT
P1 → VERIFICATION
P2 → NODE HEALTH
P3 → NORMAL TELEMETRY
P4 → BULK / HISTORICAL DATA

Emergency packets are intended to bypass normal telemetry queues.

Reliability Mechanisms

Short emergency packets

Timestamping

Sequence numbers

ACK / retry

Randomized backoff

Priority queues

Duplicate suppression

Alternate mesh routes

Local buffering

Store-and-forward

🌐 9. Internet-Outage Operation

The central server is not the emergency path.

ESP32 MESH
    ↓
RASPBERRY PI
    ↓
LOCAL DECISION
    ↓
LOCAL WARNING

If internet connectivity is unavailable:

Local monitoring continues.

Cooperative verification continues.

Local warning decisions continue.

Events are stored locally.

Data is synchronized when connectivity returns.

EVENT GENERATED
      ↓
LOCAL STORAGE
      ↓
INTERNET OUTAGE
      ↓
LOCAL OPERATION
      ↓
CONNECTION RESTORED
      ↓
DATA SYNCHRONIZATION

🌊 10. Disaster Flow Analysis

The proposed system can analyze apparent event propagation using:

Node locations

Event timestamps

Node activation order

Sensor gradients

Rate of change

Network topology

Terrain/context information

Weather information where available

Example:

ZONE A
  ↓
ZONE B
  ↓
ZONE C
  ↓
ZONE D

Potential outputs:

Direction of propagation

Next potentially affected zone

Relative propagation speed

Possible arrival time when sufficient validated data is available

⚠️ Disaster-flow predictions require testing and validation before real-world use.

🔄 11. Node and Event States

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

Additional state:

UNKNOWN

State

Meaning

🟢 NORMAL

No abnormal condition detected

🟡 SUSPECT

Initial abnormal reading detected

🟡 VERIFYING

Nearby nodes are checking the event

🟠 CONFIRMED

Cooperative verification supports the event

🔴 PROPAGATING

Event appears to be moving toward another zone

🔴 AFFECTED

Zone is currently affected

🔵 RECOVERING

Conditions are recovering

⚪ UNKNOWN

Reliable monitoring information is unavailable

🛡️ 12. Fault Tolerance

The architecture is designed to detect, isolate, and tolerate failures.

Failure

Planned Response

Sensor abnormal reading

Neighbor verification

Sensor failure

Node health monitoring

ESP32 node offline

Detect missing node

Mesh-link failure

Alternate route where available

Internet outage

Local operation + local storage

Duplicate packet

Duplicate suppression

Old packet

Timestamp / sequence validation

Multiple alerts

Event deduplication and escalation

Gateway issue

Local buffering and future redundancy

The system is designed for failure detection and graceful degradation, not an assumption of error-free operation.

🔔 13. Warning System

NORMAL
   ↓
WATCH
   ↓
WARNING
   ↓
CRITICAL

Additional state:

UNKNOWN

Planned warning mechanisms:

🔊 Local siren

📱 SMS

🔈 Voice alert

🖥️ Dashboard alert

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

🖥️ 14. Dashboard

The planned dashboard will provide:

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

🧪 15. Simulation and Technical Demonstration

Planned simulations include:

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

Any AI/3D demonstration will be clearly labeled as a simulation or conceptual technical demonstration and will not be presented as a physical prototype.

🔧 16. Planned Hardware Prototype

3 × ESP32 SENSOR NODES
          +
ENVIRONMENTAL SENSORS
          +
1 × RASPBERRY PI GATEWAY
          +
LOCAL WARNING DEVICE
          +
OPTIONAL CELLULAR / LTE

Possible sensors:

Water-level sensor

Temperature sensor

Humidity sensor

Smoke/gas sensor

Pressure sensor

Vibration sensor

Current Hardware Status

🔵 PLANNED

The physical multi-node prototype has not yet been fully built or validated.

No physical deployment results are claimed at this stage.

💻 17. Technology Stack

Hardware

ESP32

Raspberry Pi

Environmental sensors

Optional GPS / location module

Optional cellular / LTE modem

Local warning device

Communication

ESP-MESH

MQTT / HTTP

Wi-Fi

Optional cellular communication

Programming

C / C++

Python

Data Storage

Local database

Central database

Store-and-forward event storage

Dashboard

Web-based dashboard

Network monitoring

Event monitoring

Disaster-flow visualization

Data & Analysis

Sensor data processing

Cooperative verification

Multi-sensor data fusion

Event classification

Disaster-flow analysis

📁 18. Repository Structure

distributed-disaster-monitoring/
│
├── README.md
├── esp32/
│   ├── sensor-node/
│   ├── mesh/
│   ├── verification/
│   └── node-health/
├── raspberry-pi/
│   ├── gateway/
│   ├── packet-validation/
│   ├── deduplication/
│   ├── sensor-fusion/
│   ├── event-decision/
│   ├── fault-detection/
│   ├── warning-engine/
│   ├── store-and-forward/
│   └── disaster-flow/
├── server/
│   ├── backend/
│   ├── api/
│   ├── database/
│   └── analytics/
├── dashboard/
│   ├── frontend/
│   └── backend/
├── simulation/
│   ├── 2-of-3-verification/
│   ├── disaster-flow/
│   ├── internet-outage/
│   ├── sensor-failure/
│   └── mesh-failure/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── verification/
│   ├── communication/
│   └── failure-scenarios/
├── hardware/
│   ├── schematics/
│   ├── wiring/
│   ├── bill-of-materials.md
│   └── prototype-status.md
├── demo/
│   ├── screenshots/
│   ├── videos/
│   └── demo-script.md
└── docs/
    ├── architecture/
    ├── design/
    └── deployment/

Folders and components will be added as they are actually developed.

📊 19. Current Validation Status

Component

Status

Project architecture

🟢 DEFINED

Cooperative 2-of-3 logic

🔵 PLANNED

ESP32 firmware

🔵 PLANNED

ESP-MESH communication

🔵 PLANNED

Raspberry Pi gateway

🔵 PLANNED

Warning engine

🔵 PLANNED

Disaster-flow engine

🔵 PLANNED

Dashboard

🔵 PLANNED

Software simulation

🔵 PLANNED

Physical prototype

🔵 PLANNED

Field testing

🔴 NOT VALIDATED

This table will be updated as development progresses.

⚠️ 20. Current Limitations

The project is currently in the development stage.

The following require future implementation and validation:

Physical multi-node deployment

Real sensor measurements

Real ESP-MESH communication testing

Environmental interference testing

Remote-area connectivity testing

Gateway failover testing

Warning hardware testing

Disaster-flow validation using real events

Field deployment testing

No real-world performance figures are claimed until they are experimentally measured.

🚀 21. Development Roadmap

Phase 1 — Software Foundation

Implement 2-of-3 verification simulator

Implement event-state logic

Implement warning-state logic

Add unit tests

Phase 2 — Communication Simulation

Simulate ESP32 nodes

Simulate node-to-node communication

Simulate message priority

Simulate duplicate packets

Simulate stale packets

Simulate communication failure

Phase 3 — Raspberry Pi Edge Gateway

Develop gateway software

Implement packet validation

Implement deduplication

Implement sensor fusion

Implement event decision engine

Implement local warning engine

Implement local data storage

Phase 4 — Dashboard

Create backend API

Create database

Create network overview

Create event monitoring

Create disaster-flow visualization

Create infrastructure health monitoring

Phase 5 — ESP32 Prototype

Develop ESP32 sensor-node firmware

Connect sensors

Implement sensor health checks

Implement ESP-MESH communication

Implement cooperative verification

Test multiple nodes

Phase 6 — Failure Testing

Sensor failure test

Node failure test

Mesh-link failure test

Internet outage test

Duplicate packet test

Stale packet test

Store-and-forward test

Phase 7 — Disaster Flow

Implement event timeline

Track node activation order

Calculate propagation direction

Estimate relative propagation speed

Identify next potentially affected zone

Validate using simulated scenarios

Phase 8 — Physical Validation

Build multi-node ESP32 prototype

Connect Raspberry Pi gateway

Connect sensors

Test local warning

Test communication failures

Test internet outage

Document physical test results

🧾 22. Evidence and Validation Policy

This project clearly distinguishes between:

Category

Meaning

🟢 Implemented

Working component

🟡 Simulated

Software simulation

🟡 Conceptual

Proposed design / visual demonstration

🔵 Planned

Future development

🔴 Not Validated

Requires real-world testing

Only components that have actually been implemented and tested will be marked as IMPLEMENTED.

Simulation results will not be presented as physical hardware results.

Real-world performance claims will only be added after experimental validation.

📸 23. Future Project Evidence

As development progresses, this repository may contain:

Source code

Simulation results

Unit-test results

Integration-test results

Dashboard screenshots

Architecture diagrams

Hardware photographs

Circuit diagrams

Test videos

3D technical demonstration

Failure-test evidence

Prototype documentation

🌱 24. Sustainability and Scalability

The proposed architecture is intended to support incremental deployment.

1 ESP32 NODE
      ↓
LOCAL SENSOR ZONE
      ↓
MULTIPLE ESP32 NODES
      ↓
RASPBERRY PI GATEWAY
      ↓
MULTIPLE MONITORING ZONES
      ↓
REGIONAL NETWORK

Potential deployment environments include:

🌲 Forest regions

🌊 River and flood-prone areas

🛣️ Roads and villages

🏭 Industrial areas

Actual scalability and deployment performance will require experimental validation.

🧠 25. Key Design Principles

1. Distributed Sensing

Do not depend on a single sensing point.

2. Cooperative Verification

Use neighboring nodes to verify abnormal conditions.

3. Edge-First Emergency Decisions

Keep critical warning decisions close to the sensing environment.

4. Graceful Degradation

The system should detect failures and continue with available resources where possible.

5. Store-and-Forward

Preserve event information during temporary connectivity loss.

6. Evidence-Based Development

Clearly distinguish between implemented, simulated, planned, and validated components.

7. Incremental Deployment

Build and validate the system layer-by-layer.

🎯 26. Project Goal

The goal is to develop and validate a distributed disaster-monitoring architecture that can:

Detect abnormal environmental conditions.

Verify events cooperatively using nearby nodes.

Continue local operation during internet outages.

Detect and handle component and communication failures.

Generate local emergency warnings.

Analyze disaster propagation.

Provide centralized monitoring when connectivity is available.

🏆 SIH 2026 PROJECT

Distributed Self-Verifying Disaster Monitoring Network

Sense → Verify → Decide → Warn → Predict → Synchronize

👨‍💻 Development Philosophy

Build incrementally. Test every layer. Document every result. Never present simulation as field validation.

📌 Repository Development Status

CONCEPT
   ↓
SOFTWARE SIMULATION
   ↓
TESTING
   ↓
EDGE SOFTWARE
   ↓
DASHBOARD
   ↓
ESP32 IMPLEMENTATION
   ↓
PHYSICAL PROTOTYPE
   ↓
FIELD VALIDATION

The project will move through these stages progressively.

📚 References and Research Areas

Technical references and research sources will be added as implementation progresses.

Planned research areas include:

ESP32 and ESP-MESH

Raspberry Pi edge computing

Wireless sensor networks

Cooperative sensing

Distributed verification

Multi-sensor data fusion

Edge computing for early warning

Fault-tolerant IoT networks

Disaster early-warning systems

Emergency communication

Disaster propagation modelling

📄 License

License information will be added after project development and team requirements are finalized.

<p align="center">

🚨 Distributed Disaster Monitoring Network

SIH 2026

Distributed • Self-Verifying • Edge-Intelligent • Resilient

</p>
