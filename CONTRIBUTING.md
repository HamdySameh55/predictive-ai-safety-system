# Contributing to Predictive AI Safety System

Thank you for your interest in contributing to the **Predictive AI Safety System**.

This document explains how to contribute to the project and keep the development process organized.

---

## 1. Getting Started

Before contributing, make sure you have:

* Git installed.
* Access to the GitHub repository.
* The required development tools for the part of the project you are working on.
* A basic understanding of the project architecture.

Clone the repository:

```bash
git clone https://github.com/HamdySameh55/predictive-ai-safety-system.git
cd predictive-ai-safety-system
```

---

## 2. Create a Branch

Do not make changes directly on the `main` branch.

Create a new branch for your contribution:

```bash
git checkout -b feature/your-feature-name
```

Examples:

```bash
git checkout -b feature/csi-data-collection
git checkout -b feature/fall-detection-model
git checkout -b docs/update-readme
git checkout -b fix/gateway-connection
```

---

## 3. Make Your Changes

Implement your changes while following the existing project structure and conventions.

For CSI-related changes, keep the existing data contracts consistent:

```text
CSI Packet
    ↓
Preprocessing Window
    ↓
Model Output
    ↓
Event
```

If you modify a data contract, update the relevant documentation and schema version when necessary.

---

## 4. Test Your Changes

Before submitting a contribution:

1. Run the relevant tests.
2. Verify that the existing functionality still works.
3. Test new functionality where applicable.
4. Check for errors, warnings, or broken dependencies.

For hardware-related contributions, verify communication between the ESP32 nodes and the gateway when possible.

---

## 5. Commit Your Changes

Use clear and descriptive commit messages.

Example:

```bash
git add .
git commit -m "Add CSI packet data contract"
```

Other examples:

```text
Add ESP32 CSI acquisition
Add preprocessing pipeline
Update fall detection model
Fix gateway packet handling
Update CSI documentation
Add activity recognition evaluation
```

---

## 6. Push Your Branch

Push your branch to GitHub:

```bash
git push -u origin feature/your-feature-name
```

---

## 7. Create a Pull Request

After pushing your branch:

1. Open the repository on GitHub.
2. Select **Compare & pull request**.
3. Provide a clear title.
4. Explain what was changed.
5. Explain why the change was needed.
6. Mention any testing performed.
7. Submit the Pull Request.

Example Pull Request title:

```text
Add CSI packet acquisition and validation
```

---

## 8. Pull Request Guidelines

A Pull Request should:

* Have a clear purpose.
* Contain focused changes.
* Avoid unrelated modifications.
* Include relevant documentation.
* Include tests when applicable.
* Keep existing functionality working.

Large changes should be discussed with the project maintainers before implementation.

---

## 9. Hardware Contributions

Hardware-related contributions may involve:

* ESP32 CSI acquisition.
* Multiple ESP32 receiver nodes.
* Raspberry Pi gateway.
* Wi-Fi router configuration.
* USB communication.
* Power and deployment setup.

When adding hardware functionality, document:

* Hardware model.
* Required configuration.
* Firmware version.
* Network configuration.
* Required dependencies.
* Setup instructions.

---

## 10. Data and Machine Learning Contributions

For changes related to data processing or machine learning, document:

* Dataset or data source.
* Preprocessing method.
* Window size.
* Sampling frequency.
* Feature representation.
* Model architecture.
* Model version.
* Evaluation metrics.

For example:

```text
Preprocessing version: v1
Window shape: [52, 500]
Sampling frequency: 100 Hz
Model version: cnn-0.1
```

---

## 11. Data Contract Changes

The project uses versioned data contracts for communication between system components.

The main contracts are:

```text
ESP32 → Gateway
    CSI Packet

Preprocessing → Model
    Window

Model → Gateway / Backend
    Model Output

Gateway → Backend / Dashboard
    Event
```

When changing a contract:

1. Determine whether the change is backward compatible.
2. Update the relevant documentation.
3. Update `schema_version` if required.
4. Update affected components.
5. Test the complete data flow.

---

## 12. Reporting Issues

When opening an issue, provide:

* A clear title.
* Description of the problem.
* Steps to reproduce.
* Expected behavior.
* Actual behavior.
* Relevant logs or error messages.
* Hardware and software versions when applicable.

Example:

```text
Title:
ESP32 CSI packets are being dropped by the gateway

Description:
The gateway receives packets from rx1 but sequence numbers
show unexpected gaps.

Expected:
Packets should be received in sequence with minimal packet loss.

Actual:
Multiple sequence numbers are missing.
```

---

## 13. Documentation Contributions

Documentation improvements are welcome.

You can contribute by:

* Fixing incorrect information.
* Improving setup instructions.
* Adding examples.
* Documenting APIs and data contracts.
* Improving hardware setup instructions.
* Adding troubleshooting information.

Documentation-only changes can use:

```bash
git checkout -b docs/update-documentation
```

---

## 14. Code of Conduct

Contributors are expected to communicate respectfully and professionally.

Please:

* Be respectful to other contributors.
* Provide constructive feedback.
* Keep discussions focused on the project.
* Avoid personal attacks or inappropriate behavior.

---

## 15. Contribution Workflow

The recommended workflow is:

```text
Fork / Clone Repository
        ↓
Create Feature Branch
        ↓
Make Changes
        ↓
Test Changes
        ↓
Commit
        ↓
Push Branch
        ↓
Open Pull Request
        ↓
Code Review
        ↓
Merge
```

---

## 16. Questions

If you are unsure about an implementation or contribution, open an issue or discuss the proposed change with the project maintainers before starting major work.

Thank you for contributing to the **Predictive AI Safety System**.
