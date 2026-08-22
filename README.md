# 🥛 Real-Time Dual-Sensor IoT Milk Adulteration Detection

## 📌 Project Overview

This project presents an **IoT-based real-time milk adulteration detection system** that combines an **AS7265x multispectral sensor**, **Electrical Conductivity (EC) sensor**, and **ESP32 microcontroller**.

The AS7265x captures the optical characteristics of milk across multiple spectral channels, while the EC sensor measures changes in the electrical conductivity of the sample. Combining these two sensing methods provides complementary information for identifying changes associated with milk adulteration.

The ESP32 collects and processes the sensor readings and uses its built-in Wi-Fi capability to transmit the results to the **Blynk IoT platform** for real-time monitoring.

---

## 🎯 Problem Statement

Milk adulteration is a major food-safety concern. Substances such as **water, detergent, urea, and starch** can alter the physical and chemical characteristics of milk.

Conventional testing methods often require laboratory equipment, chemical reagents, and trained personnel. This creates a need for a portable and rapid screening system that can be used closer to the point of milk collection.

This project aims to develop a **dual-sensor IoT system** capable of analyzing both optical and electrical characteristics of milk for improved adulteration screening.

---

## 💡 Proposed Solution

The proposed system combines two sensing techniques.

### 🔬 AS7265x Multispectral Sensor

The AS7265x provides **18 spectral channels covering approximately 410–940 nm**. It captures the optical response of the milk sample at multiple wavelength bands.

### ⚡ EC Sensor

The Electrical Conductivity sensor measures the ability of the milk sample to conduct electrical current. Changes in ionic composition caused by certain adulterants can produce variations in conductivity.

### 🧠 ESP32

The ESP32 acts as the central processing unit. It:

* Collects AS7265x spectral data
* Collects EC measurements
* Performs preprocessing
* Compares readings with reference values
* Combines information from both sensors
* Determines the milk-quality status
* Sends results through Wi-Fi

### ☁️ Blynk IoT

Blynk provides a mobile/cloud interface for real-time monitoring of sensor readings and detection results.

---

## ⚙️ System Architecture

```text
                         MILK SAMPLE
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 ▼                         ▼
       AS7265x Multispectral          EC Sensor
             Sensor                       │
                 │                         │
        18 Spectral Channels       Conductivity Value
                 │                         │
                 └────────────┬────────────┘
                              │
                              ▼
                         ESP32
                              │
                   Data Preprocessing
                              │
                   Sensor Data Fusion
                              │
                  Reference Comparison
                              │
                 Pure / Adulterated
                              │
                           Wi-Fi
                              │
                              ▼
                       Blynk IoT Cloud
                              │
                              ▼
                     Mobile Dashboard
                              │
                              ▼
                       Final Result
```

---

## 🔬 Working Principle

1. A milk sample is placed in the measurement setup.
2. The **AS7265x multispectral sensor** captures the optical response across 18 wavelength channels.
3. The **EC sensor** measures the electrical conductivity of the same sample.
4. Both sensor outputs are transferred to the **ESP32**.
5. The ESP32 performs basic preprocessing such as filtering, averaging, and normalization.
6. The spectral and conductivity characteristics are compared with reference measurements obtained from known milk samples.
7. The combined sensor information is used to determine whether the sample shows characteristics of pure or adulterated milk.
8. The ESP32 connects to Wi-Fi and sends the processed information to **Blynk**.
9. The user can monitor the readings and final status through the Blynk dashboard.

---

## 🧪 Why Two Sensors?

A single sensor may not capture every change produced by different adulterants.

The two sensors provide complementary information:

```text
AS7265x
   ↓
Optical / Spectral Characteristics

EC Sensor
   ↓
Electrical / Conductivity Characteristics

        ↓
    Sensor Fusion

        ↓
 More Reliable Screening
```

The multispectral sensor provides information about optical changes, while the EC sensor provides information related to electrical conductivity.

---

## 🛠️ Hardware Components

* **ESP32 Development Board**
* **AS7265x Multispectral Sensor**
* **EC Sensor / Electrical Conductivity Probe**
* Milk Sample Container
* Controlled Illumination
* Breadboard / Prototype Board
* Jumper Wires
* USB Cable / Power Supply

---

## 💻 Software and Technologies

* Arduino IDE
* Embedded C/C++
* ESP32
* AS7265x Sensor Library
* I²C Communication
* Wi-Fi
* Blynk IoT Platform
* Sensor Data Processing

---

## 📡 Communication

### AS7265x → ESP32

The AS7265x communicates with the ESP32 using the **I²C protocol**.

```text
AS7265x
   │
   ├── SDA ──► ESP32
   ├── SCL ──► ESP32
   ├── VCC
   └── GND
```

### EC Sensor → ESP32

The EC sensor provides an electrical measurement that is acquired by the ESP32 through the appropriate interface of the EC module being used.

### ESP32 → Blynk

```text
AS7265x ──┐
          ├──► ESP32 ──► Wi-Fi ──► Blynk
EC Sensor ┘
```

---

## 📊 AS7265x Spectral Channels

The AS7265x provides 18 spectral channels covering the visible and near-infrared regions.

| Channel | Wavelength |
| ------- | ---------: |
| A       |     410 nm |
| B       |     435 nm |
| C       |     460 nm |
| D       |     485 nm |
| E       |     510 nm |
| F       |     535 nm |
| G       |     560 nm |
| H       |     585 nm |
| R       |     610 nm |
| I       |     645 nm |
| S       |     680 nm |
| J       |     705 nm |
| T       |     730 nm |
| U       |     760 nm |
| V       |     810 nm |
| W       |     860 nm |
| K       |     900 nm |
| L       |     940 nm |

These measurements provide a multispectral representation of the milk sample.

---

## ⚡ EC Measurement

Electrical conductivity represents the ability of a sample to conduct electrical current.

Changes in milk composition can influence its conductivity. Therefore, EC measurements are used as a complementary parameter along with the spectral readings.

For example:

* **Water dilution** can alter the ionic concentration and conductivity.
* **Detergent or urea addition** can produce changes in electrical conductivity.
* Different milk compositions can naturally produce different conductivity values.

The EC measurement is therefore interpreted together with the multispectral response rather than being used as the only detection parameter.

---

## 🧠 Data Processing

The ESP32 performs the initial processing of the sensor measurements.

The processing pipeline is:

```text
Raw Sensor Data
       ↓
Data Acquisition
       ↓
Noise Reduction / Averaging
       ↓
Normalization
       ↓
Feature Extraction
       ↓
Sensor Data Fusion
       ↓
Reference Comparison
       ↓
Milk Quality Classification
```

The reference values are obtained from controlled measurements of known milk samples.

---

## 📱 IoT Monitoring

The Blynk IoT platform is used to display:

* AS7265x spectral readings
* EC readings
* Milk-quality status
* Processed sensor values
* Real-time monitoring information

The ESP32 sends the processed information through Wi-Fi to the Blynk platform.

---

## 🌟 Key Features

* 🔬 18-channel multispectral analysis
* ⚡ Electrical conductivity measurement
* 🧠 Dual-sensor data fusion
* 📡 ESP32-based IoT connectivity
* 📱 Real-time Blynk monitoring
* 🥛 Non-destructive optical sensing
* 💰 Portable and cost-effective architecture
* ⚡ Rapid field-level screening
* 🌱 Supports smart and sustainable food-quality monitoring

---
 
---

## 🚀 Future Scope

The system can be further improved by:

* Developing a larger labeled dataset
* Applying machine-learning algorithms for adulterant classification
* Estimating adulterant concentration
* Adding temperature compensation
* Improving sensor calibration
* Developing automated sample handling
* Implementing cloud-based historical analysis
* Extending the system to other liquid food products

---

## 🌍 Applications

The system can potentially be used in:

* Dairy farms
* Milk collection centers
* Dairy quality-control units
* Food-safety screening
* Rural milk-testing facilities
* Dairy supply-chain monitoring

---

## 📚 Research Publication

A related research work was published as:

**“Real Time Dual Sensor IoT Milk Adulteration Detection”**

*Advances in Consumer Research, 2025.*

The work focuses on combining sensor-based milk-quality analysis with IoT technology for real-time adulteration screening.

---

## 🎯 Project Objective

The primary objective is to develop a **portable dual-sensor IoT system** that combines optical and electrical measurements to support rapid milk-quality screening and improve accessibility to food-safety monitoring.

---

 
