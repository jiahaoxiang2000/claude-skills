---
name: creating-figures
description: Creates publication-quality scientific figures for academic papers using TikZ. Use when creating block diagrams, system architectures, flowcharts, or technical illustrations for papers and theses. Always render a temporary PNG/JPG preview and self-verify visual quality before finalizing figure files.
---

# Creating Scientific Figures

Create compact, print-friendly figures for academic papers using LaTeX TikZ.

## Quick Start

Minimal block diagram:

```latex
\documentclass[tikz,border=2mm]{standalone}
\usetikzlibrary{arrows.meta,positioning}
\begin{document}
\begin{tikzpicture}[
  block/.style={rectangle, draw, fill=gray!15, minimum width=2cm, minimum height=0.8cm, font=\small\sffamily},
  arrow/.style={->, >=Stealth, thick}
]
  \node[block] (a) {Input};
  \node[block, right=of a] (b) {Process};
  \node[block, right=of b] (c) {Output};
  \draw[arrow] (a) -- (b);
  \draw[arrow] (b) -- (c);
\end{tikzpicture}
\end{document}
```

## Design Principles

Key principles for academic figures:

1. **Grayscale palette**: Print-friendly, no color dependency
2. **Compactness**: Minimize whitespace, maximize information
3. **Consistency**: Uniform sizing, spacing, typography
4. **Hierarchy**: Line weight and gray levels show importance

See [PRINCIPLES.md](PRINCIPLES.md) for complete design guidelines.

## Implementation

**TikZ Block Diagrams**: See [TIKZ.md](TIKZ.md) for:

- Preamble setup and required packages
- Standard style definitions
- Common patterns (linear, parallel, feedback loops)
- Positioning techniques
- Edge labels and annotations

**Working Example**: See [examples/tikz/block-diagram.tex](examples/tikz/block-diagram.tex) for a complete PID control system diagram.

## Standard Styles

Copy these styles to your preamble:

```latex
% Grayscale colors
\definecolor{figdark}{gray}{0.25}
\definecolor{figlight}{gray}{0.85}

% Block styles
\tikzset{
  block/.style={rectangle, draw=figdark, fill=figlight,
    minimum width=2cm, minimum height=0.8cm,
    text centered, font=\small\sffamily},
  terminal/.style={rectangle, draw=figdark, fill=white,
    minimum width=1.5cm, minimum height=0.6cm,
    text centered, font=\small\sffamily},
  arrow/.style={->, >=Stealth, thick, draw=figdark},
  group/.style={draw=gray, dashed, fill=gray!5,
    rounded corners=2pt, inner sep=8pt}
}
```

## Common Patterns

### Linear Flow

```latex
\node[block] (a) {A};
\node[block, right=of a] (b) {B};
\draw[arrow] (a) -- (b);
```

### Feedback Loop

```latex
\node[block] (proc) {Process};
\node[block, below=of proc] (fb) {Feedback};
\draw[arrow] (proc.east) -- ++(0.5,0) |- (fb.east);
\draw[arrow] (fb.west) -| ($(proc.west)+(-0.5,0)$) -- (proc.west);
```

### Grouped Subsystem

```latex
\node[block] (a) {A};
\node[block, right=of a] (b) {B};
\begin{scope}[on background layer]
  \node[group, fit=(a)(b), label=above:Subsystem] {};
\end{scope}
```

## Workflow

1. **Plan layout**: Sketch block arrangement on paper
2. **Define styles**: Set up colors and node styles
3. **Place nodes**: Use relative positioning (`right=of`, `below=of`)
4. **Draw connections**: Add arrows with appropriate routing
5. **Add labels**: Annotate edges and groups
6. **Refine spacing**: Adjust for visual balance
7. **Render preview**: Compile the standalone figure and create a temporary PNG or JPG preview
8. **Self-verify**: Inspect the preview for visual quality and fix issues before finalizing
9. **Test print**: Verify grayscale readability

## Required Self-Verification

Every figure creation task must include a local render-and-check loop before final delivery. The source may compile successfully while still having unreadable labels, overlapping arrows, awkward whitespace, or misaligned groups; the raster preview catches these problems before the user sees them.

1. Save the figure as standalone TikZ source (`.tex`).
2. Compile it to PDF with `latexmk -pdf` or `pdflatex` from the figure directory.
3. Convert the PDF to a temporary PNG or JPG preview using an available tool such as `pdftoppm`, ImageMagick `magick`, or `convert`.
4. Open/read the temporary preview image and inspect it visually.
5. Fix any quality problems, then rerender and reinspect until the preview is acceptable.
6. Keep the final `.tex` and requested deliverables; remove or clearly mark temporary preview files unless the user asks to keep them.

Use a temporary preview filename such as `figure-name.preview.png` or place previews under a temporary directory. Do not treat successful LaTeX compilation as sufficient verification.

Self-check the preview for:

- text legibility at paper scale and at 50% zoom
- no overlapping text, labels, arrows, nodes, or group boxes
- arrowheads and line routes point in the intended direction
- consistent node sizes, spacing, alignment, and margins
- enough padding between container labels and inner blocks
- compact layout without excessive whitespace or clipped content
- grayscale contrast that remains readable in print

Example verification commands:

```bash
latexmk -pdf system-diagram.tex
pdftoppm -png -singlefile -r 200 system-diagram.pdf system-diagram.preview
```

If `latexmk` is unavailable, use `pdflatex`. If `pdftoppm` is unavailable, use ImageMagick or another installed PDF-to-image converter.

## File Organization

```
your-paper/
├── figures/
│   ├── system-diagram.tex    % Standalone TikZ source
│   └── system-diagram.pdf    % Compiled figure
└── paper.tex                 % \includegraphics{figures/system-diagram}
```

Compile standalone figures separately, then include as PDF for faster paper compilation.
