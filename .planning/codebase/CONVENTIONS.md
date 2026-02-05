# Coding Conventions

**Analysis Date:** 2025-05-20

## Naming Patterns

**Files:**
- **Title Case:** Most notes use Title Case (e.g., `Abstract Classes.md`).
- **Course Codes:** Course MOCs or specific course notes often include the code in parentheses (e.g., `Data Structures (CIS351).md`).
- **Spaces:** Spaces are used, not hyphens or underscores.
- **Lowercase (Avoid):** Lowercase filenames (e.g., `cse384 final stuff.md`) appear to be informal/temporary and should be normalized.

**Directories:**
- **Hierarchy:** Subject / Specific Subject / [Notes] (e.g., `CIS/Data Structures/`).
- **Grouping:** Directories group related atomic notes under a broader subject.

## Code Style (Note Format)

**Frontmatter-like Metadata:**
Every note starts with a strict header block (not YAML):
```markdown
[YYYYMMDDHHmm]
Status: #[idea|MOC]
Tags:[[Link1]], [[Link2]]
```

**Status Types:**
- `#idea`: Atomic notes representing a single concept.
- `#MOC`: Map of Content, aggregating links to related notes.

**Footer:**
Standard footer for references:
```markdown
---
### References
- [[Source Note]]
```

## Import Organization (Linking)

**Wiki-links:**
- Exclusive use of `[[Note Name]]` for all links.
- No standard Markdown links `[text](url)` observed for internal navigation.

**Tags as Links:**
- The "Tags" metadata field uses Wiki-links (e.g., `Tags:[[Engineering]]`) rather than hash tags (`#engineering`).
- This treats topics as first-class notes.

## Note Design

**Atomicity:**
- Notes tagged `#idea` should focus on a single concept.
- Broad topics are split into multiple atomic notes linked by an MOC.

**Interconnectedness:**
- Heavy use of internal linking within the body text.
- MOCs serve as structural hubs.

## Directory Layout
- `000 Zettelkasten/`: Core knowledge base.
- `111 Reference/`: Non-atomic reference materials.
- `222 Files/`: Attachments (images, PDFs).
- `333 Templates/`: Note templates.
- `444 Docs/`: Vault documentation and meta-project files.

---

*Convention analysis: 2025-05-20*
