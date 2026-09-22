# Machine Learning

## Overview

The Machine Learning component is responsible for developing the AI models used for activity recognition, fall detection, behavioral anomaly detection, and related predictions.

## Proposed Pipeline

```text
CSI
 ↓
Preprocessing
 ↓
Feature Extraction
 ↓
Temporal Analysis
 ↓
Prediction
 ↓
Confidence Estimation
```

## Candidate Models

The proposal considers:

* Lightweight 1D-CNN
* LSTM
* GRU
* Lightweight State Space Model

The final model architecture will be selected experimentally based on signal quality and model performance.

## Main Tasks

The ML component will cover:

* Data preparation
* Preprocessing
* Feature extraction
* Model development
* Training
* Evaluation
* Inference
* Confidence estimation
* Personalized behavioral modeling

## Initial Scope

The initial prototype focuses on a controlled single-person environment.

