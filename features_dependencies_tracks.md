# Features, Dependencies & Team Tracks

## Revised Feature Set

| ID | Feature | Main Scope |
|---|---|---|
| **F1** | **CSI Acquisition & Gateway Communication** | ESP32 CSI acquisition, UDP transmission, gateway reception, timestamps, sampling-rate monitoring, packet-loss monitoring |
| **F2** | **Data Collection & Labeling** | Define scenarios, collect CSI data, attach activity labels, organize datasets, session-based Train/Validation/Test split |
| **F3** | **Signal Preprocessing & Feature Extraction** | Amplitude/phase extraction, phase sanitization/unwrapping, Hampel filter, low-pass filter, windowing, normalization, PCA |
| **F4** | **Activity Recognition** | Baseline model, 1D-CNN, training, validation, evaluation, comparison of recognition performance |
| **F5** | **Fall Detection & Post-Fall Monitoring** | Temporal modeling using GRU/LSTM, fall-event detection, post-event states: Movement / Limited Movement / No Significant Movement |
| **F6** | **Confidence & Alert Decision Logic** | Confidence calibration, normal/uncertain/critical states, alert triggering, waiting logic, threshold management, alert deduplication |
| **F7** | **Backend, Dashboard & Alert Integration** | API, event reception, history storage, real-time dashboard, SignalR/WebSocket, status/location/confidence/timeline, alert channel |
| **F8** | **Edge Deployment & System Evaluation** | Deploy models on the selected gateway platform, ONNX/TFLite where appropriate, latency/CPU/RAM measurements, Precision/Recall/F1, false alarms/day, detection latency |
| **F9** | **Personalized Behavioral Baseline — Stretch** | Learn normal daily activity patterns and detect deviations from the user's personalized baseline |

---

## Dependencies

```text
                         ┌──→ F4 Activity Recognition ──┐
F1 → F2 → F3 ────────────┤                              ├──→ F6 → F8
                         └──→ F5 Fall Detection ───────┘

F7 ─────────────────────────────────────────────────────────→ Integration

F9 ─────────────────────────────────────────────────────────→ Advanced / Stretch
```

### Dependency Explanation

- **F1 → F2:** Data collection depends on having a working CSI acquisition and gateway communication pipeline.
- **F2 → F3:** Collected CSI data must be available before preprocessing can be validated on real data.
- **F3 → F4/F5:** Activity recognition and fall detection require processed signals/features.
- **F4/F5 → F6:** Confidence and alert decisions depend on the outputs of the recognition and detection models.
- **F6 → F8:** Final deployment and system evaluation should use the selected decision pipeline.
- **F7:** Can be developed independently using dummy/sample data and integrated with the ML pipeline later.
- **F9:** Advanced personalization can be developed after the core MVP is stable.

> **Note:** F2 should begin as early as possible and can overlap with the later stages of F1 once the basic CSI data pipeline is working.

---

## Team Tracks

| Track | Features | Responsibility |
|---|---|---|
| **Track A — Hardware & Signal Processing** | F1 + F3 | ESP32, CSI acquisition, communication, signal preprocessing |
| **Track B — Machine Learning** | F4 + F5 + F6 | Activity recognition, fall detection, temporal modeling, confidence and decision logic |
| **Track C — Backend & Dashboard** | F7 | API, storage, real-time dashboard, event history, alerts |
| **Track D — Data & Evaluation** | F2 + F8 | Dataset collection, labeling, deployment, benchmarking and system evaluation |
| **Stretch** | F9 | Personalized behavioral modeling |

---

## Development Strategy

### Phase 1 — Foundation

- Implement basic ESP32 CSI acquisition.
- Establish communication between ESP32 and the gateway.
- Start collecting initial CSI samples.
- Define the data format and labeling procedure.
- Begin backend/dashboard development with dummy data.

### Phase 2 — Signal Processing & Dataset

- Build the preprocessing pipeline.
- Extract amplitude and phase.
- Apply filtering, windowing, normalization, and PCA.
- Build the first labeled dataset.
- Maintain session-based Train/Validation/Test splits.

### Phase 3 — Machine Learning

- Establish a simple baseline.
- Develop the 1D-CNN activity recognition model.
- Develop temporal modeling for fall detection.
- Implement post-fall monitoring states.
- Compare model performance using the defined evaluation metrics.

### Phase 4 — Confidence & Integration

- Add confidence calibration.
- Define normal, uncertain, and critical states.
- Implement alert decision logic.
- Connect ML outputs to the backend and dashboard.
- Integrate real-time event communication.

### Phase 5 — Edge Deployment & Evaluation

- Deploy the selected models on the target gateway.
- Measure inference latency, CPU usage, and RAM usage.
- Evaluate Precision, Recall, F1-score, false alarms/day, and detection latency.
- Identify bottlenecks and optimize the system.

### Phase 6 — Stretch

- Implement the personalized behavioral baseline.
- Learn normal activity patterns.
- Detect deviations from individual behavioral patterns.

---

## MVP Scope

The initial MVP should focus on:

- F1 — CSI Acquisition & Gateway Communication
- F2 — Data Collection & Labeling
- F3 — Signal Preprocessing & Feature Extraction
- F4 — Activity Recognition
- F5 — Fall Detection & Post-Fall Monitoring
- F6 — Confidence & Alert Decision Logic
- F7 — Backend, Dashboard & Alert Integration
- F8 — Edge Deployment & System Evaluation

**F9 is an optional advanced feature and should not block the MVP.**

---

## Important Implementation Notes

- UDP packet loss should be **monitored and measured**, not assumed to be zero.
- The deployment target can be **Raspberry Pi 4 or NVIDIA Jetson Nano**, according to the final hardware decision.
- ONNX/TFLite conversion should be selected based on the model framework and target hardware.
- The alert channel (for example, Telegram) should remain configurable until the team agrees on the final implementation.
- Dataset splitting should be performed by **sessions**, rather than randomly splitting individual samples, to reduce data leakage.
- Backend and dashboard development can start early with dummy data and later be connected to real model outputs.
