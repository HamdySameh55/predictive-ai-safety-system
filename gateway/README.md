# Edge Gateway

## Overview

The Edge Gateway is responsible for receiving CSI data from the ESP32 sensing nodes and performing the main local processing pipeline.

## Responsibilities

The gateway is expected to handle:

* CSI data reception
* Signal preprocessing
* Feature extraction
* Activity recognition
* Fall detection
* Behavioral anomaly detection
* Confidence estimation
* Post-event movement monitoring

## Processing Flow

```text
ESP32 Nodes
     ↓
CSI Data
     ↓
Gateway
     ↓
Preprocessing
     ↓
AI Inference
     ↓
Detection / Prediction
```

## Edge Processing

The system is designed to perform the main processing locally to reduce dependence on cloud-based processing and minimize transmission of raw sensing information.

