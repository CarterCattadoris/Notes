**Group Members:** Carter, Lucas Le, Jon-Micheal Gonzalez  
**Course:** CSE 398 Junior Design — Spring 2026  
**Week 4:** Apr 7–13

---

## Hardware Used

|Name|Role|
|---|---|
|Raspberry Pi 5|Ground station — CV pipeline, Flask dashboard, path planning|
|USB Webcam|Overhead video feed for YOLO detection|
|ESP32-S3 DevKitC-1 (WROOM-2)|Vehicle MCU — motor control via WiFi UDP|
|L298N Motor Driver|Dual H-bridge for 2WD differential drive|
|2WD Robot Chassis|Vehicle platform with DC gear motors and caster wheel|
|4x AA Battery Pack|Motor power supply (~6V)|
|Buck Converter|Steps 6V battery down to 5V for ESP32 power|
|Laptop|Dashboard client, ESP32 programming, UDP testing|

---

## Summary of Work

This week focused on motor control firmware hardening, power system debugging, motor command protocol finalization, and ground station integration with obstacle avoidance path planning.

---

## 1. Motor Control Firmware — Debugging & Refactoring

**Owner: Carter**

### Motor Direction Inversion Fix

After assembling the car, discovered that both motors were physically wired in reverse — sending a "forward" command caused the car to drive backward. No physical space to swap the motor wires, so the fix was applied in firmware by inverting the direction logic in `set_single_motor()`. Forward commands now set IN2/IN4 HIGH (opposite of standard L298N convention), and reverse commands set them LOW. Verified correct forward/reverse/turn behavior via UDP test commands.

### Motor Command Format Refactor (Signed Floats)

Completed the protocol migration from `{"left": 0.5, "right": 0.7, "dir": 1}` to per-motor signed floats: `{"left": 0.5, "right": -0.3}`. This enables true differential drive where each motor's speed and direction are independent — critical for PID-controlled turns and spin-in-place maneuvers. Changes spanned multiple files:

- **command.h** — Removed `dir` field from `motor_cmd_t`. Left and right are now signed floats (-1.0 to 1.0).
- **command.c** — Updated `command_update()` signature to drop `dir` parameter.
- **udp.c** — Updated JSON parsing to read only `left` and `right` fields. Removed stale `D=%d` format string that referenced the deleted `dir` variable.
- **motor.h** — Updated `motor_set()` signature to `motor_set(float left, float right)`.
- **motor.c** — Refactored `motor_set()` to use a per-motor helper function `set_single_motor()` that handles direction and duty independently per motor based on the sign of each float.

### Deadband Implementation

Discovered that the motors were drifting when receiving `{"left": 0.0, "right": 0.0}` — small float imprecision or noise in the command pipeline resulted in nonzero duty cycles. Implemented a ±0.05 deadband in `set_single_motor()` using `fabsf()`: any command within the deadband is treated as zero, setting duty to 0 and pulling the direction pin LOW. Eliminated all motor drift at idle.

### Power System Debugging

Worked through several power-related issues during hardware integration:

- **L298N 5V regulator insufficient for ESP32:** Initially attempted to power the ESP32 from the L298N's onboard 78M05 regulator (measured 4.8V output). The ESP32 would boot but motors wouldn't respond — motor current draw caused battery voltage sag, dropping the regulator output below the ESP32's stable operating threshold, causing brownouts. Solution: dedicated buck converter set to 5V powering the ESP32 independently from the same battery pack.
- **Common ground requirement:** Identified that disconnecting the shared ground between the L298N and ESP32 caused total loss of motor control — GPIO signals had no reference voltage. Ensured GND is always bridged between both boards.
- **Development vs. deployment power:** Established workflow of using USB power during development (flash/monitor) and buck converter for untethered Demo Day operation. Documented that USB and 5V pin should never be connected simultaneously.

### UDP End-to-End Motor Testing

Verified full command pipeline: Python script on laptop → WiFi UDP → ESP32 parsing → motor output. Tested forward, reverse, differential turns, and variable speed. Confirmed commands are received and logged correctly in serial monitor, and motors respond as expected.

---

## 2. Ground Station — Integration & Path Planning

**Owner: Lucas Le**

### PID Tuning Adjustments

Refined the PID autopilot controller parameters to improve driving stability:

- Added integral gain (KI) to eliminate steady-state errors where the car would consistently undershoot or offset from the target path.
- Tuned derivative gain (KD) and fixed division logic to dampen oscillations — the car was previously overshooting and overcorrecting in a feedback loop during turns and approach.

### IMU Sensor Fusion

Implemented heading estimation by fusing the MPU6050's Z-axis gyroscope data with YOLO's velocity vector:

- Gyroscope provides smooth, high-rate yaw tracking even during in-place pivots where CV velocity vectors are unreliable.
- YOLO velocity vectors provide bounded drift correction, preventing gyro integration error from accumulating over time.
- Blending keeps heading accurate during both straight-line driving and rotational maneuvers.

### A* Path Planning & Obstacle Avoidance

Implemented A* pathfinding for autonomous navigation around obstacles in the demo arena:

- Obstacles detected via YOLO are mapped into a grid representation of the arena.
- A* computes a collision-free path from the car's current position to the docking target.
- Navigation routes are updated dynamically as the car moves and obstacle positions are refined.

### Ground Calibration for Object Detection

Calibrated the overhead camera's pixel-to-world coordinate mapping to ensure accurate position tracking. This establishes the transformation between the webcam's image plane and the physical 2x2m arena, allowing YOLO bounding box centers to be converted to real-world coordinates for the PID controller.

### Dynamic CV Mapping & Dashboard Visualization

Extended the dashboard to render navigation data directly into the MJPEG video stream:

- Path planning routes from A* are drawn as overlays on the live camera feed.
- Real-time visualization of the planned path, car position, and target location visible to the operator in the browser dashboard.

---

## 3. Dashboard & Documentation

**Owner: Jon-Micheal Gonzalez**

### Differential Mixing Constraints

Overhauled the differential drive mixing logic:

- Removed reverse-driving logic that was corrupting spatial coordinate tracking — driving backward inverted the relationship between motor commands and world-space position, breaking the PID controller's assumptions.
- Replaced reverse driving with pure pivoting (spin-in-place) for reorientation maneuvers. The car now only drives forward, using differential pivot turns to face the correct heading before proceeding.

---

## Current Firmware Status

|Module|File|Status|
|---|---|---|
|WiFi Station Mode|wifi.c / wifi.h|✅ Complete|
|UDP Listener|udp.c / udp.h|✅ Complete|
|Command State (mutex)|command.c / command.h|✅ Complete|
|Motor PWM Driver|motor.c / motor.h|✅ Complete|
|Motor Task (FreeRTOS)|motor_task in motor.c|✅ Complete|
|IMU (MPU6050 I2C)|imu.c / imu.h|TODO|
|Watchdog Failsafe|watchdog.c / watchdog.h|TODO|

---

## Next Week Plan (Apr 14–20) — Final Week Before Demo

- **Carter:** implement watchdog failsafe task (500ms timeout), final integration testing.
- **Lucas:** Finalize obstacle avoidance path planning, YOLO model retraining with fully assembled car, end-to-end autonomous docking test.
- **Jon-Micheal:** PID tuning for reliable docking, demo arena construction, poster design, demo rehearsal.
- **All:** Full system integration testing, demo script rehearsal, poster submission (due Apr 20).