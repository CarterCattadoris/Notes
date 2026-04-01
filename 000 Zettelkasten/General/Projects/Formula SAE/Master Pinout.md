202603302226
Status: #idea
Tags:[[Formula SAE]]

Maybe free wire colors (verify):
white/green??
blue/black
blue/gray
blue/green (used)
blue/orange (used)
blue/red (used)
brown/white (used)

NEED TO DO:
choose wire color for fan switch from ecu -> pdm (brown/white)


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
| V   | Pneumatic Positive             | white/purple | TBD                     | TBD    |
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

## Discrepancies & Missing Information

### 🔴 High Priority

- **No specific ECU/PDM pin numbers documented.** Connector docs reference generic buses ("sensor 0v B", "sensor 5v B", "PDM output 2/3/9") but never specify actual ECU or PDM header pin numbers. Awaiting pinout data.

- **Crank Position Sensor and Cam Position Sensor share identical wire colors.** Crank signal = white, cam signal = white. Crank 0v = white/blue, cam 0v = white/blue. These run in separate shielded cables so they're physically distinguishable, but if the shields are ever stripped back or wires are serviced loose, there's no way to tell crank from cam by color alone. Consider differentiating.

### 🟡 Medium Priority

1. **Gear Neutral Switch has no Power Plug pin.** It passes through Main Plug outer:C to the ECU but doesn't appear on the Power Plug at all. This implies the neutral wire only needs to reach the Main Plug (signal only, no power/ground through Power Plug) — confirm routing is correct.

2. **Main Plug inner 12ga pins a and c are unassigned.** Two empty 12ga positions available if future loads are needed.

3. **Power Plug outer pins T–X have wire colors but still need ECU/PDM destinations and branch assignments.** Pneumatic Upshift (yellow/blue), Pneumatic Downshift (yellow/brown), Pneumatic Positive (white/purple), Brake Positive (orange/red), Brake Negative (orange/black). These also need to be added to the branching diagram once routing is decided.

### ⚪ Low Priority

- **Coolant Temperature Sensor, Oil Temperature Sensor, and Intake Temperature Sensor are all 2-wire** (signal + 0v, no 5v). Correct for NTC thermistors with internal ECU pull-up — just confirm sensor types match.

- **Cam Position Sensor = 3 wires (signal, 5v, 0v); Crank Position Sensor = 2 wires (signal, 0v).** Implies Hall-effect cam and VR/reluctor crank. Confirm this matches actual sensor hardware.

- **Multiple sensors share orange/red for 5v and orange/black for 0v.** Fine if bussed to the same ECU rail, but document splice points per branch for troubleshooting.

- **Fuel Pump PDM wire listed as green** — gauge not explicitly stated in harness order (12ga implied by Main Plug inner ring grouping). Confirm.

---

## Wire Color Quick Reference

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

### Sensor Signals

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

### Sensor Power & Ground

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| Sensor 5v bus | orange/red | 20ga |
| Sensor 0v bus | orange/black | 20ga |
| Sensor 0v bus | orange/white | 20ga |

### Communication

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| CAN Lo (LTC Module) | blue | 22ga |
| CAN Hi (LTC Module) | green | 22ga |

### High-Current Power

| Wire Name | Color | Gauge |
|-----------|-------|-------|
| LTC Module PDM power | blue | 12ga |
| LTC Module battery − | black | 12ga |
| Fuel Pump PDM power | green | 12ga |
| Fuel Pump battery − | black | 12ga |

### Pneumatic Shift & Brake

| Wire Name               | Color        | Gauge |
| ----------------------- | ------------ | ----- |
| Pneumatic Upshift 12V   | yellow/blue  | 20ga  |
| Pneumatic Downshift 12V | yellow/brown | 20ga  |
| Pneumatic GND           | white/purple | 20ga  |
| Brake Positive          | orange/red   | 20ga  |
| Brake Negative          | orange/black | 20ga  |
