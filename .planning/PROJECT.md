# Project: Obsidian Zettelkasten Evolution

## Core Value
Transform future academic and professional inputs (PDFs, PPTs) into a structured, atomic Zettelkasten knowledge base with agent-maintained subject roadmaps and centralized asset management.

## What This Is
A new workflow for an existing Obsidian vault that focuses on automated processing of lecture materials into atomic notes, while maintaining high-level subject roadmaps without refactoring legacy content.

## Context
- **User Role**: Student/Lifelong Learner
- **Environment**: Obsidian Vault (Linux)
- **Status**: Subsequent Milestone (Building on existing vault structure)

## Requirements

### Validated
- ✓ **VAULT-STRUC**: Use existing numbered folder system (`000 Zettelkasten`, `111 Reference`, `222 Files`).
- ✓ **ZETTEL-CONV**: Follow Zettelkasten principles (atomic notes, wiki-links).
- ✓ **ASSET-MGMT**: Store images in `222 Files/` and link them in notes.

### Active
- [ ] **PROC-PDF-PPT**: Agent-led processing of PDF and PPT files into structured markdown.
- [ ] **ATOM-SPLIT**: Automatically split processed materials into atomic Zettelkasten notes.
- [ ] **SUBJ-ROADMAP**: Maintain `_ROADMAP [Subject].md` files at the top of subject folders.
- [ ] **AUTO-MAP-UPDATE**: Agent updates roadmaps with "Overarching vs Sub-ideas" whenever new notes are added.
- [ ] **IMG-EXTRACT**: Extract diagrams/screenshots from presentations that can't be rendered in LaTeX/Markdown.

### Out of Scope
- **LEGACY-REF**: Refactoring existing notes (unless explicitly prompted).
- **NON-MD-ROADMAPS**: Interactive or non-markdown roadmap formats.
- **SYNC-MGMT**: Handling Obsidian sync or external publishing.

## Key Decisions
| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Subject Roadmaps | Needs high-level view of topics vs sub-ideas for easy navigation. | `_ROADMAP [Subject].md` |
| Agent-Led Updates | Markdown lacks native automation; agent will manage roadmap state. | Pending |
| No Refactoring | Preserve existing notes to avoid disrupting established context. | Validated |
| Asset Centralization | Standardize on `222 Files/` to fix existing "Files/" vs "222 Files/" fragmentation. | Pending |

---
*Last updated: 2026-02-05 after initialization*
