# Testing & Integrity Patterns

**Analysis Date:** 2025-05-20

## Integrity Verification

Since this is an Obsidian vault, "testing" refers to maintaining the structural integrity and quality of the knowledge graph.

### Metadata Validation
- **Requirement:** Every note in `000 Zettelkasten/` must start with a 12-digit timestamp.
- **Requirement:** Every note must have a `Status:` line with either `#idea` or `#MOC`.
- **Requirement:** Every note must have a `Tags:` line using Wiki-links.

### Link Integrity
- **Broken Links:** Check for `[[Link]]` where the target file does not exist.
- **Orphan Check:** Identify notes with no incoming links (not linked by any MOC or other note).
- **Dead Ends:** Identify notes with no outgoing links (excluding `### References`).

### Naming Consistency
- **Regex Check:** Ensure files follow Title Case and do not contain unauthorized characters.
- **Course Code Format:** Ensure course-related notes consistently use the `(CODE###)` suffix.

## Verification Tools (Recommended)

**Vault Audit Script (Proposed):**
```bash
# Check for missing ID line
grep -rL "^[0-9]\{12\}$" "000 Zettelkasten/"

# Check for missing Status
grep -rL "^Status: #" "000 Zettelkasten/"

# Find notes with lowercase names (potential debt)
find "000 Zettelkasten/" -name "[a-z]*" -type f
```

## Structure Checks

**MOC Completeness:**
- For every directory in `000 Zettelkasten/`, there should be a corresponding MOC file (e.g., `CIS/` has `CIS.md`).
- Every note in a subfolder should be linked by at least one `#MOC` in its lineage.

**Attachment Tracking:**
- Check for unused files in `222 Files/` or `Files/` that are not linked in any `.md` file.
- Check for broken image links.

## Test Types

**Unit Tests (Note level):**
- Verify file format matches `333 Templates/Core Zettel Idea.md`.
- Verify `#idea` notes are under a certain word count (to ensure atomicity).

**Integration Tests (Graph level):**
- Verify every course code mentioned in `Tags:` has a corresponding MOC file.
- Verify the `000 Zettelkasten/` hierarchy matches the directory structure.

---

*Testing analysis: 2025-05-20*
