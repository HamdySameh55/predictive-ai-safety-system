# Hardware

## 1. Overview

The proposed system uses distributed sensing nodes and an Edge Gateway to collect and process Wi-Fi CSI data.

---

## 2. CSI Sensing Nodes

The sensing layer is based on ESP32 devices.

The ESP32 nodes are responsible for:

* Collecting Wi-Fi CSI measurements
* Capturing wireless signal variations caused by human movement
* Transmitting CSI data to the Edge Gateway

The prototype should use multiple sensing nodes to support distributed CSI acquisition.

---

## 3. Edge Gateway

The Edge Gateway performs local signal processing and AI inference.

The proposal considers embedded computing platforms such as:

* NVIDIA Jetson Nano
* Raspberry Pi 4

The final platform should be selected based on the computational requirements of the AI pipeline.

---

## 4. Supporting Hardware

The prototype may require:

* ESP32 development boards
* Edge Gateway
* USB cables
* Power supplies
* Network connectivity equipment
* Required connectors and accessories

The exact hardware configuration will be finalized based on the implementation requirements.

---

## 5. Hardware Architecture

```text
ESP32 Node 1 ─┐
ESP32 Node 2 ─┼──→ Edge Gateway ──→ AI Processing
ESP32 Node 3 ─┘
```

The ESP32 nodes form the sensing layer, while the Edge Gateway provides local processing.

---

## 6. Hardware Considerations

The final hardware setup should consider:

* CSI support
* Processing capability
* Memory requirements
* Network connectivity
* Power requirements
* Physical sensor placement
* Environment and room configuration

The hardware configuration may be adjusted during experimentation.

