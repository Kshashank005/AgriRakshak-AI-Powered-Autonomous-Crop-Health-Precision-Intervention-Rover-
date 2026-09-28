# 🌾 AgriRakshak: AI-Powered Autonomous Crop Health & Precision Intervention Rover

> **A Field-Deployable Smart Farming Assistant for Early Disease Detection, Soil Health Monitoring, and Targeted Pesticide Spraying**

---

## 🌍 Overview

India's farmers face recurring, large-scale crop losses from undetected diseases, pests, nutrient deficiencies, and climate stress — with crop damage repeatedly crossing **5+ million hectares annually** (peaking at 11.42 mha in 2019-20) due to floods, droughts, and heat waves, compounded by pest/disease losses of **15–25% of annual yield** in Indian field studies.

**AgriRakshak** is an autonomous, field-deployable AI rover that closes this gap by scanning every plant for disease and pests, sensing soil moisture and nutrients in real time, and responding with **targeted, plant-level pesticide spraying** — all through **on-device AI intelligence** that works even without internet connectivity. Paired with the **AgriSense dashboard**, it turns raw field data into farmer-ready alerts and AI-driven treatment recommendations.

Built for **Smart India Hackathon 2026** — Problem Statement 26180 (Agriculture, FoodTech & Rural Development).

---

## 🚀 Key Features

- **Autonomous Field Navigation:** Depth-camera-based obstacle avoidance for movement across uneven field terrain and between plant rows.
- **Plant-by-Plant Disease Detection:** Dual-camera crop scanning processed through an on-device MobileNetV2 model (38-class plant disease classification, ~42ms inference latency).
- **Closed-Loop Targeted Spraying:** Onboard pesticide reservoir, pump, and solenoid valves spray only the exact diseased plant — no blanket application.
- **Soil Health Monitoring:** Real-time moisture and NPK sensing to guide irrigation and fertilization decisions.
- **On-Device, Offline-Capable Intelligence:** Navigation, detection, and spray decisions run directly on the rover — no cloud dependency required for core operation.
- **Farmer + Rover Dashboard:** Live camera feed, sensor trends, and AI-driven action plans delivered through a real-time web dashboard.

---

## 🛠️ Technology Stack

**Frontend & Dashboard:**
- ⚛️ **React 19 + TypeScript** – Component-driven, type-safe dashboard UI
- ⚡ **Vite** – Build tooling and HMR
- 🎨 **Tailwind CSS** – Styling and responsive layout
- 📊 **Recharts** – Real-time sensor trend and disease-distribution visualization

**AI, Compute & Backend:**
- 🧠 **MobileNetV2 (PyTorch)** – Edge-optimized plant disease classification
- 🚀 **FastAPI + Uvicorn** – Inference server and REST API
- 🖼️ **PIL (Pillow)** – Image preprocessing (crop, resize, normalize)
- 📷 **Intel RealSense D435i** – Depth sensing for autonomous navigation

**Embedded Hardware & Firmware:**
- 🖥️ **Raspberry Pi 5** – AI inference, camera host, sensor readings
- 🔧 **ESP32 (WROOM-32)** – Real-time motor, sensor, and actuator control
- 🔌 **UART Serial Protocol** – ESP32 ↔ Pi 5 command bridge with watchdog safety

---

## ⚙️ Hardware Components

| Component | Function |
|---|---|
| **Raspberry Pi 5** | Main compute — AI inference, camera host, dashboard interface |
| **ESP32 (WROOM-32)** | Real-time controller — motor, sensor, and actuator commands |
| **Intel RealSense D435i** | Depth camera for autonomous navigation and obstacle avoidance |
| **2× Webcams (Left/Right)** | Plant-by-plant crop scanning for disease/pest detection |
| **Dual BTS7960 H-Bridge Drivers** | Differential-drive motor control |
| **DC Motors + Wheels** | Rover mobility across field terrain |
| **Soil Moisture Sensor + NPK Sensor** | Soil health and irrigation-need sensing |
| **DHT11 Sensor** | Temperature and humidity (microclimate) monitoring |
| **12V Diaphragm Pump + Solenoid Valves** | Targeted pesticide spraying on affected plants |
| **Reservoir Tank** | Onboard pesticide/spray liquid storage |
| **12V LiFePO4 Battery + Voltage Divider** | Power source and battery telemetry |

---

## 🧩 Software Modules

1. **Perception & Detection**
   - Dual-camera image acquisition and preprocessing
   - On-device AI classification (disease / pest / nutrient deficiency)

2. **Soil Data Acquisition**
   - Real-time moisture and NPK sensor readings across the field

3. **Treatment Decision & Targeting**
   - Determines treatment necessity, calculates spray dosage, and maps target plant position

4. **Actuation, Logging & Dashboard**
   - Activates spray actuator, logs treatment (disease, dosage, images, moisture)
   - Streams live updates and alerts to the farmer dashboard

5. **Farmer Dashboard (AgriSense)**
   - Live rover camera feed, sensor trend graphs, AI-driven action plans and treatment recommendations

---

## 🧪 Prototype Workflow

1. Rover autonomously navigates the field using depth-camera-based obstacle avoidance →
2. Dual webcams continuously scan crops; soil sensors log moisture/NPK data →
3. On-device AI classifies each plant as healthy, diseased, pest-affected, or nutrient-deficient →
4. If a problem is detected, the system calculates spray dosage and maps the target plant's position →
5. Solenoid-controlled pump sprays precisely on the affected plant →
6. Treatment is logged and pushed to the farmer dashboard with real-time alerts and recommendations.

---

## 🧠 Challenges & Engineering Strategies

| Challenge | Strategy |
|---|---|
| Uneven field terrain limits rover mobility | Rugged wheelbase with adjustable ground clearance, field-tested across terrain types |
| Similar visual symptoms across diseases risk misdiagnosis | Multi-angle imaging with models trained to distinguish symptom-similar disease classes |
| Lighting/weather shifts affect detection accuracy | Training on diverse field-condition datasets with auto-exposure calibration |
| Weak/unstable network delays dashboard sync | Store-and-forward architecture: logs locally, bursts sync when connectivity returns |
| Difficulty navigating between plant rows/fields | Depth-based vision navigation for real-time obstacle avoidance |
| Missed disease cases (false negatives) risk silent spread | Confidence-threshold flagging — uncertain cases sent for farmer review instead of auto-classified as healthy |

---

## 📊 Results & Impact *(update with real test data as validation progresses)*

- **Prototype Status:** Hardware and dashboard built; AI model and navigation under active field validation.
- **Model:** MobileNetV2, 38-class plant disease classification, ~42ms edge inference latency.
- **Projected Impact** *(based on published precision-agriculture research — see References below)*:
  - ~35–40% reduction in pesticide/fertilizer costs via targeted spraying
  - ~30% reduction in water usage via sensor-guided irrigation
  - Early detection targeted at reducing the 15–25% pest/disease-driven yield loss reported in Indian field studies

---

## 🧭 Competitive Landscape

| Solution | Focus | Limitation |
|---|---|---|
| **TartanSense BladeRunner (India)** | Robotic spot-spraying for cotton | Spraying only — no integrated soil health sensing or farmer dashboard |
| **IoT Soil Sensor Platforms (e.g., Fasal, CropIn)** | Soil/crop monitoring | Sensing only — no autonomous intervention or spraying capability |
| **International Precision-Spray Robots** | Targeted agrochemical application | High cost, not designed for Indian smallholder field conditions |
| **AgriRakshak (Proposed)** | Integrated detect → diagnose → treat → monitor, in one autonomous platform | Field-deployable, on-device intelligence, closed-loop treatment — combines capabilities usually sold as separate point solutions |

---

## 📚 References

1. Indian pest/disease-driven crop loss data (15–25% of annual yield) — [Link](https://arxiv.org/pdf/2011.04056)
2. Precision water delivery / irrigation efficiency studies (up to 30% water savings) — [Link](https://www.frontiersin.org/journals/sustainable-food-systems/articles/10.3389/fsufs.2026.1755061/full)
3. MobileNetV2-based plant disease classification benchmark (94.7% accuracy, 101 diseases, 33 crops) — [Link](https://arxiv.org/pdf/2508.10817)
4. TartanSense BladeRunner — India spot-spray robot case study — [Link](https://yourstory.com/2021/08/funding-agritech-robotics-startup-tartansense-fmc-omnivore-blume-ventures)
5. Digital Agriculture Mission, Government of India (₹2,817 crore, Sept 2024) — [Link](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2101848&reg=48&lang=2)

---

## 📅 Team

**Team Name:** Yuva Raitharu KT
**Team ID:** 167323
**Problem Statement ID:** 26180
**Theme:** Agriculture, FoodTech & Rural Development
**PS Category:** Hardware
