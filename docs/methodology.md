# Methodology

## 1. Overview

The proposed methodology uses Wi-Fi Channel State Information (CSI) and Edge AI to perform device-free human activity monitoring.

The system follows a sensing, preprocessing, feature extraction, temporal analysis, and prediction pipeline.

---

## 2. Data Acquisition

ESP32-based sensing nodes collect Wi-Fi CSI measurements affected by human movement.

The collected CSI data is transmitted to the Edge Gateway for processing.

The initial prototype focuses on a controlled single-person environment.

---

## 3. Signal Preprocessing

Raw CSI measurements require preprocessing before being provided to AI models.

The proposed preprocessing stages include:

### 3.1 Amplitude Extraction

The system can extract the amplitude of the complex CSI measurements.

### 3.2 Phase Extraction

CSI phase information can also be extracted and processed using phase unwrapping and sanitization techniques.

### 3.3 Outlier Mitigation

A temporal Hampel filter may be applied to reduce abnormal measurements caused by hardware noise and signal spikes.

### 3.4 Low-Pass Filtering

A digital low-pass filter may be applied to reduce high-frequency noise while retaining signal variations associated with human movement.

### 3.5 Dimensionality Reduction

Principal Component Analysis (PCA) will be investigated to reduce dimensionality and redundancy in CSI subcarrier measurements.

---

## 4. Proposed Processing Pipeline

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

The final preprocessing configuration will be selected experimentally based on signal quality and model performance.

---

## 5. Activity Recognition

The system aims to recognize human activities from processed CSI sequences.

A lightweight 1D-CNN may be investigated for extracting movement-related features.

A temporal model such as LSTM, GRU, or a lightweight State Space Model may then analyze temporal activity patterns.

---

## 6. Personalized Behavioral Modeling

The system will learn representations of an individual's normal activity patterns.

Activities can be represented as sequences, for example:

```text
[Bed_Exit] → [Walk] → [Kitchen] → [Sitting]
```

New activity sequences can be compared with the learned baseline.

Significant deviations may be classified as behavioral anomalies and used as an additional safety signal.

---

## 7. Fall Detection

The system will analyze temporal CSI patterns associated with sudden changes in human movement.

Potential indicators include:

* Rapid movement changes
* Sudden amplitude variations
* Abrupt transitions between activities
* Transition from movement to prolonged inactivity

Fall detection is intended to consider temporal context rather than relying only on a single threshold.

---

## 8. Post-Fall Monitoring

After a potential fall is detected, the system enters a post-event monitoring mode.

The subsequent CSI activity is analyzed and initially classified into:

* Movement Detected
* Limited Movement
* No Significant Movement

---

## 9. Confidence-Aware Prediction

AI predictions will be associated with confidence values.

Example:

```text
Activity: Walking
Confidence: 92%
```

Or:

```text
Event: Possible Fall
Confidence: 94%
```

A confidence threshold can be investigated to distinguish between normal observations, uncertain events, and high-confidence critical events.

---

## 10. Evaluation

The final preprocessing and model configuration will be selected experimentally based on signal quality and model performance.

The initial system will be developed and evaluated in a controlled single-person environment.

