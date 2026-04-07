202603302226
Status: #idea
Tags:[[Formula SAE]]

Maybe free wire colors (verify):
white/green??
blue/black
blue/gray
## Firewall Connector Pin-Outs

### Power Plug — Inner Ring, 20ga

| Pin | Function                  | Wire Color   | ECU/PDM Destination | Branch |
| --- | ------------------------- | ------------ | ------------------- | ------ |
| h   | Coil 1 PDM return         | white/brown  | PDM (coil 1 output) | 5      |
| z   | Coil 2 PDM return         | white/orange | PDM (coil 2 output) | 5      |
| b   | Coil 3 PDM return         | black/gray   | PDM (coil 3 output) | 5      |
| d   | Coil 4 PDM return         | white/purple | PDM (coil 4 output) | 5      |
| f   | Oil Temperature Sensor 0v | orange/black | sensor 0v B         | 4      |

### Power Plug — Outer Ring, 20ga

| Pin | Function                       | Wire Color   | ECU/PDM Destination     | Branch |
| --- | ------------------------------ | ------------ | ----------------------- | ------ |
| A   | Oil Pressure Sensor 0v         | orange/black | sensor 0v B             | 4      |
| B   | Oil Pressure Sensor 5v         | orange/red   | sensor 5v B             | 4      |
| C   | Throttle Position Sensor 0v    | orange/black | sensor 0v B             | 4      |
| D   | Throttle Position Sensor 5v    | orange/red   | sensor 5v B             | 4      |
| E   | Injector 1 PDM return          | green/orange | PDM (injector 1 output) | 3      |
| F   | Injector 2 PDM return          | green/grey   | PDM (injector 2 output) | 3      |
| G   | Injector 3 PDM return          | green/blue   | PDM (injector 3 output) | 3      |
| H   | Injector 4 PDM return          | green/white  | PDM (injector 4 output) | 3      |
| J   | Intake Pressure Sensor 5v      | orange/red   | sensor 5v B             | 3      |
| K   | Intake Pressure Sensor 0v      | orange/black | sensor 0v B             | 3      |
| L   | Intake Temperature Sensor 0v   | orange/black | sensor 0v B             | 3      |
| M   | Sprocket Speed Sensor 0v       | orange/black | sensor 0v B             | 2      |
| N   | Sprocket Speed Sensor 5v       | orange/red   | sensor 5v B             | 2      |
| P   | Coolant Temperature Sensor 0v  | orange/white | sensor 0v B             | 2      |
| R   | Gear Position Sensor 5v pullup | orange/red   | sensor 5v B             | 2      |
| S   | Gear Position Sensor 0v        | orange/white | sensor 0v B             | 2      |
| T   | Pneumatic Upshift              | yellow/blue  | TBD                     | TBD    |
| U   | Pneumatic Downshift            | yellow/brown | TBD                     | TBD    |
| V   | Pneumatic Positive             | blue/black   | (change???)             | TBD    |
| W   | Brake Positive                 | orange/red   | TBD                     | TBD    |
| X   | Brake Negative                 | orange/black | TBD                     | TBD    |

### Main Plug — Inner Ring, 20ga

| Pin | Function | Wire Color | ECU/PDM Destination | Branch |
|-----|----------|------------|---------------------|--------|
| h | Crank Position Sensor 0v | white/blue | sensor 0v B | 4 |
| z | Crank Position Sensor signal | white | ECU crank input | 4 |
| b | Cam Position Sensor 0v | white/blue | sensor 0v B | 5 |
| d | Cam Position Sensor signal | white | ECU cam input | 5 |
| f | Cam Position Sensor 5v | white/red | sensor 5v B | 5 |

### Main Plug — Inner Ring, 12ga

| Pin | Function             | Wire Color | ECU/PDM Destination | Branch |
| --- | -------------------- | ---------- | ------------------- | ------ |
| i   | LTC Module PDM power | blue 12ga  | PDM output 9        | 4      |
| Y   | LTC Module battery − | black 12ga | battery −           | 4      |
| a   | **UNASSIGNED**       | —          | —                   | —      |
| c   | **UNASSIGNED**       | —          | —                   | —      |
| e   | Fuel Pump PDM power  | green 12ga | PDM output 3        | 1      |
| g   | Fuel Pump battery −  | black 12ga | battery −           | 1      |

### Main Plug — Outer Ring

| Pin | Function                          | Wire Color    | ECU/PDM Destination     | Branch |
| --- | --------------------------------- | ------------- | ----------------------- | ------ |
| A   | Coolant Temperature Sensor signal | yellow/white  | ECU coolant temp input  | 2      |
| B   | Gear Position Sensor signal       | orange/grey   | ECU gear position input | 2      |
| C   | Gear Neutral Switch               | yellow/grey   | ECU neutral input       | 2      |
| D   | Sprocket Speed Sensor signal      | orange/green  | ECU speed input         | 2      |
| E   | Injector 1 signal                 | white #5      | ECU injector 1 driver   | 3      |
| F   | Injector 2 signal                 | white #6      | ECU injector 2 driver   | 3      |
| G   | Intake Pressure Sensor signal     | orange/yellow | ECU MAP input           | 3      |
| H   | Intake Temperature Sensor signal  | yellow/red    | ECU IAT input           | 3      |
| J   | Injector 3 signal                 | white #7      | ECU injector 3 driver   | 3      |
| K   | Injector 4 signal                 | white #8      | ECU injector 4 driver   | 3      |
| L   | Throttle Position Sensor signal   | yellow/black  | ECU TPS input           | 4      |
| M   | Oil Pressure Sensor signal        | orange/blue   | ECU oil pressure input  | 4      |
| N   | Oil Temperature Sensor signal     | yellow/purple | ECU oil temp input      | 4      |
| P   | CAN Lo (LTC Module)               | blue 22ga     | ECU/CAN bus Lo          | 4      |
| R   | CAN Hi (LTC Module)               | green 22ga    | ECU/CAN bus Hi          | 4      |
| S   | Coil 1 igniter signal             | white #1      | ECU ignition 1 driver   | 5      |
| T   | Coil 2 igniter signal             | white #2      | ECU ignition 2 driver   | 5      |
| U   | Coil 3 igniter signal             | white #3      | ECU ignition 3 driver   | 5      |
| V   | Coil 4 igniter signal             | white #4      | ECU ignition 4 driver   | 5      |
| W   | **SPARE — unassigned**            | —             | —                       | —      |
| X   | **SPARE — unassigned**            | —             | —                       | —      |

---

## Front Harness

### Front Harness Wire List

| Wire Name                      | Color        | Notes                                  |
| ------------------------------ | ------------ | -------------------------------------- |
| Sensor 5v B                    | white/red    | Front brake pressure sensor supply     |
| Sensor 0v B                    | green/black  | Front brake pressure sensor ground     |
| Front Brake Pressure signal    | green/gray   |                                        |
| Rear Brake Pressure signal     | green/orange |                                        |
| CAN Hi                         | green        |                                        |
| CAN Lo                         | blue         |                                        |
| Launch Switch                  | white/blue   |                                        |
| Anti Lag Switch                | green/purple |                                        |
| Starter Button Return          | white/green  |                                        |
| Cockpit Kill (and BOTS) Return | white/brown  |                                        |
| Dash PDM 12v                   | blue/red     |                                        |
| GND                            | black        | To chassis, not routed through harness |
| Upshift Paddle                 | blue/orange  |                                        |
| Downshift Paddle               | green/blue   |                                        |
| Brake Switch                   | blue/gray    |                                        |
| Fuel Pump Switch               | white/orange |                                        |
| Inj/Ign Enable Switch          | blue/brown   |                                        |
| Fan Override Switch            | white/purple |                                        |
| PDM 0v                         | white/black  |                                        |
| PDM 0v                         | blue/green   |                                        |

### PDM ↔ ECU Link

| Wire Name | Color | Notes |
|-----------|-------|-------|
| ECU Fan Switch | brown/white | |
| ECU 12v | brown | |

### Connector Hub → Dash

| Wire Name                 | Color         |
| ------------------------- | ------------- |
| Wheel DRS Button          | yellow/green  |
| Dash Back Button          | orange/green  |
| GND                       | black         |
| Dash Encoder DT           | yellow/white  |
| GND                       | black         |
| Dash Potentiometer Signal | orange/grey   |
| Dash Shift Light PWM      | yellow/purple |
| Dash Encoder CLK          | orange/yellow |
| Dash Menu Button          | yellow/red    |
| Riverdi 3.3v              | orange/blue   |
| Dash Encoder SW           | orange/white  |

---

## Wire Color Quick Reference (Full Car)

### Ignition Signal (ECU → Coil Igniters)

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Coil 1 igniter signal | white #1 | 20ga |
| Coil 2 igniter signal | white #2 | 20ga |
| Coil 3 igniter signal | white #3 | 20ga |
| Coil 4 igniter signal | white #4 | 20ga |

### Injection Signal (ECU → Injectors)

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Injector 1 signal | white #5 | 20ga |
| Injector 2 signal | white #6 | 20ga |
| Injector 3 signal | white #7 | 20ga |
| Injector 4 signal | white #8 | 20ga |

### Ignition Power (PDM → Coils)

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Coil 1 PDM return | white/brown | 20ga |
| Coil 2 PDM return | white/orange | 20ga |
| Coil 3 PDM return | black/gray | 20ga |
| Coil 4 PDM return | white/purple | 20ga |

### Injection Power (PDM → Injectors)

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Injector 1 PDM return | green/orange | 20ga |
| Injector 2 PDM return | green/grey | 20ga |
| Injector 3 PDM return | green/blue | 20ga |
| Injector 4 PDM return | green/white | 20ga |

### Engine Sensor Signals

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Crank Position Sensor signal | white (shielded) | 20ga |
| Crank Position Sensor 0v | white/blue (shielded) | 20ga |
| Cam Position Sensor signal | white (shielded) | 20ga |
| Cam Position Sensor 5v | white/red (shielded) | 20ga |
| Cam Position Sensor 0v | white/blue (shielded) | 20ga |
| Throttle Position Sensor signal | yellow/black | 20ga |
| Oil Pressure Sensor signal | orange/blue | 20ga |
| Oil Temperature Sensor signal | yellow/purple | 20ga |
| Intake Pressure Sensor signal | orange/yellow | 20ga |
| Intake Temperature Sensor signal | yellow/red | 20ga |
| Sprocket Speed Sensor signal | orange/green | 20ga |
| Coolant Temperature Sensor signal | yellow/white | 20ga |
| Gear Position Sensor signal | orange/grey | 20ga |
| Gear Neutral Switch | yellow/grey | 20ga |

### Engine Sensor Power & Ground

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Sensor 5v bus | orange/red | 20ga |
| Sensor 0v bus | orange/black | 20ga |
| Sensor 0v bus | orange/white | 20ga |

### Pneumatic Shift & Brake (Engine Harness)

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Pneumatic Upshift | yellow/blue | 20ga |
| Pneumatic Downshift | yellow/brown | 20ga |
| Pneumatic Positive | white/purple | 20ga |
| Brake Positive | orange/red | 20ga |
| Brake Negative | orange/black | 20ga |

### Communication

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| CAN Lo | blue | 22ga |
| CAN Hi | green | 22ga |

### High-Current Power

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| LTC Module PDM power | blue | 12ga |
| LTC Module battery − | black | 12ga |
| Fuel Pump PDM power | green | 12ga |
| Fuel Pump battery − | black | 12ga |
### PDM ↔ ECU

| Wire Name      | Color       | Gauge |
| -------------- | ----------- | ----- |
| ECU Fan Switch | brown/white | 20ga  |
| ECU 12v        | brown       | 16ga  |

### Front Harness — Brake Pressure Sensors

| Wire Name                   | Color        | Gauge |
| --------------------------- | ------------ | ----- |
| Sensor 5v B (front brake)   | white/red    | 20ga  |
| Sensor 0v B (front brake)   | green/black  | 20ga  |
| Front Brake Pressure signal | green/gray   | 20ga  |
| Rear Brake Pressure signal  | green/orange | 20ga  |

### Front Harness — Driver Switches & Inputs

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Launch Switch | white/blue | 20ga |
| Anti Lag Switch | green/purple | 20ga |
| Starter Button Return | white/green | 20ga |
| Cockpit Kill (and BOTS) Return | white/brown | 20ga |
| Upshift Paddle | blue/orange | 20ga |
| Downshift Paddle | green/blue | 20ga |
| Brake Switch | blue/gray | 20ga |
| Fuel Pump Switch | white/orange | 20ga |
| Inj/Ign Enable Switch | blue/brown | 20ga |
| Fan Override Switch | white/purple | 20ga |

### Front Harness — Power & Ground

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Dash PDM 12v | blue/red | 20ga |
| PDM 0v | white/black | 20ga |
| PDM 0v | blue/green | 20ga |
| GND (chassis) | black | — |

### Front Harness — Dash Connector Hub

| Wire Name                 | Color         | Gauge |
| ------------------------- | ------------- | ----- |
| Wheel DRS Button          | yellow/green  | 20ga  |
| Dash Back Button          | orange/green  | 20ga  |
| Dash Encoder DT           | yellow/white  | 20ga  |
| Dash Potentiometer Signal | orange/grey   | 20ga  |
| Dash Shift Light PWM      | yellow/purple | 20ga  |
| Dash Encoder CLK          | orange/yellow | 20ga  |
| Dash Menu Button          | yellow/red    | 20ga  |
| Riverdi 3.3v              | orange/blue   | 20ga  |
| Dash Encoder SW           | orange/white  | 20ga  |