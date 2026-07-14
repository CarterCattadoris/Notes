# Design Review — CR6 DAQ Board (`daq_board`)

**Date:** 2026-07-14
**Reviewed files:** `daq_board.kicad_sch`, `daq_board.kicad_pcb` (on-disk saved state), `production/daq_board.zip` gerbers
**Analysis run:** `analysis/2026-07-14_1839/`

---

## Verdict

**Conditional pass — functionally sound, not yet clean for release.** The core design is solid: a well-structured 4-layer stackup with two dedicated inner ground planes, a correct 12 V → 3.3 V → 3.0 V power tree, and datasheet-verified pinouts on the parts checked. No board-killing defects were found. Before fabrication, resolve the **schematic↔PCB sync mismatch** (C2/C4), decide on the **MPN sourcing gap**, and confirm a handful of **layout ESD/return-path items**. Most analyzer "errors" are expected artifacts (RF shield courtyard, top-layer pour fragmentation) and are triaged below.

> ⚠️ **Review caveat:** git shows `daq_board.kicad_sch` modified and a newer `_autosave-daq_board.kicad_pcb` than the saved `.kicad_pcb`. This review reflects the **on-disk saved files**, not unsaved in-editor changes. Re-run after saving if the board has moved on.

---

## Overview

| | |
|---|---|
| Function | Automotive/motorsport data-acquisition board |
| Components | 91 (schematic) / 92 footprints (PCB) |
| Unique parts | 33 |
| Nets | 100 |
| Stackup | 4-layer: **L1 Top (sig) / L2 GND / L3 GND(+12V pour) / L4 Bottom (sig)** |
| Routing | Complete; 382 vias |
| Key ICs | ESP32-S3-WROOM-1U (MCU), ADS7038-Q1 (8-ch 12-bit ADC), ASM330LHBTR (IMU), NEO-M9N (GNSS), SN65HVD230 (CAN), LMR36015 (buck), TPS7A2030 (LDO) |

### Power tree (verified)

```
+12V (battery, fused: F1/F2)
  └─ BUCK1  LMR36015AQRNXRQ1  (12V → 3.3V buck, automotive Q1)
       └─ +3V3  ── ESP32-S3 (3V3), ASM330 IMU (Vdd/Vdd_IO), ADS7038 (AVDD+DVDD), SN65HVD230 (VCC), SD card
            └─ U3  TPS7A2030PDQNR  (3.3V → 3.0V ultra-low-noise LDO)
                 └─ +3V0 ── NEO-M9N GNSS (VCC), D_SEL
Backup: BT1 coin cell ── GPS V_BCKP (RTC/ephemeris keep-alive)
USB-C VBUS (5V) ── USB port, protected by U2 (USBLC6-2SC6)
```

**U3 (TPS7A2030) verified against datasheet extraction** (`datasheets/extracted/TPS7A2030PDQNR.json`): OUT→+3V0 (pin 1), GND (2), EN→+3V3 (3), IN→+3V3 (4), thermal pad→GND (5). Matches the DQN/X2SON pin table exactly. Input 3.3 V → output 3.0 V leaves **300 mV headroom vs 140 mV max dropout @ 300 mA** — valid. EN tied to +3V3 = always-on (internal 500 kΩ pulldown overridden), intentional.

---

## Analyzers run

| Analyzer | Status | Notes |
|---|---|---|
| `analyze_schematic.py` | ✅ | 55 findings (2 error, 22 warn, 31 info) |
| `analyze_pcb.py --full` | ✅ | 50 findings (8 error, 8 warn, 34 info) |
| `cross_analysis.py` | ✅ | 8 findings |
| `analyze_emc.py` | ✅ | 28 findings (12 error, 10 warn, 6 info) |
| `analyze_thermal.py` | ✅ | 0 findings — no significant dissipators (buck/LDO at low current) |
| `analyze_gerbers.py` | ✅ | 1 warn (paste ratio, benign) |
| SPICE | ✅ | ngspice-42; 11 subcircuits, 10 pass, 1 warn (see Simulation below) |
| Lifecycle audit | ⏭️ **Skipped** | Needs network + analyzer recognition of the `Mfg Part #` field (MPNs are present) |
| Deep Review (per-IC) | ✅ Partial | Power path + supply-rating checks done vs datasheet extractions |

---

## Blockers & action items

| # | Severity | Item | Detail | Action |
|---|---|---|---|---|
| 1 | **Warning** | C2/C4 value mismatch | Schematic = **100n**, PCB = **220n** (both +12V bypass). Real sch↔PCB sync gap; BOM (from schematic) would be wrong. | Reconcile the two; re-annotate + update BOM. Functionally either works. |
| 2 | ~~Warning~~ **Resolved / false positive** | SS-001 / DS-003 "no MPN" | ~~0/33 parts carry an MPN~~ **Incorrect.** MPNs are present under the `Mfg Part #` property (108 instances). The analyzer missed them: it lowercases property keys but doesn't strip punctuation, so `Mfg Part #` → `mfg part #`, which doesn't match its lookup key `mfg part`. No action needed on the design; the tooling gap is the analyzer's, not the board's. |
| 3 | **Verify** | ESD ground vias (ES-002) | D4/D5 (ESDS304 on microSD `SD_CMD`/`SD_DAT`/`SD_DETA`) flagged with no GND via near the device. ESD clamps need a short, low-inductance ground return. | Confirm a GND via sits immediately at each ESD array's GND pad. |
| 4 | **Verify** | Clock/SPI return path (RP-002) | SCLK/MOSI cross gaps in the **top-layer** GND pour. Mitigated by the solid L2 GND plane directly beneath (see triage), but worth a visual confirm that no via transition strands the return. | Spot-check SCLK/MOSI vias land near GND stitching; likely fine. |
| 5 | **Observation** | ADC reference on switching rail | ADS7038 AVDD (= ADC reference) is on **+3V3 (buck)**, while the clean **+3V0 LDO** powers the GPS. For a 12-bit DAQ ADC, buck ripple on AVDD limits effective resolution. | Confirm this is intentional. If ADC accuracy matters, consider referencing AVDD to +3V0 or using the ADS7038 internal reference with good DECAP filtering. |

---

## Verification basis

Claims marked "verified" rest on the structured datasheet extractions created this session (`datasheets/extracted/*.json`, 10 ICs, schema-validated + self-consistency checked), cross-referenced against the analyzer pin-to-net data:

- **U3 TPS7A2030** — full pinout + dropout/headroom math (above). ✅ datasheet-backed.
- **U1 ESP32-S3** — 3V3 supply within 3.0–3.6 V rating. ✅ datasheet-backed.
- **U4 ASM330LHBTR** — Vdd/Vdd_IO on +3V3, within 1.71–3.6 V rating. ✅ datasheet-backed.
- **ADC1 ADS7038-Q1** — AVDD/DVDD 3.3 V within 2.35–5.5 V. ✅ datasheet-backed (see Observation #5).
- **GPS1 NEO-M9N** — VCC on +3V0 (2.7–3.6 V ✓); V_BCKP fed by BT1 coin cell (intended). ✅ datasheet-backed.

Parts **not** individually deep-verified: LMR36015 buck (BUCK1) — not in the extraction set; SN65HVD230 CAN transceiver pin-map (extracted but not pin-traced here); passives.

---

## False positives triaged (do not act on these)

| Finding | Why it's a false positive |
|---|---|
| PM-001 ×8 courtyard overlaps with **J3** | J3 is `RFShield_TwoPieces` — an **RF shield can**. The GPS-section parts (C22–C26, D3, L2, R24, R26) are *meant* to sit under it. Intentional. |
| DC-002 "no decoupling near **U2**" | U2 is the **USBLC6-2SC6 ESD array** — no power pin, needs no decoupling cap. |
| PP-001 "**GPS1.22 V_BCKP** no DC path to rail" | V_BCKP is powered by **BT1 backup coin cell** (net `GPSVBCKP`); the 2-hop BFS rejects the series cap edge and doesn't treat BT1 as a rail. Correct backup-supply topology. |
| PS-002 / RP-002 / GP-001 GND "plane split, 10 islands" | Island analysis: **1 island = 392 pads** (the real GND, spanning all 4 layers incl. both inner planes); the other 9 are 1–3-pad pockets in the **top-layer** GND pour, which is fragmented by dozens of per-net signal zones. The functional reference (L2/L3 GND planes) is intact. Downgrade from "error." |
| GR-004 paste 46% of copper | Normal — THT pads, vias, test points, mounting holes get no paste. |

---

## Design strengths

- **Two dedicated inner GND planes** (L2 + L3) on a 4-layer stack — excellent return-path environment.
- **Clean analog supply chain**: ultra-low-noise TPS7A20 LDO dedicated to the noise-sensitive GNSS receiver.
- **GNSS backup battery** on V_BCKP for warm-start.
- **ESD protection** on all external ports: USBLC6 on USB-C, ESDS304 arrays on microSD, TVS on 12 V input.
- **Automotive-grade** buck (LMR36015-Q1) and ADC (ADS7038-Q1) — appropriate for a motorsport DAQ.
- **RF shield** over the GPS front-end.

---

## Simulation verification (ngspice-42)

11 subcircuits simulated — **10 pass, 1 warn**:

- **Buck feedback divider R6/R7 → 0.9955 V** ≈ LMR36015 1.0 V reference → confirms **+3V3 rail** (1.0 V ÷ 0.3017 = 3.31 V). Datasheet-independent.
- RC filters (R26/C26 @159 kHz, R3/C3 @15.9 Hz), decoupling networks, inrush (+3V0 settles to 3.0 V), and rail-clamp protection (D2 @12 V, D3 @3.3 V) all pass.
- **Warn:** GPS-section LC filter (L2 27 nH / C26) shows Q≈116, +40 dB peak at 3.06 MHz. This is the standard *ideal-inductor-no-DCR* SPICE artifact — real ferrite/inductor loss damps it. Confirm L2's series resistance/damping, but not expected to be a real resonance.

## Per-pin trace verification (critical parts)

Three-way cross-check: symbol-library pin numbering ↔ datasheet package pinout ↔ schematic net assignment.

### BUCK1 — LMR36015AQRNXRQ1 (12→3.3 V buck) — ✅ PASS
All 12 pins match the datasheet (RNX VQFN-HR) by number: PGND(1,11)→GND, VIN(2,10)→+12V, BOOT(4)→BUCKBOOT, VCC(5)→BUCKVCC (1µF), AGND(6)→GND, FB(7)→BUCKFB (R6/R7 divider, SPICE→3.31 V), SW(12)→BUCKSW.
- **PG(8)→GND**: power-good is open-drain and unused; the datasheet explicitly permits grounding PG when unused. Not a fault.
- **EN(9)→+12V**: always-on; datasheet permits tying EN directly to VIN.
- **NC(3)** unconnected in schematic — acceptable (no internal connection).

### USB1 — USB4105-GF-A (USB-C receptacle) — ✅ PASS
Symbol pin numbering matches the datasheet. D+ (A6/B6) and D− (A7/B7) route through U2 (USBLC6) ESD protection between connector and MCU; secondary pair tied to primary (correct for USB 2.0, orientation-independent). CC1(A5)/CC2(B5) each have a **5.11 kΩ Rd pulldown (R9/R8)** = correct UFP/sink role.
- **All four VBUS pins (A4/A9/B4/B9) → NO_CONNECT**: intentional — board is self-powered from +12 V; USB is data/programming only. Valid.
- **Low-priority note:** the USBLC6 VBUS clamp pin (U2.5) is also floating. Data-line ESD clamping still works via the internal TVS; tying VBUS to a rail would be marginally better, but there is no VBUS rail here.

### Sensor SPI bus (ESP32 ↔ ADS7038 ↔ ASM330) — ✅ PASS
- SCLK: ESP32 IO13 →R2→ ADC1.13 + U4.13 (shared, series-terminated)
- MOSI: ESP32 IO12 →R1→ ADC1.14 (SDI) + U4.14 (SDI, series-terminated)
- MISO: ESP32 IO14 ← R22/R23 (per-peripheral isolation) ← ADC/IMU SDO
- **CS lines distinct** — ADC_CS = IO21→R4→ADC1.11; IMU_CS = IO47→R5→U4.12. No CS conflict.
- **SD card on a separate SDIO bus** (GPIO43/44), not on the sensor SPI bus — no contention.
- All ESP32-S3 GPIOs valid; SPI via GPIO matrix (~40 MHz cap, ample for both sensors).

## Component lifecycle & temperature audit

Ran against the automotive −40/125 °C range. **Temperature: 0 violations.** **Lifecycle: inconclusive** — all 30 unique MPNs returned `unknown` (LC-004) because only the no-auth LCSC source was reachable and it doesn't expose lifecycle status. No part came back EOL/NRND, but that is *absence of evidence*, not confirmation of active status. A real verdict needs DigiKey/Mouser/element14 API credentials.

## Not performed / limits

- **Per-pin trace of remaining parts** — SN65HVD230 (CAN), NEO-M9N (GPS), microSD, and passives not exhaustively traced (extractions exist for the ICs; SD/GPS pinouts spot-checked only).
- **Lifecycle status** — inconclusive without a credentialed distributor API (see above).
- **Lifecycle/obsolescence audit** — skipped (no MPN properties, needs distributor API/network). Re-run after adding MPNs.
- **Prior-review delta** — none; this is the first recorded review (`analysis/manifest.json` had no prior runs).
- **Deep pin-map verification** limited to the power path + supply ratings. A full per-pin trace of the ESP32 (41 pads), ADS7038 SPI bus, and CAN transceiver against datasheets was not exhaustively performed — recommended before release given the analyzer relies on the (custom `CitrusSymbols`) library pinouts, which are the potential source of a consistency-invisible error.
- Analysis reflects **saved on-disk files**; unsaved editor state (autosave PCB is newer) not included.