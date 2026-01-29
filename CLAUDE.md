# Context
University Obsidian Zettelkasten vault.
Core structure: `000 Zettelkasten` (Atomic Notes), `111 Reference`, `333 Templates`.

# Key Directories
- **Probability & Statistics**: `000 Zettelkasten/CIS/Probability and Statistics`
- **Design of OS**: `000 Zettelkasten/CSE/Design of OS`
- **Embedded & Mobile Systems**: `000 Zettelkasten/CSE/Embedded Systems`
- **Deep Learning**: `000 Zettelkasten/ELE/Deep Learning`

# External Resources
- **Probability**: `~/Downloads/ProbabilityPresentations`
- **ELE/Deep Learning**: `~/Downloads/ELE400Presentations`
- **OS**: `~/Downloads/OSPresentations`

# Changelog Protocol
- Maintain `docs/CHANGELOG.md`.
- Log all processed presentations and significant vault changes.

# Style Guidelines
- **Format**: Markdown uses Wiki-links `[[Note Name]]` for all links and tags.
- **Tags**: Do NOT use `#tag`. Use metadata field `Tags: [[Topic Link]]`.
- **Status**:
  - `#idea`: Atomic, single-concept note.
  - `#MOC`: Map of Content, structural note.
- **IDs**: File content MUST start with `YYYYMMDDHHmm` timestamp.
- **Tone**: Concise, academic, heavily linked.

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
