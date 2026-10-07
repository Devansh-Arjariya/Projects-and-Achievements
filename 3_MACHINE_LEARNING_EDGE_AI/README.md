# 🤖 Division 3: Machine Learning & Edge AI Engineering

> **On-device neural inference, battery electrochemical degradation modeling, and intelligent manufacturing computer vision.**

---

## 🎯 Division Overview

Modern cyber-physical systems cannot rely exclusively on cloud computing for mission-critical decisions. Latency bottlenecks, intermittent wireless connectivity, and privacy concerns necessitate **Edge AI**—executing trained mathematical models directly on microcontrollers and embedded edge processors.

This division bridges data science and embedded engineering across two strategic domains:
1. **Electrochemical Battery Intelligence (`A_BATTERY_MODELS`):** Replacing simplistic linear approximations with machine learning estimators to predict State-of-Charge (SoC), State-of-Health (SoH), and Remaining Useful Life (RUL) under noisy, dynamic load conditions.
2. **Industrial Computer Vision (`B_MANUFACTURING_AI`):** Edge-deployed convolutional neural networks (CNNs) for real-time assembly line anomaly detection and component defect classification, highlighted by the **Cognizant Technoverse** challenge.

---

## 🗂️ Directory Architecture

```text
3_MACHINE_LEARNING_EDGE_AI/
│
├── 📁 A_BATTERY_MODELS/         # Machine learning estimators for battery health & degradation
│   └── 📄 README.md
│
└── 📁 B_MANUFACTURING_AI/       # Industrial edge vision & anomaly detection
    ├── 📄 README.md
    └── 📁 Cognizant_Technoverse/ # Automated manufacturing inspection challenge project
        └── 📄 README.md
```

---

## 📊 Comparative Technical Matrix

| Dimension | Battery Intelligence (`A_BATTERY_MODELS`) | Industrial Vision (`B_MANUFACTURING_AI`) |
|---|---|---|
| **Input Data Modality** | Multi-channel continuous 1D time-series ($V, I, T, \Delta t$) | 2D / 3D spatial image matrices (RGB / Grayscale inspection frames) |
| **Model Architectures** | Polynomial Regression, Random Forests, 1D-CNN / LSTM | Lightweight CNNs (MobileNetV2, SqueezeNet, YOLO-tiny) |
| **Target Edge Silicon** | ESP32 (Xtensa Dual-Core) / ARM Cortex-M4 | Raspberry Pi 4 / Coral Edge TPU / Jetson Nano / x86 Edge |
| **Runtime Engine** | TensorFlow Lite for Microcontrollers (TFLM) / C++ arrays | ONNX Runtime / OpenCV DNN / TFLite C++ Runtime |
| **Primary Metric** | Root Mean Square Error ($RMSE < 1.5\%$) on SoC | Precision, Recall, and Inference Latency ($< 30 \, ms/frame$) |

---

## 🔗 Sub-Folder Quick Links

* 👉 [**Battery State Estimation Models**](./A_BATTERY_MODELS/README.md)
* 👉 [**Manufacturing AI Overview**](./B_MANUFACTURING_AI/README.md)
* 👉 [**Cognizant Technoverse Industrial Inspection Project**](./B_MANUFACTURING_AI/Cognizant_Technoverse/README.md)
