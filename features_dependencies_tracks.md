# Features, Dependencies & Team Tracks

## Revised Feature Set

| ID     | Feature                                        | Main Scope                                                                                                                                                                                                       |
| ------ | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **F1** | **CSI Acquisition & Gateway Communication**    | ESP32 CSI acquisition, UDP transmission, gateway reception, timestamps, sampling-rate monitoring, packet-loss monitoring                                                                                         |
| **F2** | **External Dataset Acquisition & Preparation** | Find and download public CSI datasets, select relevant activities, inspect dataset quality/metadata, convert/unify formats, prepare labels, and create leakage-safe Train/Validation/Test splits                 |
| **F3** | **Signal Preprocessing & Feature Extraction**  | Amplitude/phase extraction, phase sanitization/unwrapping, Hampel filter, low-pass filter, windowing, normalization, PCA; ensure the same preprocessing pipeline is used during training and real-time inference |
| **F4** | **Activity Recognition**                       | Baseline model, 1D-CNN, training, validation, evaluation, and comparison of activity-recognition performance                                                                                                     |
| **F5** | **Fall Detection & Post-Fall Monitoring**      | Temporal modeling using GRU/LSTM, fall-event detection, and post-event states: Movement / Limited Movement / No Significant Movement                                                                             |
| **F6** | **Confidence & Alert Decision Logic**          | Confidence calibration, normal/uncertain/critical states, alert triggering, waiting logic, threshold management, and alert deduplication                                                                         |
| **F7** | **Backend, Dashboard & Alert Integration**     | API, event reception, history storage, real-time dashboard, SignalR/WebSocket, status/location/confidence/timeline, and configurable alert channel                                                               |
| **F8** | **Edge Deployment & System Evaluation**        | Deploy trained models on the selected gateway platform, ONNX/TFLite where appropriate, latency/CPU/RAM measurements, Precision/Recall/F1, false alarms/day, and detection latency                                |
| **F9** | **Personalized Behavioral Baseline — Stretch** | Learn normal daily activity patterns and detect deviations from the user's personalized baseline                                                                                                                 |

---

## System Architecture

### Training / Development Pipeline

Public CSI Datasets are used to train the models:

```text
Public CSI Datasets
        ↓
       F2
Dataset Acquisition
& Preparation
        ↓
       F3
Preprocessing
        ↓
     F4 / F5
Model Training
        ↓
   Trained Models
```

### Real-Time Inference Pipeline

After the models are trained, the actual system works as:

```text
Person
  ↓
ESP32-S3
  ↓
F1 — CSI Acquisition
  ↓
Gateway
  ↓
F3 — Same Preprocessing Pipeline
  ↓
Trained F4 / F5 Model
  ↓
Prediction
  ↓
F6 — Confidence & Decision Logic
  ↓
F7 — Backend / Dashboard / Alert
```

Example:

```text
Walking
   ↓
ESP32-S3 captures CSI
   ↓
F1
   ↓
F3
   ↓
Activity Recognition Model
   ↓
"Walking"
```

For a fall:

```text
Fall
   ↓
ESP32-S3 captures CSI
   ↓
F1
   ↓
F3
   ↓
Fall Detection Model
   ↓
"Fall"
   ↓
F6
   ↓
Alert Decision
```

---

## Dependencies

```text
                  ┌──→ F4 Activity Recognition ──┐
                  │                               │
F2 → F3 ──────────┤                               ├──→ F6 → F7
                  │                               │
                  └──→ F5 Fall Detection ────────┘
                                                   │
                                                   ↓
                                                  F8


F1 ───────────────→ Real-Time CSI Input ──────────┘

F9 ───────────────→ Advanced / Stretch
```

### Dependency Explanation

* **F2 → F3:** Public CSI datasets must be acquired and prepared before the preprocessing pipeline can be validated on them.
* **F3 → F4/F5:** Activity recognition and fall detection models require processed CSI signals/features.
* **F4/F5 → F6:** Confidence and alert decisions depend on the outputs of the trained models.
* **F6 → F7:** The backend/dashboard receives the final decision and confidence information.
* **F6/F7 → F8:** Final edge deployment and system evaluation should use the complete selected decision pipeline.
* **F1 → F3:** During real-time operation, CSI acquired from the ESP32 and received by the gateway must pass through the same preprocessing pipeline used during model training.
* **F1 does not depend on F2 for real-time operation.** F1 provides the live CSI input after the models have already been trained.
* **F7:** Can be developed independently using dummy/sample model outputs and integrated with the real ML pipeline later.
* **F9:** Advanced personalization can be developed after the core MVP is stable.

---

## Team Tracks

| Track                                      | Features     | Responsibility                                                                                                      |
| ------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Track A — Hardware & Signal Processing** | F1 + F3      | ESP32, CSI acquisition, gateway communication, signal preprocessing, and real-time signal pipeline                  |
| **Track B — Machine Learning**             | F4 + F5 + F6 | Activity recognition, fall detection, temporal modeling, confidence, and decision logic                             |
| **Track C — Backend & Dashboard**          | F7           | API, storage, real-time dashboard, event history, and alerts                                                        |
| **Track D — Data & Evaluation**            | F2 + F8      | Public dataset acquisition/preparation, dataset quality, benchmarking, deployment evaluation, and system evaluation |
| **Stretch**                                | F9           | Personalized behavioral modeling                                                                                    |

---

## Development Strategy

### Phase 1 — Foundation

* Implement basic ESP32 CSI acquisition.
* Establish communication between ESP32 and the gateway.
* Verify CSI packet reception and packet-loss monitoring.
* Define the common CSI data format.
* Search for suitable public CSI datasets.
* Begin backend/dashboard development with dummy data.

### Phase 2 — Dataset & Signal Processing

* Download and inspect suitable public CSI datasets.
* Select datasets/classes relevant to the project.
* Unify different dataset formats where necessary.
* Define the common label schema.
* Build the preprocessing pipeline.
* Extract amplitude and phase.
* Apply filtering, windowing, normalization, and PCA where appropriate.
* Create leakage-safe Train/Validation/Test splits.

### Phase 3 — Machine Learning

* Establish a simple baseline.
* Develop the 1D-CNN activity recognition model.
* Train and validate the activity-recognition model.
* Develop temporal modeling for fall detection.
* Implement post-fall monitoring states.
* Compare model performance using the defined evaluation metrics.

### Phase 4 — Real-Time Integration

* Connect the trained models to the real-time CSI pipeline.
* Feed ESP32 CSI through the same preprocessing pipeline used during training.
* Test real-time activity recognition.
* Test real-time fall detection.
* Add confidence calibration.
* Define normal, uncertain, and critical states.
* Implement alert decision logic.
* Connect ML outputs to the backend and dashboard.

### Phase 5 — Edge Deployment & Evaluation

* Deploy the selected trained models on the target gateway.
* Use ONNX/TFLite where appropriate.
* Measure inference latency, CPU usage, and RAM usage.
* Evaluate Precision, Recall, F1-score, false alarms/day, and detection latency.
* Identify bottlenecks and optimize the system.

### Phase 6 — Stretch

* Implement the personalized behavioral baseline.
* Learn normal activity patterns.
* Detect deviations from individual behavioral patterns.

---

## MVP Scope

The initial MVP should focus on:

* **F1 — CSI Acquisition & Gateway Communication**
* **F2 — External Dataset Acquisition & Preparation**
* **F3 — Signal Preprocessing & Feature Extraction**
* **F4 — Activity Recognition**
* **F5 — Fall Detection & Post-Fall Monitoring**
* **F6 — Confidence & Alert Decision Logic**
* **F7 — Backend, Dashboard & Alert Integration**
* **F8 — Edge Deployment & System Evaluation**

**F9 is an optional advanced feature and should not block the MVP.**

---

## Important Implementation Notes

* F1 is responsible for the **real-time CSI input pipeline**, not model training or prediction.
* F2 uses **external/public CSI datasets** to prepare training and evaluation data.
* The project does not require F2 to collect the real-time CSI used during deployment.
* F3 must use a consistent preprocessing definition between training and inference to avoid training/inference mismatch.
* UDP packet loss should be **monitored and measured**, not assumed to be zero.
* Dataset splitting should be performed by **participant/session groups where possible**, rather than randomly splitting individual windows, to reduce data leakage.
* Different public datasets may have different CSI dimensions, sampling rates, channels, bandwidths, and preprocessing conventions. These differences must be documented before combining datasets.
* The deployment target can be **Raspberry Pi 4 or NVIDIA Jetson Nano**, according to the final hardware decision.
* ONNX/TFLite conversion should be selected based on the model framework and target hardware.
* The alert channel (for example, Telegram) should remain configurable until the team agrees on the final implementation.
* Backend and dashboard development can start early with dummy model outputs and later be connected to the real inference pipeline.
* Public datasets are used primarily for model development; the final real-time system receives CSI directly from the project's ESP32-S3 hardware.
