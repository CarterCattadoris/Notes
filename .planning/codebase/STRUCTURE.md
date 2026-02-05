# Codebase Structure

**Analysis Date:** 2025-01-31

## Directory Layout

```
Zettelkasten/
├── 000 Zettelkasten/   # Core knowledge base (atomic notes and MOCs)
│   ├── CIS/            # Computer Information Systems
│   ├── CSE/            # Computer Science & Engineering
│   ├── ELE/            # Electrical Engineering
│   └── General/        # General subjects (Physics, Math, etc.)
├── 111 Reference/      # External reference materials
├── 222 Files/          # Asset storage (images, PDFs)
├── 333 Templates/      # Obsidian templates for new notes
├── 444 Docs/           # Meta-documentation about the vault
├── Files/              # Alternative/Legacy asset storage
├── Excalidraw/         # Hand-drawn diagrams and sketches
├── Homework/           # Academic assignments and solutions
├── Lecture Notes/      # Raw notes taken during class
└── README.md           # Vault entry point
```

## Directory Purposes

**000 Zettelkasten:**
- Purpose: The "Brain" of the vault. Contains processed, permanent notes.
- Contains: Folders for major disciplines and markdown files for concepts/MOCs.
- Key files: `000 Zettelkasten/CIS/CIS.md`, `000 Zettelkasten/CSE/CSE.md`.

**333 Templates:**
- Purpose: Ensures consistency across all notes.
- Contains: Markdown templates with predefined metadata fields.
- Key files: `333 Templates/Core Zettel Idea.md`, `333 Templates/MOC.md`.

**444 Docs:**
- Purpose: Governance and tracking.
- Contains: Guidelines, audit reports, and the vault changelog.
- Key files: `444 Docs/vault_documentation.md`, `444 Docs/CHANGELOG.md`.

**222 Files / Files:**
- Purpose: Stores non-markdown assets.
- Contains: Images (PNG, JPG) and other attachments referenced in notes.

## Key File Locations

**Entry Points:**
- `README.md`: High-level overview.
- `000 Zettelkasten/[Subject]/[Subject].md`: Subject-specific landing pages.

**Configuration:**
- `444 Docs/vault_documentation.md`: The "Source of Truth" for vault conventions.
- `333 Templates/`: Blueprints for all content.

**Core Logic:**
- `000 Zettelkasten/`: The primary location for conceptual data.

## Naming Conventions

**Files:**
- **Atomic Notes:** Descriptive nouns (e.g., `Full Adder.md`, `Binary Relations.md`).
- **MOCs:** Subject name or course name (e.g., `CIS.md`, `Digital Logic Design (CSE261).md`).
- **Assets:** Prefixed with `Pasted image` or descriptive names.

**Directories:**
- **Root:** 3-digit prefix + Name (e.g., `111 Reference`).
- **Sub-folders:** Descriptive category names (e.g., `Discrete Math`).

## Where to Add New Code

**New Conceptual Note:**
- Primary code: Create in the relevant sub-folder within `000 Zettelkasten/`.
- Template: Use `333 Templates/Core Zettel Idea.md`.

**New Subject/Course Hub:**
- Implementation: Create a new `.md` file in the subject root (e.g., `000 Zettelkasten/ELE/Signal Processing.md`).
- Template: Use `333 Templates/MOC.md`.

**Utilities/Meta:**
- Guidelines: `444 Docs/`.
- Assets: `222 Files/` or `Files/`.

## Special Directories

**Excalidraw:**
- Purpose: Contains editable vector drawings.
- Generated: Yes (via Obsidian plugin).
- Committed: Yes.

**.claude:**
- Purpose: LLM-specific settings.
- Committed: Yes.

---

*Structure analysis: 2025-01-31*
