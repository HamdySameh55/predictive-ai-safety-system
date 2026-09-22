
# Firmware

## Overview

The firmware component is responsible for the ESP32-based CSI sensing nodes.

## Responsibilities

The firmware is expected to handle:

* Wi-Fi configuration
* CSI acquisition
* Sensor/node identification
* CSI data collection
* Basic data preparation
* Transmission of CSI data to the Edge Gateway

## Data Flow

```text
Wi-Fi Signal
     ↓
ESP32
     ↓
CSI Acquisition
     ↓
Data Preparation
     ↓
Edge Gateway
```

## Development

Firmware implementation details, communication configuration, and CSI extraction procedures will be documented here as development progresses.
