# Technology Stack

**Project:** Obsidian Zettelkasten Automation
**Researched:** 2026-02-05

## Recommended Stack

### Core Processing (Local)
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| **Python** | 3.10+ | Runtime | Required for all recommended libraries; universal glue code. |
| **Marker** | Latest | PDF -> Markdown | SOTA local conversion. Handles tables/equations better than PyMuPDF. Extracts images automatically. |
| **python-pptx** | Latest | PPTX Extraction | Granular access to Slides, Shapes, and Notes. Better than generic converters for preserving "Slide = Context" boundaries. |
| **MarkItDown** | Latest | Office -> Markdown | Microsoft's tool. Good fallback for non-PPTX Office docs (DOCX, XLSX) if needed. |

### Metadata & File Management
| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| **python-frontmatter** | Latest | YAML Manipulation | Reading/Writing Obsidian frontmatter without breaking content. |
| **PyYAML** | Latest | Config/Data | Parsing complex YAML structures in roadmaps. |
| **Pillow (PIL)** | Latest | Image Processing | Resizing/converting extracted diagrams before saving to `222 Files/`. |

### Infrastructure (Obsidian)
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| **Dataview** | Plugin | Dynamic Lists | Essential for "automatically" listing notes under roadmap sections (if desired) or auditing. |
| **Templater** | Plugin | File Creation | If manual trigger is needed; otherwise Python scripts handle file creation. |

## Alternatives Considered

| Category | Recommended | Alternative | Why Not |
|----------|-------------|-------------|---------|
| PDF Engine | **Marker** | `PyMuPDF` (fitz) | PyMuPDF is faster but requires much more code to reconstruct tables and layout. Marker does the heavy lifting. |
| PDF Engine | **Marker** | `IBM Docling` | Docling is powerful but slower and heavier. Marker is optimized for "Markdown Output" specifically. |
| PPT Engine | **python-pptx** | `MarkItDown` | MarkItDown dumps the whole presentation to one MD file. We need slide-by-slide control for atomic splitting. |
| OCR | **Surya** (via Marker) | `Tesseract` | Surya is modern, GPU-accelerated (if available), and better at line-level text layout. |

## Installation

```bash
# Core Extraction
pip install marker-pdf python-pptx markitdown

# Support Utilities
pip install python-frontmatter PyYAML Pillow

# Optional: Deep Learning/OCR support for Marker
pip install surya-ocr
```

## Sources

- [Marker GitHub](https://github.com/VikParuchuri/marker) - SOTA PDF conversion.
- [python-pptx Documentation](https://python-pptx.readthedocs.io/) - The standard for PPTX manipulation.
- [Microsoft MarkItDown](https://github.com/microsoft/markitdown) - Office document conversion utility.
