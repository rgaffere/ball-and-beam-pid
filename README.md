# ⚖️ Ball-and-Beam PID Controller

A real-time control systems project that uses a **PID controller** to balance a rolling ball on a tilting beam.  
Developed using **Simulink**, an **Arduino Mega 2560**, and a **Time-of-Flight (ToF) sensor**, this project demonstrates hardware-software co-design for stabilizing an inherently unstable mechanical system.

---

## 🎯 Project Goal

To design, build, and tune a closed-loop control system capable of maintaining a plastic ball at a specific horizontal position on an aluminum beam by dynamically adjusting the beam’s tilt.

---

## 🛠️ System Overview

- **Ball and Beam Mechanism**  
  - Aluminum beam, rolling ball, pivot mount
  - Servo motor tilts the beam to control ball position

- **Sensor & Control**  
  - VL53L0X Time-of-Flight sensor measures ball position
  - Arduino Mega 2560 runs Simulink-deployed PID control
  - PWM output drives 3001HB servo motor

- **Software**  
  - Simulink model reads sensor, applies PID, outputs PWM
  - Uses spike filtering and FIR smoothing to clean sensor data
  - PID tuning via real-time feedback using Simulink External Mode

---

## ⚙️ Materials Used

| Component                     | Purpose                              |
|------------------------------|--------------------------------------|
| Arduino Mega 2560            | Main controller                      |
| VL53L0X ToF Sensor           | Position sensing                     |
| 3001HB Servo Motor           | Beam actuation                       |
| Buck Converter               | Power regulation (12V → 5V)          |
| Breadboard + Jumpers         | Wiring interface                     |
| Custom Beam + PLA Mounts     | Mechanical setup                     |
| MATLAB / Simulink            | Modeling and control implementation  |

---

## 📊 Controller Design

- **Control Law**:  
  PID controller implemented with the following tuned parameters:
  - `Kp = 1.05`
  - `Ki = 0.0095`
  - `Kd = 0.15`

- **Sensor Filtering**:  
  - Spike clamping for outlier rejection  
  - FIR filter: `[0.2, 0.2, 0.2, 0.2, 0.2]`

- **Servo Output**:  
  - Biased control output (centered at 150°)
  - Saturated to [90°, 180°] range for reliable actuation

---

## ✅ Results

| Metric                | Result                     |
|-----------------------|----------------------------|
| Settling Time         | ~2–3 seconds               |
| Steady-State Error    | < ±1 cm                    |
| Overshoot             | Low to moderate (tunable)  |
| Setpoint Tracking     | Smooth, low delay          |
| Power Issues          | None observed              |

---

## 🧪 Key Takeaways

- Simulink External Mode allowed real-time tuning and observability
- Sensor filtering and servo backlash compensation were crucial
- Hands-on application of control theory under physical constraints
- Reinforced importance of noise handling and mechanical design in embedded systems

---

## 👨‍🔧 Authors

- **Ryan G** – [@rgaffere](https://github.com/rgaffere)  
- **Gibril T**

Project completed for **ENEE 461: Control Systems Lab**, Spring 2025  
University of Maryland, Department of Electrical and Computer Engineering
