# Figure Design Principles

Design principles for creating publication-quality scientific figures.

## Core Philosophy

Follow Tufte's principles: maximize data-ink ratio, minimize chartjunk. Every element must serve a purpose.

## Grayscale Palette

Print-friendly grayscale values for academic figures:

```latex
% Primary grayscale palette
\definecolor{figblack}{gray}{0.0}      % Text, primary lines
\definecolor{figdark}{gray}{0.25}      % Borders, arrows
\definecolor{figmid}{gray}{0.5}        % Secondary elements
\definecolor{figlight}{gray}{0.85}     % Block fills
\definecolor{figpale}{gray}{0.95}      % Group backgrounds
```

| Element           | Gray Value  | Use Case                   |
| ----------------- | ----------- | -------------------------- |
| Text/Labels       | 0.0 (black) | All text content           |
| Borders/Arrows    | 0.25        | Node outlines, connections |
| Secondary lines   | 0.5         | Grid lines, annotations    |
| Block fills       | 0.85        | Interior of nodes          |
| Group backgrounds | 0.95        | Subsystem groupings        |

## Layout Principles

### Compactness

- **Tight spacing**: Use minimum necessary whitespace
- **Consistent gaps**: 5-8mm between adjacent blocks
- **No decorative elements**: Remove unnecessary borders, shadows, gradients

### Alignment

- **Grid-based**: Align nodes to implicit grid
- **Centered connections**: Arrows connect at node centers or edges
- **Balanced composition**: Distribute visual weight evenly

### Sizing

- **Uniform nodes**: Same-type blocks have identical dimensions
- **Proportional hierarchy**: Important elements slightly larger
- **Readable at scale**: Test at 50% zoom

Standard block dimensions:

```
Minimum width:  2.0cm (primary blocks)
Minimum height: 0.8cm (primary blocks)
Small blocks:   1.5cm x 0.6cm
Text padding:   2mm internal margin
```

## Typography

### Font Selection

- **Sans-serif**: Use `\sffamily` for all figure text
- **Match document**: Same font family as paper body when possible
- **Consistent weight**: Regular weight for labels, bold sparingly

### Font Sizes

```latex
\small      % Primary labels (recommended)
\footnotesize  % Secondary annotations
\scriptsize    % Tertiary details (use sparingly)
```

### Label Placement

- **Inside blocks**: Centered, single line preferred
- **Edge labels**: Positioned at midpoint, offset from line
- **External labels**: Consistent distance from referenced element

## Line Weights

Hierarchy through stroke width:

```latex
thin        % 0.4pt - tertiary lines, grids
semithick   % 0.6pt - secondary connections
thick       % 0.8pt - primary arrows (recommended)
very thick  % 1.2pt - emphasis only
```

## Arrow Styles

Standard arrow conventions:

- **Data flow**: Solid line, filled arrowhead (`-Stealth`)
- **Control flow**: Solid line, open arrowhead (`-Latex`)
- **Optional/conditional**: Dashed line
- **Bidirectional**: Double-headed arrow

## Block Diagram Conventions

### Node Types

| Type         | Shape       | Fill     | Border  | Use                    |
| ------------ | ----------- | -------- | ------- | ---------------------- |
| Process      | Rectangle   | figlight | figdark | Main processing blocks |
| Input/Output | Rectangle   | white    | figdark | System boundaries      |
| Decision     | Diamond     | figlight | figdark | Conditional logic      |
| Storage      | Cylinder    | figlight | figdark | Data stores            |
| Group        | Dashed rect | figpale  | figmid  | Subsystem grouping     |

### Connection Rules

1. **Horizontal preference**: Flow left-to-right when possible
2. **Orthogonal lines**: Use right angles, avoid diagonal connections
3. **Minimal crossings**: Rearrange to reduce line intersections
4. **Consistent direction**: Maintain flow direction within subsystems

### Grouping

Use dashed rectangles to indicate:

- Subsystems or modules
- Repeated structures
- Logical groupings

Group styling:

```latex
group/.style={
  draw=figmid,
  dashed,
  fill=figpale,
  rounded corners=2pt,
  inner sep=8pt
}
```

## Accessibility

### Contrast

- Minimum contrast ratio 4.5:1 for text
- Test figure in grayscale (already optimized)
- Ensure readability when printed

### Patterns

When color distinction needed (future extension):

- Combine color with pattern (hatching, dots)
- Use shape variation alongside color
- Add text labels as backup

## Quality Checklist

Before finalizing a figure:

- [ ] Standalone TikZ source compiles without errors
- [ ] Temporary PNG/JPG preview was rendered from the compiled figure
- [ ] Preview was visually inspected and any issues were fixed
- [ ] All text readable at intended print size
- [ ] Consistent spacing throughout
- [ ] No orphaned or misaligned elements
- [ ] Arrows point in logical flow direction
- [ ] Labels do not overlap lines or nodes
- [ ] Figure works in grayscale
- [ ] Minimal visual clutter
