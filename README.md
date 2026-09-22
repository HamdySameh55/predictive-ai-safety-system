# Predictive AI — Personalized Human Safety Intelligence System

## Overview

The **Predictive AI — Personalized Human Safety Intelligence System** is a privacy-preserving safety monitoring system based on **Wi-Fi Channel State Information (CSI)**, multi-sensor data, and **Edge AI**.

The system aims to monitor human activities without requiring wearable devices or continuous visual surveillance. ESP32-based sensing nodes collect Wi-Fi CSI measurements, while an Edge Gateway performs signal preprocessing and AI inference locally.

The system focuses on detecting human activities, falls, behavioral anomalies, and post-event movement while learning an individual's normal activity patterns.

---

## Problem

Traditional safety-monitoring systems have several limitations:

* Wearable devices require continuous user compliance.
* Camera-based monitoring can introduce significant privacy concerns.
* Basic motion sensors provide limited contextual information.
* Rule-based systems may not capture changes in an individual's normal behavior.
* Many systems focus mainly on detecting an event after it occurs.

The proposed system addresses these limitations through device-free Wi-Fi sensing and local Edge AI processing.

---

## Proposed Solution

The system uses changes in Wi-Fi CSI caused by human movement as an ambient sensing mechanism.

### High-Level Pipeline

```text
ESP32 CSI Nodes
      ↓
CSI Acquisition
      ↓
Signal Preprocessing
      ↓
Feature Extraction
      ↓
Activity Recognition
      ↓
Temporal Analysis
      ↓
Anomaly / Fall Detection
      ↓
Confidence Estimation
      ↓
Safety Alert
```

The Edge Gateway performs the main processing pipeline locally to reduce dependence on cloud-based processing and minimize transmission of raw sensing information.

---

## Core Components

### ESP32 Sensing Nodes

ESP32-based nodes collect Wi-Fi CSI measurements and transmit the extracted CSI data to the Edge Gateway.

### Edge Intelligence Gateway

The Edge Gateway performs:

* Signal preprocessing
* Feature extraction
* Activity recognition
* Fall detection
* Behavioral anomaly detection
* Confidence estimation
* Post-event movement monitoring

The proposed gateway platform may use an embedded computing device such as an **NVIDIA Jetson Nano** or **Raspberry Pi 4**.

### AI Pipeline

The initial AI pipeline may investigate:

* A lightweight **1D-CNN** for movement-related feature extraction.
* A temporal model such as **LSTM, GRU, or a lightweight State Space Model** for analyzing temporal activity patterns.

The final model configuration will be selected experimentally based on signal quality and model performance.

---

## Key Capabilities

The initial prototype focuses on:

* Device-free human activity recognition
* Wi-Fi CSI signal acquisition
* CSI preprocessing and feature extraction
* Basic personalized behavioral modeling
* Fall detection
* Behavioral anomaly detection
* Confidence-aware predictions
* Post-event movement monitoring
* Local Edge AI inference
* Privacy-preserving dashboard
* Safety alert generation

The initial system will operate in a controlled **single-person environment**.

---

## Signal Processing Pipeline

The proposed preprocessing pipeline is:

```text
ESP32
  ↓
CSI
  ↓
Amplitude / Phase
  ↓
Hampel Filter
  ↓
Low-Pass Filter
  ↓
PCA
  ↓
1D-CNN
  ↓
Activity Recognition
```

The final preprocessing configuration will be selected experimentally.

---

## Personalized Behavioral Modeling

The system will learn representations of an individual's normal movement patterns.

Example:

```text
[Bed_Exit] → [Walk] → [Kitchen] → [Sitting]
```

New activity sequences can then be compared with the learned baseline to identify significant behavioral deviations.

---

## Privacy

The system follows a privacy-first design.

It does not depend on continuous video monitoring. Instead, the dashboard presents structured information such as:

```text
Status: Walking
Location: Living Room
Confidence: 92%
```

For potential critical events:

```text
Status: Possible Fall Detected
Confidence: 94%
Post-Event Movement: Low
Action: Safety Alert Generated
```

No visual image of the monitored individual is required by the proposed sensing pipeline.

---

## Repository Structure

```text
predictive-ai-safety-system/
│
├── contracts/
│   └── contracts.md
│
├── docs/
│   ├── architecture.md
│   ├── methodology.md
│   └── hardware.md
│
├── firmware/
│   └── README.md
│
├── gateway/
│   └── README.md
│
├── ml/
│   └── README.md
│
├── backend/
│   └── README.md
│
├── dashboard/
│   └── README.md
│
└── README.md
```

---

## Project Scope

The initial prototype focuses on developing and evaluating the core sensing and AI pipeline in a controlled single-person environment.

Advanced capabilities are considered future research directions rather than requirements of the initial prototype.

These include:

* Multi-resident CSI disentanglement
* Few-shot cross-environment calibration
* Federated learning
* Advanced explainability
* Generative data augmentation
* Advanced continuous-time modeling

---

## Project Status

**Current Phase:** Initial System Development

The project is currently being organized into hardware, firmware, gateway, machine learning, backend, dashboard, and documentation components.
