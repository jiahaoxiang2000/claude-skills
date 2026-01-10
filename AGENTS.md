# AGENTS.md

This repository contains Claude Skills - reusable instruction files for AI agents.

## Repository Type

Documentation repository for Claude Skills, not a traditional software project. No build system, tests, or CI/CD.

## File Structure

```
claude-skills/
├── practices.md           # Best practices for authoring Skills
├── creating-figures/       # Example Skill: TikZ diagrams
├── AGENTS.md              # This file
└── README.md              # Project overview
```

## Working With This Repository

### Reading Skills

- Start with `SKILL.md` - contains YAML frontmatter and quick start
- Follow progressive disclosure: linked files provide details
- SKILL.md should be under 500 lines

### Creating New Skills

Follow patterns in `creating-figures/`:

**1. Directory structure:**

```
skill-name/
├── SKILL.md              # Required - main entry with YAML frontmatter
├── PRINCIPLES.md         # Optional - design principles
├── REFERENCE.md          # Optional - technical reference
├── EXAMPLES.md           # Optional - usage examples
└── examples/             # Optional - working examples
```

**2. YAML frontmatter format:**

```yaml
---
name: skill-name
description: What the skill does and when to use it. Max 1024 chars.
---
```

**3. Naming conventions:**

- `name`: Max 64 chars, lowercase + numbers + hyphens only
- Preferred: Gerund form (`creating-figures`, `processing-pdfs`)
- Avoid: Vague names (`helper`, `utils`), reserved words (`anthropic-helper`)

**4. Content guidelines:**

- Keep SKILL.md concise (Claude is smart, assume prior knowledge)
- Use third person perspective in descriptions
- Link out to detailed files for depth
- See `practices.md` for complete guidelines

## Key Resources

- **Best practices**: `practices.md` (1,214 lines - complete guide)
- **Example Skill**: `creating-figures/SKILL.md` (working reference)
- **Design patterns**: `creating-figures/PRINCIPLES.md`
- **Implementation**: `creating-figures/TIKZ.md`

## Important Notes

- This is NOT a Python/LaTeX/Typst project - it's about Skills for AI agents
- No package managers, requirements.txt, or CI/CD
- Focus on clear, concise instruction writing
- Reference `practices.md` before creating or modifying Skills
