# Vault Reorganization Plan

## Objective
Reorganize `CSE`, `ELE`, and `General` directories to match the `CIS` structure (course-specific subfolders). Update all internal Wiki-links to reflect new paths.

## 1. Target Directory Structure

### CSE (`000 Zettelkasten/CSE`)
| Proposed Folder | Description/Keywords |
| :--- | :--- |
| `CSE 261 Digital Logic Design` | Gates, Boolean Algebra, K Maps, Latches, Flip Flops, FSM, Combinational/Sequential Logic. |
| `CSE 384 Systems & Network Programming` | `CSE 384.md`, low-level systems programming notes. |
| `CSE 381 Computer Architecture` | MIPS, CPI, Datapath, Assembly, Pipelining, `CSE 381.md`. |
| `CSE 486 Design Operating Systems` | *Existing folder* (`Design of OS`). Move contents here. |
| `CSE 398 Embedded & Mobile Systems` | *Existing folder* (`Embedded Systems`). Move embedded notes here. |
| `CSE 464 Intro to VLSI Design` | CMOS, Transistors, Inverter, Layout, Stick Diagrams, `VLSI Exam`, `Finfet`, `Moore vs Mealy`. |
| `PHY 212 General Physics II` | Basic Circuits (`Resistor`, `Capacitor`, `Ohm's Law`, `Voltage`, `Current`). |

### ELE (`000 Zettelkasten/ELE`)
| Proposed Folder | Description/Keywords |
| :--- | :--- |
| `ELE 251 Fundamentals of Linear Systems` | Laplace (Transform, Inverse), Transfer Function, Bode Plots, Signals, `Linear Systems (ELE251).md`. |
| `ELE 400 Deep Learning in Engrng Apps` | *Existing folder* (`Deep Learning`). Ensure all DL notes are inside. |


### General (`000 Zettelkasten/General`)
| Proposed Folder | Description/Keywords |
| :--- | :--- |
| `Meta` | `College.md`, `Sophomore.md`, `Engineering.md` (Personal/Career). |
| `Projects/Formula SAE` | Move `Formula SAE` into a `Projects` subfolder or keep as is. |

## 2. Execution Instructions (For LLM)

1.  **Create Directories**: Ensure all proposed folders exist.
2.  **Move Files**:
    *   Read file content if ambiguous (e.g., `Memory` could be OS or Arch).
    *   Move files to their respective course folders.
3.  **Update Links**:
    *   **CRITICAL**: Obsidian Wiki-links usually don't need path updates if filename is unique, BUT if you are using relative paths or strict linking, update them.
    *   *Self-Correction*: Obsidian auto-updates links when files move if using the app. Since we are doing this via CLI/LLM, we must **grep and replace** any links that heavily rely on paths, although standard `[[Note Name]]` works globally in Obsidian.
    *   **Update MOCs**: Update `CSE.md`, `ELE.md`, and `General.md` to link to the new subfolders or key MOC notes within those folders.

## 3. Progress Tracking & Resumability (CRITICAL)
To ensure another LLM can pick up if this process pauses:
1.  **Granular Logging**: Update `docs/CHANGELOG.md` frequently (e.g., after moving 3-5 files).
    - Example: `[IN-PROGRESS] Moved 5 logic gate files to CSE 261.`
2.  **Checkpointing**: If you stop, leave the log in a state where the next agent knows *exactly* what is pending.
3.  **Consolidation**: Once a full category (e.g., "All Digital Logic notes mapped") is complete, collapse the granular log entries into a single summary line:
    - Example: `[COMPLETED] Reorganized CSE 261 Digital Logic Design folder.`

## 4. Specific File Mappings

- **Move to `CSE 261 Digital Logic Design`**:
  - `AND Gate.md`, `OR gate.md`, `NOT Gate.md`, `NAND Gate.md`, `NOR Gate.md`
  - `Boolean Algebra*.md`, `De Morgan's Law.md`
  - `K Maps.md`, `Product of Sum K Map.md`
  - `Latch.md`, `D Latch.md`, `SR Latch.md`, `Flip Flop.md`
  - `Adders.md`, `Full Adder.md`, `Half Adder.md`
  - `FSM.md`, `Sequential Logic.md`, `Combinational Logic.md`

- **Move to `CSE 381 Computer Architecture`**:
  - `MIPS.md`, `CPI.md`
  - `CSE 381.md`
  - `comp arch final.md`

- **Move to `CSE 384 Systems & Network Programming`**:
  - `CSE 384.md`

- **Move to `CSE 464 Intro to VLSI Design`**:
  - `CMOS.md`, `CMOS Gates.md`, `Transistor.md`, `nMos.md`, `pMos.md`
  - `VLSI Final.md`, `vlsi practice exam.md`
  - `Stick Diagram.md` (if exists), `Inverter.md`

- **Move to `ELE 251 Fundamentals of Linear Systems`**:

  - `Laplace Transform*.md`, `Inverse Laplace*.md`
  - `Transfer Function.md`, `Steady State.md`, `Transient State.md`
  - `Dirac Delta function.md`, `Step Function.md`

## 4. Unidentified Files
If a file's location is ambiguous:
1.  Read the content.
2.  Check for "Tags" metadata.
3.  If still unsure, leave in root of `CSE` or `ELE` and add `#needs-sorting` tag.
