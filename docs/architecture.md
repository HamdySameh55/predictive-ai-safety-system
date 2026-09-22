
# System Architecture

## 1. Overview

The Predictive AI — Personalized Human Safety Intelligence System uses Wi-Fi Channel State Information (CSI), Edge AI, and privacy-preserving sensing to monitor human activity without requiring wearable devices or continuous visual monitoring.

The architecture separates sensing from intelligent processing.

ESP32-based sensing nodes collect Wi-Fi CSI measurements, while an Edge Gateway performs signal preprocessing and AI inference locally.

---

## 2. High-Level Architecture

```text
ESP32 CSI Sensing Nodes
          │
          │ CSI Data
          ▼
   Edge Intelligence Gateway
          │
          ├── Signal Preprocessing
          ├── Feature Extraction
          ├── Activity Recognition
          ├── Fall Detection
          ├── Anomaly Detection
          ├── Confidence Estimation
          └── Post-Event Monitoring
          │
          ▼
       Backend
          │
          ▼
      Dashboard
          │
          ▼
    Safety Alerts
```

---

## 3. CSI Sensing Nodes

ESP32-based nodes collect Wi-Fi CSI measurements caused by human movement.

The sensing nodes are responsible for:

* CSI acquisition
* Basic packet-level information collection
* Transmission of extracted CSI data to the Edge Gateway

The monitored individual does not need to wear a device or remain within direct camera visibility.

---

## 4. Edge Intelligence Gateway

The Edge Gateway performs the main local processing pipeline.

The gateway is responsible for:

* Receiving CSI streams
* Signal preprocessing
* Feature extraction
* Activity recognition
* Fall detection
* Behavioral anomaly detection
* Confidence estimation
* Post-event movement monitoring

The proposed gateway may use an embedded computing platform such as an NVIDIA Jetson Nano or Raspberry Pi 4.

---

## 5. AI Processing Pipeline

The proposed processing pipeline is:

```text
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

A lightweight 1D-CNN may be investigated for movement-related feature extraction.

A temporal model such as LSTM, GRU, or a lightweight State Space Model may then analyze the evolution of extracted features over time.

The final model configuration will be selected experimentally.

---

## 6. Post-Event Monitoring

After a potential fall is detected, the system enters a post-event monitoring mode.

The system analyzes subsequent CSI activity and initially classifies the post-event state as:

* Movement Detected
* Limited Movement
* No Significant Movement

This information can provide additional context before generating a safety alert.

---

## 7. Backend and Dashboard

The backend and dashboard provide the software interface for presenting system outputs.

The dashboard presents structured information such as:

* Current activity
* Location
* Confidence
* Anomaly status
* Fall status
* Post-event movement
* Safety alerts

The system does not require live video footage for its proposed sensing pipeline.

---

## 8. Privacy-Preserving Design

The architecture is designed around privacy-preserving sensing.

The proposed system avoids dependence on continuous visual monitoring and performs the main AI processing locally at the Edge Gateway.

This reduces dependence on cloud-based processing and minimizes transmission of raw sensing information.

---

## 9. Initial Deployment Scope

The initial prototype focuses on a controlled single-person environment.

Advanced capabilities such as multi-resident sensing, few-shot environment adaptation, federated learning, advanced explainability, generative data augmentation, and continuous-time modeling are considered future research directions.
