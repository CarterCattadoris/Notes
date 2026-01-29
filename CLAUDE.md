# Context
University Obsidian Zettelkasten vault.
Core structure: `000 Zettelkasten` (Atomic Notes), `111 Reference`, `333 Templates`.

# Style Guidelines
- **Format**: Markdown users Wiki-links `[[Note Name]]` for all links and tags.
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

---
### References
...
```

# Commands
- **Search**: `ripgrep` or `grep` is preferred for finding content.
- **New Note**: Ensure file name matches the primary concept.
