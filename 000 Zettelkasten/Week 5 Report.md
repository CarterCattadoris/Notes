**Group Members:** Carter, Lucas Le, Jon-Micheal Gonzalez  
**Course:** CSE 398 Junior Design — Spring 2026  
**Week 5:** Apr 13–19

---

## Hardware Used

|Name|Role|
|---|---|
|Raspberry Pi 5|Ground station — CV pipeline, Flask dashboard, PID autopilot|
|USB Webcam|Overhead video feed for YOLO detection|
|ESP32-S3 DevKitC-1 (WROOM-2)|Vehicle MCU — motor control and IMU telemetry via WiFi UDP|
|L298N Motor Driver|Dual H-bridge for 2WD differential drive|
|MPU6050 IMU|6-axis gyroscope/accelerometer for heading data|
|2WD Robot Chassis|Vehicle platform with DC gear motors and caster wheel|
|4x AA Battery Pack|Motor power supply (~6V)|
|Buck Converter|Steps 6V battery down to 5V for ESP32 power|
|Laptop|Dashboard client, testing|

---

## Summary of Work

Final week before Demo Day (April 22). This week focused on PID tuning for reliable autonomous docking, retraining the YOLO model for the demo environment floor, dashboard UI polish, and adding calibration sequences to streamline setup on Demo Day.

---

## 1. PID Tuning & Autopilot Refinement

**Owners: Lucas Le, Jon-Micheal Gonzalez**

### PID Parameter Tuning

Continued iterative tuning of the PID autopilot controller to achieve consistent, reliable docking behavior:

- Fine-tuned proportional, integral, and derivative gains across both the steering and throttle control loops.
- Focused on reducing overshoot during the final approach phase where the car needs to slow down and align precisely with the docking target.
- Tested across multiple starting positions and orientations within the 2x2m arena to ensure robustness.

> **[SCREENSHOT: Dashboard showing car autonomously navigating to docking target with path overlay]**

---

## 2. YOLO Model Retraining for Demo Environment

**Owner: Lucas Le**

### New Model for Dark Blue Floor

The demo hallway outside the 3rd-floor elevator has a dark blue floor, which differs significantly from the lab environment where the original training data was collected. The existing model's detection confidence dropped on the new surface due to the change in background contrast.

- Collected a new dataset of the fully assembled car on the dark blue floor under the hallway lighting conditions.
- Annotated and trained a new YOLOv11n model at 416×416 resolution via Roboflow.
- Exported to NCNN and deployed on the Pi 5. Verified high-confidence detection on the demo surface.

> **[SCREENSHOT: YOLO detection output showing bounding box on car against dark blue floor]**

---

## 3. Dashboard UI Improvements

**Owner: Jon-Micheal Gonzalez**

### UI Cleanup & Polish

Improved the Flask/WebSocket dashboard for a cleaner, more presentable Demo Day experience:

- Streamlined the layout to reduce visual clutter and highlight key information: live video feed, telemetry readouts, and autopilot controls.
- Improved readability of real-time telemetry data (position, heading, speed, distance to target, PID state).
- Ensured the manual drive controls and autopilot toggle are prominent and intuitive for audience members to interact with during the demo.

> **[SCREENSHOT: Updated dashboard UI showing live feed with tracking overlay and telemetry panel]**

---

## 4. Calibration Sequences

**Owners: Lucas Le, Carter**

### Automated Calibration for Demo Setup

Added calibration sequences to streamline the system setup process, reducing manual configuration needed on Demo Day:

- Camera-to-world coordinate calibration: a guided sequence that maps pixel coordinates to physical arena positions, establishing the transformation matrix for accurate YOLO-to-real-world position tracking.
- IMU gyroscope bias calibration: automated startup routine on the ESP32 that samples the MPU6050 gyroscope at rest, averages the readings, and subtracts the bias from all subsequent measurements for clean heading data.

> **[SCREENSHOT: Dashboard showing calibration sequence in progress]**

---

## Current Firmware Status

|Module|File|Status|
|---|---|---|
|WiFi Station Mode|wifi.c / wifi.h|✅ Complete|
|UDP Listener|udp.c / udp.h|✅ Complete|
|Command State (mutex)|command.c / command.h|✅ Complete|
|Motor PWM Driver|motor.c / motor.h|✅ Complete|
|Motor Task (FreeRTOS)|motor_task in motor.c|✅ Complete|
|IMU (MPU6050 I2C)|imu.c / imu.h|✅ Complete|
|Watchdog Failsafe|watchdog.c / watchdog.h|✅ Complete|

---

## Demo Day Readiness (Apr 22)

- **Firmware:** All ESP32-S3 modules complete and tested — WiFi, UDP, motor control, IMU streaming, watchdog failsafe.
- **CV Pipeline:** YOLOv11n retrained for demo floor, deployed via NCNN on Pi 5 with real-time detection.
- **Autopilot:** PID controller tuned for reliable docking from multiple starting positions.
- **Dashboard:** Clean UI with live video overlay, manual controls, autopilot toggle, and telemetry display.
- **Calibration:** Automated sequences for camera mapping and IMU bias reduce setup time.
- **Networking:** Phone hotspot planned for Demo Day to avoid university WiFi device isolation.
- **Poster:** Due today (Apr 20).

### Demo Day Script

1. Webcam mounted overhead shows the 2x2m arena on the laptop dashboard.
2. Audience member manually drives the car using keyboard controls.
3. Car enters camera view — YOLO locks on with visible bounding box and path trail.
4. User presses "Autopilot" — car autonomously navigates to the docking target.
5. Dashboard displays real-time telemetry, path planning, and PID state throughout.