# Requirements: Obsidian Zettelkasten Automation

## v1 Requirements

### Document Extraction (EXT)
- [ ] **EXT-01**: Extract text, tables, and formatting from PDF files using the Marker engine.
- [ ] **EXT-02**: Extract slides, speaker notes, and text from PPTX files using python-pptx.
- [ ] **EXT-03**: Extract diagrams/images from PDF/PPTX, saving them to `222 Files/` with SHA-256 hash-based naming.
- [ ] **EXT-04**: Convert mathematical equations from presentations into standard LaTeX blocks.

### Zettelkasten Management (ZET)
- [ ] **ZET-01**: Generate a "Source Note" hub for every processed file to maintain narrative context.
- [ ] **ZET-02**: Split extracted content into atomic Zettelkasten notes based on slide boundaries or major headers.
- [ ] **ZET-03**: Automatically generate consistent YAML frontmatter (subject, date, source, status) for all new notes.
- [ ] **ZET-04**: Create wiki-links between atomic notes and their parent Source Note.

### Subject Roadmaps (MAP)
- [ ] **MAP-01**: Initialize `_ROADMAP [Subject].md` at the top of subject folders if it doesn't exist.
- [ ] **MAP-02**: Automatically inject links to new notes into the relevant `_ROADMAP` file.
- [ ] **MAP-03**: Organize roadmap links into a hierarchy of "Overarching Concepts" vs. "Sub-ideas".
- [ ] **MAP-04**: Ensure roadmap updates are static (real links) for reliability and searchability.

## v2 Requirements (Deferred)
- **AI-CONCEPT-SPLIT**: Using LLMs to split notes by semantic concept rather than structural boundaries.
- **FOLDER-CANVAS**: Automated generation of Obsidian Canvas files for visual subject mapping.
- **DATAVIEW-DASH**: Complex Dataview dashboards for tracking learning progress.

## Out of Scope
- Refactoring existing legacy notes in the vault.
- Managing external sync or cloud backups.
- OCR for hand-written notes (unless supported natively by extraction engines).

## Traceability
*(To be filled by roadmap)*

---
*Last updated: 2026-02-05*
