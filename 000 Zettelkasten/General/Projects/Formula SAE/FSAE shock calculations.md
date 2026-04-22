## Starting Values

- Total weight with driver: **650 lbs** (estimated off past cars)
- Weight distribution: **45% front / 55% rear** (estimated also)
- Front sprung corner weight: **116 lbs**
- Rear sprung corner weight: **149 lbs**
- Unsprung mass per corner: ~30 lbs (estimated)

---

## Frequency Formula

```
f = (1 / 2π) × √(K_wheel × 386.4 / W_sprung_corner)
```

Where:

- K_wheel = K_spring × MR² × cos²(θ)
- 386.4 = gravitational constant in in/s²

---

## Current Setup

**Front:** 200 lb/in spring, MR = 2.0

```
K_wheel = 200 × (2.0)² = 800 lb/in
f = (1/6.28) × √(800 × 386.4 / 116) = 8.21 Hz  ← way too stiff
```

**Rear:** 350 lb/in spring, MR = 1.0, 30° from vertical

```
K_wheel = 350 × (1.0)² × cos²(30°) = 350 × 0.75 = 262.5 lb/in
f = (1/6.28) × √(262.5 × 386.4 / 149) = 4.15 Hz ← kinda too stiff
```

5 before
6.5 after
20 to wheel


---

## New Setup

**Front:** 200 lb/in spring (keep), MR = 0.66 (redesign rocker)

```
K_wheel = 200 × (0.66)² = 87 lb/in
f = (1/6.28) × √(87 × 386.4 / 116) = 2.71 Hz  ✓
```

**Rear:** 200 lb/in spring (swap from 350), MR = 1.0, 30° from vertical

```
K_wheel = 200 × (1.0)² × cos²(30°) = 150 lb/in
f = (1/6.28) × √(150 × 386.4 / 149) = 3.14 Hz  ✓
```

---

## Summary

| Spring            | MR            | Wheel Rate | Frequency   |             |
| ----------------- | ------------- | ---------- | ----------- | ----------- |
| **Front current** | 200 lb/in     | 2.0        | 800 lb/in   | 8.21 Hz     |
| **Front new**     | 200 lb/in     | **0.66**   | 87 lb/in    | **2.71 Hz** |
| **Rear current**  | 350 lb/in     | 1.0        | 262.5 lb/in | 4.15 Hz     |
| **Rear new**      | **200 lb/in** | 1.0        | 150 lb/in   | **3.14 Hz** |



## New numbers

with nick on scales: 1 7/8 off ground
scales 1 1/4 tall

5/8" in ground clearance
3 3/8 spring length
7 in ground to wheel

