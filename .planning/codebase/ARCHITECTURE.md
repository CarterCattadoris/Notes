# Architecture

**Analysis Date:** 2025-01-31

## Pattern Overview

**Overall:** Hierarchical Zettelkasten with Maps of Content (MOCs).

**Key Characteristics:**
- **Atomic Notes:** Focused on a single concept, tagged with `#idea`.
- **Structural Hubs:** MOCs (Maps of Content) aggregate and organize related atomic notes, tagged with `#MOC`.
- **Numbered Root Folders:** High-level organization follows a 3-digit prefix system (e.g., `000`, `111`).
- **Subject-Based Partitioning:** Within the Zettelkasten, content is partitioned by academic department or general category.

## Layers

**Organization Layer:**
- Purpose: Defines the vault's structure and metadata standards.
- Location: `444 Docs/` and `333 Templates/`
- Contains: `vault_documentation.md`, `MOC.md` template.
- Depends on: None.
- Used by: All note-taking processes.

**Navigation Layer (MOCs):**
- Purpose: Provides entry points into specific subjects and courses.
- Location: Top-level subject folders in `000 Zettelkasten/` (e.g., `000 Zettelkasten/CIS/CIS.md`).
- Contains: Lists of course MOCs and topical links.
- Depends on: Knowledge Layer.
- Used by: The user to navigate the vault.

**Knowledge Layer (Atomic Notes):**
- Purpose: Stores the actual conceptual information.
- Location: Nested course/topic folders (e.g., `000 Zettelkasten/CSE/Digital Logic Design/*.md`).
- Contains: `#idea` notes with concise explanations, formulas, and diagrams.
- Depends on: References and External sources.
- Used by: MOCs for aggregation.

## Data Flow

**Knowledge Integration Flow:**

1. **Capture:** Raw information enters via `Lecture Notes/`, `Homework/`, or `111 Reference/`.
2. **Atomization:** Concepts are extracted and formatted into `#idea` notes using the `Core Zettel Idea.md` template.
3. **Linking:** New notes are linked to relevant "Tags" (which are actually other notes) and added to a parent `#MOC`.
4. **Refinement:** MOCs are updated to reflect the new structure or relationship between concepts.

**State Management:**
- **Status Tags:** Notes use `#idea` or `#MOC` to define their functional role.
- **Timestamp IDs:** Every note begins with a unique temporal ID (e.g., `202501231549`) for identification and linking stability.

## Key Abstractions

**Map of Content (MOC):**
- Purpose: Acts as a table of contents or hub for a specific area.
- Examples: `000 Zettelkasten/CIS/CIS.md`, `000 Zettelkasten/CSE/CSE.md`.
- Pattern: Lists of wikilinks to sub-MOCs or atomic notes.

**Atomic Idea:**
- Purpose: Represents a single, irreducible concept.
- Examples: `000 Zettelkasten/CSE/Digital Logic Design/Full Adder.md`.
- Pattern: Header with ID, Status, and Tags, followed by concise content and a `### References` section.

## Entry Points

**Main Index:**
- Location: `README.md` (likely points to subject MOCs).
- Triggers: User opening the vault.
- Responsibilities: High-level navigation.

**Subject Hubs:**
- Location: `000 Zettelkasten/[Subject]/[Subject].md`
- Triggers: Deep diving into a specific field (CIS, CSE, ELE).
- Responsibilities: Listing courses and major sub-topics.

## Error Handling

**Strategy:** Consistency Checks and Reorganization Plans.

**Patterns:**
- **Audit Reports:** Found in `444 Docs/audit_report.md` to identify orphans or structure issues.
- **Reorganization Plans:** Formalized in `444 Docs/reorganization_plan.md` before major structural shifts.

## Cross-Cutting Concerns

**Logging:** Tracked in `444 Docs/CHANGELOG.md` to record additions and modifications.
**Metadata:** Standardized format at the top of every file (Timestamp, Status, Tags).
**Assets:** Centralized storage in `Files/`, `222 Files/`, and `Excalidraw/`.

---

*Architecture analysis: 2025-01-31*
