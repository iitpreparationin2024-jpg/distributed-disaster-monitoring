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

```text
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
