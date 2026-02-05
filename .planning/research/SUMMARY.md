# Research Summary

**Project:** Obsidian Zettelkasten Automation
**Date:** 2026-02-05
**Status:** Synthesis Complete

## Executive Summary

The project aims to automate the conversion of academic materials (PDFs, PPTs) into a highly networked Obsidian Zettelkasten. Research indicates a clear preference for a **"Linear Transformation Pipeline"** that decouples extraction from synthesis. The recommended approach uses **Python** as the runtime, **Marker** for SOTA PDF-to-Markdown conversion (preserving layout/tables), and **python-pptx** for granular slide extraction. This ensures high-fidelity input for the knowledge base, addressing the critical need to preserve diagrams and equations.

To manage the complexity of academic content, the system must avoid "monolithic dumps" by implementing intelligent chunking and "asset-first" management. Images should be extracted, hashed, and stored centrally (`222 Files/`) to prevent duplication and link rot. The architecture promotes a "Human-in-the-loop" workflow where automation handles the drudgery of formatting and linking, while the user focuses on refinement.

Key risks center on context loss during extraction and "ghost linking" by AI. Mitigation strategies include maintaining "Source Notes" as hubs for atomic concepts, using hash-based image naming to avoid collisions, and relying on standard YAML frontmatter over proprietary plugin formats to ensure long-term data portability.

## Key Findings

### Stack Decisions
*   **Core:** **Python 3.10+** as the universal glue.
*   **PDF Engine:** **Marker** (over PyMuPDF) for superior table/layout handling.
*   **PPT Engine:** **python-pptx** for granular control over slides/notes.
*   **Utilities:** **python-frontmatter** for metadata, **Pillow** for image processing.
*   **Obsidian:** **Dataview** for lists, **Folder Canvas** for visual maps.

### Feature Priorities
*   **Table Stakes:** Deep PDF parsing (images/tables), Reference management (Zotero integration).
*   **Differentiators:** **AI Atomic Splitting** (concept-based, not just text splitting), **Visual Folder Roadmaps**.
*   **Anti-Features:** Monolithic conversions (one huge MD file), Base64 image embedding, Over-tagging.

### Architecture Patterns
*   **Pipeline:** Ingest -> Router -> Extraction (PDF/PPT) -> Semantic Chunking -> Integration -> Vault.
*   **Pattern: "Asset First" Write:** Extract and hash-name images to `222 Files/` *before* generating Markdown to guarantee link integrity.
*   **Pattern: "Slide Context":** Treat slides as "Context Blocks" initially; don't split mid-slide.
*   **Pattern: Roadmap Injection:** Parse and insert links into `_ROADMAP` files rather than blindly appending.

### Critical Pitfalls
*   **Context Loss:** Splitting related slides destroys narrative; solve by keeping a "Source Note" hub.
*   **Image Pathing:** Broken links if paths aren't vault-relative; solve with hash-based filenames in `222 Files/`.
*   **Stale Roadmaps:** Dataview lag; solve by scoping queries or writing static links for critical paths.
*   **Asset Pollution:** Extracting thousands of bullet-point icons; solve with size/dimension filters.

## Implications for Roadmap

The research suggests a phased approach starting with high-fidelity extraction before attempting intelligent synthesis.

### Phase 1: The Extraction Engine
**Focus:** Building the "Ingest -> Extract -> Normalize" pipeline.
*   **Deliverables:** Scripts to convert PDF/PPT to Markdown + extracted images.
*   **Key Tech:** Marker, python-pptx, Pillow.
*   **Pitfall Avoided:** Image Pathing (implement hash-naming immediately).
*   **Rationale:** Without clean, structure-preserving data, downstream splitting/linking is impossible.

### Phase 2: Integration & Roadmap Management
**Focus:** Connecting the raw output to the Obsidian Vault structure.
*   **Deliverables:** Integration Agent to write frontmatter/files; Roadmap Manager to update `_ROADMAP`.
*   **Key Tech:** python-frontmatter, Regex/AST parsing.
*   **Pitfall Avoided:** Stale Roadmaps (implement static injection).
*   **Rationale:** Turns "files on disk" into "accessible notes" within the user's workflow.

### Phase 3: Visuals & User Experience
**Focus:** Making the data consumable.
*   **Deliverables:** Folder Canvas setup, Dataview dashboards.
*   **Key Tech:** Obsidian Plugins (Folder Canvas, Dataview).
*   **Rationale:** Provides the "visual roadmap" capability requested.

### Phase 4: Intelligent Atomization (AI)
**Focus:** Moving from "Source Notes" to "Atomic Concepts".
*   **Deliverables:** Semantic Chunker using LLM/Heuristics.
*   **Key Tech:** LLM API, prompt engineering.
*   **Pitfall Avoided:** Context Loss (requires careful prompt tuning).
*   **Rationale:** High complexity; best built on a stable foundation of Phases 1-3.

## Research Flags

*   **Standard Patterns:** Phase 1 & 2 are well-covered by `STACK.md` and `ARCHITECTURE.md`.
*   **Needs Research:** Phase 4 (AI Atomization). Specific prompts for academic context (e.g., "Extract definitions from this slide but keep the example") need experimentation.
*   **Validation Needed:** Performance of **Marker** on local hardware (GPU requirements).

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| **Stack** | High | Standard, well-maintained libraries selected. |
| **Features** | High | Clear distinction between "must-have" and "nice-to-have". |
| **Architecture** | High | "Linear Pipeline" is a robust pattern for this domain. |
| **Pitfalls** | High | Known issues (images, context) are well-documented. |

## Sources
*   **Marker GitHub:** Layout analysis pipeline.
*   **python-pptx Docs:** Slide object model.
*   **Zettelkasten Method:** Atomicity principles.
*   **Obsidian Forum:** Community findings on PDF extraction and image handling.