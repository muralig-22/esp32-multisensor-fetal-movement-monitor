
# ESP32 Multisensor Fetal Movement Monitor

### Distributed Motion Sensing Using I2C Multiplexing

## Overview

An ESP32-based multi-sensor motion-monitoring prototype integrating three MPU6050 accelerometer and gyroscope modules through a TCA9548A I2C multiplexer.

The system acquires motion data from multiple sensor locations, computes acceleration magnitude, performs threshold-based motion classification, and generates buzzer alerts for kick-level events.

## Problem Statement

Multi-location motion sensing can improve the amount of movement information available to an embedded monitoring system.

However, identical I2C sensor modules often share the same fixed bus address, preventing multiple devices from operating independently on a single I2C bus.

## Proposed Solution

Integrated three MPU6050 sensors through a TCA9548A I2C multiplexer to enable multiple same-address devices to communicate with one ESP32 controller.

Each sensor provides three-axis acceleration measurements.

The firmware calculates acceleration magnitude and classifies readings into:

- Normal.
- Stretching.
- Kick.

A buzzer is activated for kick-level events, while the system also transmits monitoring data through Bluetooth Serial.

## System Architecture

```text
MPU6050 - Sensor 1 ──┐
                     |
MPU6050 - Sensor 2 ──┼── TCA9548A
                     |       |
MPU6050 - Sensor 3 ──┘       |
                             |
                             v
                           ESP32
                             |
                 Acceleration Processing
                             |
                             v
                    Motion Classification
                             |
                   ┌─────────┴─────────┐
                   |                   |
                   v                   v
                Buzzer           Bluetooth Serial
```

## Hardware Components

| Component | Function |
|---|---|
| ESP32 | Main controller |
| MPU6050 × 3 | Three-axis motion sensing |
| TCA9548A | I2C bus multiplexing |
| Buzzer | Audible event indication |

## Technical Implementation

### 1. Multi-Sensor I2C Integration

Connected three MPU6050 modules through separate TCA9548A multiplexer channels.

This allows identical-address I2C devices to be accessed individually.

### 2. Motion Data Acquisition

Acquired three-axis acceleration measurements from each sensor.

### 3. Acceleration Magnitude

Calculated acceleration magnitude using:

\[
A = \sqrt{a_x^2+a_y^2+a_z^2}
\]

### 4. Motion Classification

Implemented threshold-based classification to identify normal, stretching, and kick-level motion patterns.

### 5. Event Indication

Activated a buzzer when kick-level thresholds were detected.

### 6. Wireless Communication

Bridged motion classification results through Bluetooth Serial for external monitoring.

## Key Features

- Three independent MPU6050 sensors.
- TCA9548A I2C address multiplexing.
- Multi-location acceleration acquisition.
- Three-axis acceleration magnitude calculation.
- Threshold-based motion classification.
- Buzzer-based event notification.
- Bluetooth Serial communication.

## Technology Stack

- ESP32.
- Embedded C / Arduino framework.
- MPU6050.
- TCA9548A.
- I2C.
- Bluetooth Serial.
- Accelerometer-based motion processing.

## Project Outcome

Developed a working multi-sensor motion-classification prototype demonstrating address-safe I2C device integration, distributed motion sensing, embedded event detection, and wireless communication.

## Future Enhancements

- Sensor calibration.
- Adaptive motion thresholds.
- Sensor fusion.
- Time-series motion analysis.
- Wireless mobile application.
- Data logging and visualization.
- Improved noise and false-event rejection.

## Applications

- Multi-sensor motion monitoring research.
- Biomedical instrumentation prototypes.
- Embedded motion detection.
- Distributed I2C sensor systems.

## Medical Disclaimer

This is an experimental motion-sensing prototype, not a clinically validated fetal monitoring device. It cannot assess fetal wellbeing, diagnose fetal distress, or replace medical examination and professional fetal monitoring.

---

**Project Category:** ESP32 | Biomedical Instrumentation | Motion Sensing | I2C

**Status:** Working Prototype
