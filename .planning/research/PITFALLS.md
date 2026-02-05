# Domain Pitfalls

**Domain:** Obsidian Zettelkasten Automation (PDF/Presentation Processing)
**Researched:** 2024-05-23

## Critical Pitfalls

Mistakes that cause data loss, broken workflows, or unusable knowledge bases.

### Pitfall 1: PDF/Presentation Extraction Context Loss
**What goes wrong:** Automated scripts (e.g., converting PPTX/PDF to Markdown) often treat slides/pages as independent atomic units without linkable context.
**Why it happens:** Presentations often span a single concept across multiple slides (e.g., "Part 1", "Part 2" or continued lists).
**Consequences:** Resulting atomic notes are fragmented and lack necessary context to be understood alone. The "narrative thread" of the lecture is lost.
**Prevention:**
*   **Manual Review:** Always include a "refactoring" step after bulk extraction.
*   **Heuristic Grouping:** Script should detect "cont." or similar titles and merge them.
*   **Source Linking:** Every atomic note *must* backlink to the original source file (page number/slide link) in its properties.

### Pitfall 2: Automated Image Pathing & Linking
**What goes wrong:** Extraction scripts save images to paths that Obsidian cannot resolve, or fail to handle image name collisions across multiple PDFs.
**Why it happens:** External tools (like `pdfimages` or Python libraries) don't know Obsidian's vault settings or folder structure.
**Consequences:** "Image not found" errors in Obsidian, or images visible in Edit mode but broken in Reader/Export.
**Prevention:**
*   **Vault-Relative Paths:** Ensure the script outputs standard Markdown image links `![[image.png]]` or `![alt](path/to/image.png)` relative to the vault root.
*   **Dedicated Asset Folder:** Configure the script to move extracted images to the configured Obsidian attachments folder (e.g., `222 Files/` as per project structure).
*   **Hash-Based Naming:** Use SHA-256 hashes of the image data for filenames to prevent collisions and automatically de-duplicate identical images across different presentations.

### Pitfall 3: "Automatic" Roadmap Staleness (Dataview)
**What goes wrong:** Roadmaps built with Dataview queries (e.g., "List all notes in this folder") fail to update immediately when files are added via script.
**Why it happens:** Dataview indexes files periodically; heavy vaults or complex queries can lag (stale data).
**Consequences:** Users make decisions based on outdated roadmaps.
**Prevention:**
*   **Folder Scoping:** Restrict Dataview queries to specific folders to improve indexing speed.
*   **Core Plugin Preference:** Transition from Dataview to **Obsidian "Bases"** or **"Projects"** (core/official plugins) which have better internal cache integration.
*   **Static Generation:** For critical roadmaps, use a script (e.g., Python or Templater) to *write* physical links to a "Map of Content" (MOC) file rather than relying on a dynamic query.

### Pitfall 4: Dependency on Abandoned/Maintenance-Only Plugins
**What goes wrong:** Building a core workflow around plugins like **Dataview** or **Annotator**, which have slowed development or pending successors (Datacore).
**Why it happens:** Obsidian core features (like Properties) are evolving, often making older plugins redundant or broken.
**Consequences:** Workflow collapse if a major Obsidian update (e.g., v1.8+) breaks a community plugin.
**Prevention:**
*   **Property-First Data:** Store all metadata in standard YAML/Properties, not inline fields (e.g., `Status:: Done`).
*   **Minimize Plugins:** Use core features (Properties, Canvas) where possible for roadmaps.

## Moderate Pitfalls

Mistakes that cause friction or technical debt.

### Pitfall 1: Asset Folder Pollution (The "Icon" Problem)
**What goes wrong:** Extracting every single image from a PPTX (including footer logos, background lines, bullet icons).
**Consequences:** The `222 Files/` folder floods with thousands of 1KB garbage images.
**Prevention:** Implement a size/dimension filter in the extraction script (e.g., "Ignore images < 10KB or < 200x200px").

### Pitfall 2: OCR Reading Order Failure
**What goes wrong:** Standard PDF extractors often read across multi-column slides, mixing sentences from different parts of the page.
**Prevention:** Use layout-aware extraction tools like **Marker** or **Azure Document Intelligence** which recognize columns and reading flow.

## Phase-Specific Warnings

| Phase Topic | Likely Pitfall | Mitigation |
|-------------|---------------|------------|
| **Extraction Scripting** | Image name collisions | Use hash-based naming (MD5/SHA). |
| **Roadmap Setup** | Indexing lag (Stale data) | Scope Dataview to subfolders; use Waypoint for MOCs. |
| **Note Refactoring** | Over-atomization | Keep a "Master Note" that links all fragments in order. |

## Sources
- Obsidian Forum: "PDF extraction and images" (2024-2025 updates)
- Dataview GitHub: "Stale data on file change" issue reports.
- Marker-pdf Documentation: Comparison of layout extraction accuracy.
- Community wisdom on "Bases" as Dataview successor (2025).
