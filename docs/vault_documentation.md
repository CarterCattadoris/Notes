# Vault Documentation & LLM Guide

## 1. Directory Structure

- **000 Zettelkasten/**: The core knowledge base. Notes are organized by subject folder (e.g., `CSE`, `General`, `Discrete Math`).
- **111 Reference/**: Reference materials that are not atomic notes.
- **333 Templates/**: Templates for creating new notes (`Core Zettel Idea.md`, `MOC.md`).
- **Files/**, **Excalidraw/**: Attachments and diagrams.

## 2. Note Types & Status

Notes are categorized by a `Status` metadata field:

- **#idea**: An atomic note representing a single concept.
    - **Goal**: Concise explanation of one topic.
    - **Example**: `CMOS.md`
- **#MOC** (Map of Content): A structural note that links to multiple related atomic notes.
    - **Goal**: Aggregate knowledge on a broader subject.
    - **Example**: `CSE.md` listing courses.

## 3. Note Format

All notes follow a strict frontmatter-like structure (though not YAML frontmatter):

```markdown
<YYYYMMDDHHmm> (Timestamp ID)
Status: <#idea or #MOC>
Tags: [[Tag1]], [[Tag2]] (Note: Tags are Wiki-links to other notes, not #hashtags)

<Content Body>

---
### References
<Link to source if applicable>
```

## 4. Linking Strategy

- **Wiki-links (`[[Note Name]]`)**: Used exclusively for linking.
- **Tags as Links**: The "Tags" field uses `[[Topic]]` format rather than Obsidian `#topic` tags, treating topics as first-class notes.
- **Backlinks**: Rely on the graph structure; `#MOC` notes serve as hubs.

## 5. Style Guidelines

- **Atomic**: Keep `#idea` notes focused on one concept.
- ** interconnected**: Heavily link related concepts in the body.
- **Timestamped**: Every note starts with a unique temporal ID.

## 6. External Resources
The following directories contain class presentations and reference materials. These should be processed and integrated into notes as needed:
- **Probability & Statistics**: `~/Downloads/ProbabilityPresentations`
- **Deep Learning / ELE**: `~/Downloads/ELE400Presentations`
- **Operating Systems**: `~/Downloads/OSPresentations`

## 7. Changelog Protocol
The LLM must maintain a changelog to track progress and processed materials.
- **Location**: `docs/CHANGELOG.md`
- **Content**:
    - List of presentations/files added to the vault.
    - Summary of significant changes or refactors.
    - Date and context of the operation.
