# Context
University Obsidian Zettelkasten vault.
Core structure: `000 Zettelkasten` (Atomic Notes), `111 Reference`, `333 Templates`.

# Key Directories
- **Probability & Statistics**: `000 Zettelkasten/CIS/Probability and Statistics`
- **Design of OS**: `000 Zettelkasten/CSE/Design Operating Systems`
- **Embedded & Mobile Systems**: `000 Zettelkasten/CSE/Embedded & Mobile Systems`
- **Deep Learning**: `000 Zettelkasten/ELE/Deep Learning in Engrng Apps`

# External Resources
- **Probability**: `~/Downloads/ProbabilityPresentations`
- **ELE/Deep Learning**: `~/Downloads/ELE400Presentations`
- **OS**: `~/Downloads/OSPresentations`

# Changelog Protocol
- Maintain `444 Docs/CHANGELOG.md`.
- Log all processed presentations and significant vault changes.

# Style Guidelines
- **Format**: Markdown uses Wiki-links `[[Note Name]]` for all links and tags.
- **Tags**: Do NOT use `#tag`. Use metadata field `Tags: [[Topic Link]]`.
- **Status**:
  - `#idea`: Atomic, single-concept note.
  - `#MOC`: Map of Content, structural note.
- **IDs**: File content MUST start with `YYYYMMDDHHmm` timestamp.
- **Tone**: Concise, academic, heavily linked.

# Image Handling
- **Storage**: Store relevant images/diagrams that cannot be rendered in Markdown/LaTeX in `222 Files`.
- **Source**: Extract from presentations.
- **Usage**: Embed in relevant markdown files.

# Roadmap Protocol
- **File Requirement**: Each subject area must have a roadmap file.
- **Naming Convention**: `_(Abbreviated Name) ROADMAP.md` (e.g., `_DL ROADMAP.md`).
- **Location**: Stored in the respective subject folder.
- **Content**: Ordered list of big ideas and relevant sub-ideas representing the learning path.
- **Links**: Atomic note links are optional; focus on conceptual hierarchy.

# Note Template
```markdown
YYYYMMDDHHmm
Status: #idea
Tags: [[Broad Topic]]

## Content
...
```

# Commands
- **Search**: `ripgrep` or `grep` is preferred for finding content.
- **New Note**: Ensure file name matches the primary concept.

# Source Policy
- **Primary Source**: Always use equations, definitions, and details from the course presentations (in `~/Downloads/*`) over external knowledge.
- **External Info**: Use only to supplement understanding or when explicitly prompted. Course material is the source of truth.