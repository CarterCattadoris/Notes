# Phase 1 Context: Extraction Engine

## User Intent
The primary goal is a low-friction extraction pipeline that converts academic sources (PDF/PPTX) into Markdown notes that look and feel like existing vault entries. The user wants to trigger extraction via an agent that intelligently handles "new" vs. "existing" files.

## Extraction Workflow
- **Scope:** Target all files in a source directory that have not been previously processed.
- **Updates:** If a file has already been processed, the engine should only perform additive updates (e.g., adding missing sections). 
- **Safety:** Never delete or overwrite manual user edits unless the modification is incorrect and explicitly confirmed by the user.

## Note Organization & Naming
- **Hierarchy:** Organize output by lecture number.
- **Heuristic:** If no lecture number is found in the content/filename, use the file's upload or modification date to determine the sequence.
- **Assets:** All images go to `222 Files/` using SHA-256 hashes for filenames.

## Formatting Standards (Mimic Existing)
All generated notes must strictly follow the established Zettelkasten pattern:
1. **Timestamp ID:** A 12-digit timestamp (`YYYYMMDDHHMM`) at the very top.
2. **Status:** `Status: #idea` line.
3. **Tags:** Automated tagging based on the subject (e.g., `Tags: [[Data Structures (CIS351)]]`).
4. **Body:** Clean Markdown content (formatting in the source PDF/PPTX is ignored in favor of readability).
5. **Footer:** A horizontal rule `---` followed by a `### References` section.

## Feedback & Failures
- **Progress:** Visual progress bars are preferred for feedback during processing.
- **Error Handling:** If an image fails to extract, the agent must report it specifically rather than skipping silently or crashing.
