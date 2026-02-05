# Technology Stack

**Analysis Date:** 2025-02-05

## Languages

**Primary:**
- Markdown - All notes and documentation are written in Markdown.

**Secondary:**
- LaTeX (MathJax) - Used for mathematical equations and formal proofs in notes (e.g., `000 Zettelkasten/CIS/Discrete Math/Direct Proofs.md`).
- Shell/Bash - Used for vault management and Claude-assisted searching.

## Runtime

**Environment:**
- Obsidian - The primary environment for managing and viewing the knowledge base.

**Package Manager:**
- Git - Used for version control of the vault.

## Frameworks

**Core:**
- Zettelkasten Method - The organizational framework for atomic notes and structural hubs (MOCs).

**External Visualization:**
- Excalidraw - Used for hand-drawn diagrams and visual notes, stored as `.excalidraw.md` files in `Excalidraw/`.

## Key Dependencies

**Critical:**
- Wiki-links (`[[Note Name]]`) - The primary dependency for vault-wide connectivity and tagging.

**Metadata:**
- Timestamp IDs - Every note depends on a 12-digit ID (`YYYYMMDDHHmm`) for uniqueness and temporal tracking.

## Configuration

**Environment:**
- `.claude/settings.local.json` - Configuration for Claude's interaction with the vault.
- `CLAUDE.md` - Operational guidelines for AI-assisted note-taking.

**Build:**
- Not applicable (Static Markdown).

## Platform Requirements

**Development:**
- Obsidian Desktop/Mobile.
- Git (for synchronization).
- `ripgrep` or `grep` (for searching).

---

*Stack analysis: 2025-02-05*
