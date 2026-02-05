# Codebase Concerns

**Analysis Date:** 2025-05-27

## Tech Debt

**Duplicate Image Storage:**
- Issue: Images are split between `222 Files/` and `Files/`. This breaks the numbered directory convention and scatters assets.
- Files: `222 Files/Pasted image...`, `Files/Pasted image...`
- Impact: Confusing asset management; potential for broken links if one folder is deleted without checking.
- Fix approach: Consolidate all images into `222 Files/` (matching the numbered convention) and update links. Delete `Files/`.

**Inconsistent Root Directory Naming:**
- Issue: The vault uses a numbered system (`000 Zettelkasten`, `111 Reference`, etc.) but newer folders violate this (`Homework`, `Lecture Notes`, `Excalidraw`).
- Files: `Homework/`, `Lecture Notes/`, `Excalidraw/`
- Impact: Decreases vault navigability and sorting order.
- Fix approach: Rename or move these folders to fit the numbered scheme (e.g., move `Excalidraw` to `222 Files` or `Files`, move `Homework` to `000 Zettelkasten`).

## Organized Chaos

**Fragmented Homework Files:**
- Issue: Homework files are split between a root `Homework/` folder and course specific folders in `000 Zettelkasten/`.
- Files: `Homework/Homework 7.md`, `000 Zettelkasten/Discrete Math/Homework 9.md`
- Impact: No single source of truth for assignments.
- Fix approach: Move all homework notes into their respective course folders in `000 Zettelkasten/` or a dedicated `Homework` sub-folder within courses.

**Loose Files in Zettelkasten Root:**
- Issue: Notes sitting in the root of `000 Zettelkasten/` instead of categorized subfolders.
- Files: `000 Zettelkasten/Lab 4.md`, `000 Zettelkasten/Recitation 3.md`, `000 Zettelkasten/testing.md`
- Impact: Clutters the main entry point of the knowledge base.
- Fix approach: Move these to appropriate course or topic folders (e.g., `Lab 4.md` to its relevant course).

## Empty/Zombie Directories

**Unused Root Directories:**
- Issue: Directories exist but contain no files.
- Files: `111 Reference/`, `Lecture Notes/`
- Impact: Adds visual noise without value.
- Fix approach: Delete if unused, or populate if they have a distinct purpose from `000 Zettelkasten`.

## Missing Critical Features

**Lack of Consistent Note Metadata:**
- Problem: Many loose notes likely lack YAML frontmatter or tags for better organization.
- Blocks: Effective querying (Dataview) and graph filtering.

**Automation Feasibility:**
- Problem: "Automatic roadmap updates" (requested in project setup) requires custom scripting or complex Dataview queries which don't currently exist.
- Impact: Manual maintenance burden until automation is built.

---

*Concerns audit: 2025-05-27*
