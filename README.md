# Edge-AI Based Adaptive LoRa Link Optimization

**A lightweight Edge-AI framework for adaptive Spreading Factor (SF) and Transmission Power (TP) optimization in LoRa end devices under dynamic channel conditions.**

## Overview

LoRa is widely used in Internet of Things (IoT) applications because of its long-range communication capabilities and low-power operation. However, changing channel conditions can affect packet delivery, communication reliability, latency, and energy consumption.

Conventional adaptive approaches may rely on network-side observations or predefined adaptation rules. This project investigates whether a lightweight machine learning model running locally on an ESP32-based LoRa end device can use recent communication feedback to adapt the Spreading Factor and transmission power.

The system will collect link-quality information, process recent packet history, and evaluate candidate SF and transmission-power settings. Its performance will be compared against a conventional baseline under controlled and dynamic channel conditions.

The project focuses on the practical trade-offs between communication performance, energy consumption, inference cost, and embedded resource constraints.

## Objectives

- Develop a lightweight machine learning pipeline for adaptive LoRa link configuration.
- Use RSSI, SNR, packet delivery history, and retry information as input features.
- Prepare the model for local inference on an ESP32-class microcontroller.
- Investigate adaptive Spreading Factor and transmission-power selection.
- Compare Edge-AI adaptation against a conventional baseline.
- Evaluate packet delivery ratio, packet loss, latency, energy consumption, and adaptation time.
- Characterize model size, memory requirements, and inference latency.
- Validate the approach using data collected from the project's own hardware testbed.

## Proposed Architecture

```text
        Dynamic Channel Conditions
                   |
                   v
          LoRa End Device
          ESP32 + SX1278
                   |
                   v
        Link-Metric Collection
        - RSSI and SNR
        - Packet success/failure
        - Retry and packet history
                   |
                   v
         Lightweight Edge-AI
                   |
                   v
        Adaptive Configuration
        - Spreading Factor
        - Transmission Power
                   |
                   v
           LoRa Transmission
                   |
                   v
            Gateway / Receiver
                   |
                   v
        ACK and Packet Feedback
                   |
                   +------> Updated Link History
```

*This is the proposed architecture. On-device integration and complete end-to-end hardware validation remain future implementation stages.*

## Key Features

- **Edge inference:** Designed to run locally on a resource-constrained end device.
- **Link-aware adaptation:** Uses recent communication observations to inform configuration decisions.
- **Lightweight ML:** Evaluates compact candidate models suitable for embedded deployment.
- **Feedback-driven operation:** Uses packet outcomes and retry history to update the runtime feature window.
- **Performance benchmarking:** Compares adaptive operation against a conventional baseline.
- **Reproducible data collection:** Uses a defined logging schema, experiment configuration, and validation workflow.
- **Resource analysis:** Examines model size, memory requirements, inference time, and deployment constraints.

## Hardware Platform

| Component | Purpose |
|---|---|
| ESP32-WROOM development boards × 2 | Transmitter and receiver-side processing |
| SX1278 LoRa modules × 2 | LoRa radio communication |
| DHT22 sensor × 1 | Environmental measurements for experiment context |
| INA219 current and power monitor × 1 | Power and energy measurement where the measurement setup supports it |
| Gateway/receiver setup | Packet reception and feedback logging |

The hardware list describes the planned testbed. Wiring, radio configuration, measurement accuracy, and the final experimental setup must be verified during implementation.

The SX1278 modules planned for this project operate in the 433 MHz band. Applicable Indian frequency-allocation, equipment, and operating requirements must be checked before transmitting.

## Machine Learning Approach

The project evaluates lightweight candidate models through a staged workflow:

1. **Data preparation:** Validate and preprocess communication logs.
2. **Feature engineering:** Build causal features from current link metrics and recent packet history.
3. **Model comparison:** Evaluate candidate classifiers using an appropriate training and validation procedure.
4. **Deployment preparation:** Export the selected candidate, preserve preprocessing consistency, and investigate quantization where appropriate.
5. **On-device evaluation:** Measure inference cost and communication performance after integration with the actual hardware.
6. **Final assessment:** Select a model and adaptation policy using real-data and hardware evidence.

Candidate models include Decision Tree, Logistic Regression, and Random Forest approaches. The final model will be selected only after suitable experimental evidence is available.

## Evaluation Metrics

| Metric | Purpose |
|---|---|
| Packet Delivery Ratio (PDR) | Measures successful packet delivery |
| Packet Loss Rate | Measures unsuccessful packet delivery |
| RSSI and SNR | Characterize received link quality |
| End-to-end latency | Measures communication delay |
| Energy consumption | Estimates or measures communication energy |
| Adaptation time | Measures how quickly the policy responds to changing conditions |
| Model size | Determines storage requirements |
| RAM usage | Evaluates embedded memory requirements |
| Inference latency | Measures the computational cost of a prediction |

Comparisons will use controlled experimental conditions wherever possible. Measured, estimated, and simulated or synthetic values will be identified separately.

## Software and Tools

- **Embedded platform:** ESP32
- **Radio module:** SX1278
- **Programming:** Python for data processing and model development; embedded C/C++ for firmware integration
- **Machine learning:** Scikit-learn-based candidate models, subject to the existing implementation
- **Data pipeline:** Structured logging, schema validation, preprocessing, and experiment metadata
- **Version control:** Git and GitHub

Specific tools and deployment libraries may change as model-export and firmware requirements are established.

## Project Status

**Current stage:
