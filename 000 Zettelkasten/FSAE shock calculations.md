# Inputs
most were guesstimated based on past cars, or taken from car wen available

| Parameter                         | Value           |
| --------------------------------- | --------------- |
| Total weight with driver          | 650 lbs         |
| Weight distribution (F/R)         | 45% / 55%       |
| Front coilover spring rate        | 200 lb/in       |
| Front motion ratio (spring/wheel) | 2.0             |
| Rear coilover spring rate         | 350 lb/in       |
| Rear motion ratio (spring/wheel)  | 1.0             |
| Rear shock angle from vertical    | 30°             |
| Unsprung mass per corner (est.)   | 30 lbs          |
| TTX25 shock stroke                | 57 mm (2.24 in) |

---
## Corner Weights
again guessed for sprung vs unsprung

```
Front axle weight = 650 × 0.45 = 292.5 lbs
Rear axle weight  = 650 × 0.55 = 357.5 lbs

Front per corner  = 292.5 / 2 = 146.25 lbs
Rear per corner   = 357.5 / 2 = 178.75 lbs

Front sprung per corner = 146.25 − 30 = 116.25 lbs
Rear sprung per corner  = 178.75 − 30 = 148.75 lbs
```

---
## Current Setup

### Front
**Wheel rate:**

```
K_wheel = K_spring × MR²
K_wheel = 200 × (2.0)²
K_wheel = 200 × 4.0
K_wheel = 800 lb/in
```

**Ride frequency:**

```
f = (1 / 2π) × √(K_wheel / m)

where m = W_sprung / g = 116.25 / 386.4 = 0.3008 lb·s²/in

f = (1 / 6.2832) × √(800 / 0.3008)
f = (1 / 6.2832) × √(2659.6)
f = (1 / 6.2832) × 51.57
f = 8.21 Hz
```

**Static deflection/sag:**

```
δ = W_corner / K_wheel
δ = 146.25 / 800
δ = 0.183 in (4.6 mm)
```

**Available wheel travel (limited by shock stroke):**

```
Wheel travel = Shock stroke / MR
Wheel travel = 57 mm / 2.0
Wheel travel = 28.5 mm (1.12 in)
```

**Remaining bump travel after sag:**

```
Bump travel = 28.5 − 4.6 = 23.9 mm (0.94 in)
```

### Rear

**Effective wheel rate:**
measured roughly 30 degrees to vertical for rears

```
K_wheel = K_spring × MR² × cos²(θ)
K_wheel = 350 × (1.0)² × cos²(30°)
K_wheel = 350 × 1.0 × (0.8660)²
K_wheel = 350 × 0.75
K_wheel = 262.5 lb/in
```

**Ride frequency:**

```
m = 148.75 / 386.4 = 0.3849 lb·s²/in

f = (1 / 6.2832) × √(262.5 / 0.3849)
f = (1 / 6.2832) × √(681.7)
f = (1 / 6.2832) × 26.11
f = 4.15 Hz
```

**Static deflection (sag):**

```
δ = W_corner / K_wheel
δ = 178.75 / 262.5
δ = 0.681 in (17.3 mm)
```

**Available wheel travel:**

```
Wheel travel = Shock stroke / (MR × cos(θ))
Wheel travel = 57 / (1.0 × 0.866)
Wheel travel = 65.8 mm (2.59 in)
```

**Remaining bump travel after sag:**

```
Bump travel = 65.8 − 17.3 = 48.5 mm (1.91 in)
```

### Current Frequency Ratio

```
Ratio = f_front / f_rear = 8.21 / 4.15 = 1.98

Target ratio = 0.90 to 1.00 (rear equal or slightly higher than front)
Current ratio = 1.98 ← BADLY MISMATCHED
```

---

## Target Setup Calculations

### Design Targets

```
Front ride frequency:  2.7 Hz
Rear ride frequency:   3.0 Hz (rear ~10% higher than front)
Frequency ratio:       2.7 / 3.0 = 0.90 ✓
```

### Front

**Required wheel rate for 2.7 Hz:**

```
K_wheel = (2π × f)² × m
K_wheel = (2π × 2.7)² × 0.3008
K_wheel = (16.965)² × 0.3008
K_wheel = 287.8 × 0.3008
K_wheel = 86.6 lb/in
```

**Required MR (keeping 200 lb/in spring):**

```
K_wheel = K_spring × MR²
MR² = K_wheel / K_spring
MR² = 86.6 / 200
MR² = 0.433
MR = √(0.433)
MR = 0.658
```

**New front static deflection:**

```
δ = 146.25 / 87.1 = 1.68 in (42.7 mm)
```

**New front available wheel travel:**

```
Wheel travel = 57 / 0.66 = 86.4 mm (3.40 in)
```

**New front bump travel after sag:**

```
Bump travel = 86.4 − 42.7 = 43.7 mm (1.72 in) ✓
```

### Rear

**Required wheel rate for 3.0 Hz:**

```
K_wheel = (2π × 3.0)² × m
K_wheel = (18.85)² × 0.3849
K_wheel = 355.3 × 0.3849
K_wheel = 136.8 lb/in
```

**Required spring rate (keeping MR = 1.0, θ = 30°):**

```
K_spring = K_wheel / (MR² × cos²(θ))
K_spring = 136.8 / (1.0 × 0.75)
K_spring = 182.4 lb/in
```

**→ Nearest Hyperco: 175 lb/in or 200 lb/in**

**Verify with 200 lb/in spring:**

```
K_wheel = 200 × 1.0 × 0.75 = 150.0 lb/in

f = (1 / 6.2832) × √(150.0 / 0.3849)
f = (1 / 6.2832) × √(389.7)
f = (1 / 6.2832) × 19.74
f = 3.14 Hz ✓
```

**Verify with 175 lb/in spring:**

```
K_wheel = 175 × 1.0 × 0.75 = 131.25 lb/in

f = (1 / 6.2832) × √(131.25 / 0.3849)
f = (1 / 6.2832) × √(340.9)
f = (1 / 6.2832) × 18.47
f = 2.94 Hz ✓
```

**New rear static deflection (with 200 lb/in spring):**

```
δ = 178.75 / 150.0 = 1.19 in (30.2 mm)
```

**New rear bump travel (with 200 lb/in spring):**

```
Bump travel = 65.8 − 30.2 = 35.6 mm (1.40 in) ✓
```

---

## Before vs After Summary

|Parameter|Front (current)|Front (new)|Rear (current)|Rear (new, 200 lb/in)|
|---|---|---|---|---|
|Spring rate|200 lb/in|200 lb/in|350 lb/in|200 lb/in|
|Motion ratio|2.0|**0.66**|1.0|1.0|
|Shock angle|—|—|30°|30°|
|Wheel rate|800 lb/in|**87.1 lb/in**|262.5 lb/in|**150 lb/in**|
|Ride frequency|8.21 Hz|**2.71 Hz**|4.15 Hz|**3.14 Hz**|
|Static sag|4.6 mm|**42.7 mm**|17.3 mm|**30.2 mm**|
|Bump travel remaining|23.9 mm|**43.7 mm**|48.5 mm|**35.6 mm**|
|Freq ratio (F/R)|**1.98**||**0.86**||

---

## Formulas stolen from google

```
Wheel rate:          K_wheel = K_spring × MR² × cos²(θ)
Ride frequency:      f = (1/2π) × √(K_wheel × g / W_sprung_corner)
Static deflection:   δ = W_corner / K_wheel
Required spring:     K_spring = (2πf)² × (W_sprung / g) / (MR² × cos²(θ))
Required MR:         MR = √(K_wheel_target / K_spring)
Wheel travel:        Travel_wheel = Stroke_shock / (MR × cos(θ))
```