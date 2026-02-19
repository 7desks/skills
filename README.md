# 7desks AI Skills

AI skills for frontend development: SOLID principles and pixel-perfect design-to-code. Compatible with Cursor, Windsurf, Cline, Codex, and other AI IDEs.

These are Agent Skills—instruction sets that teach the AI how to perform specific frontend tasks with consistent quality and structure.

---

## For AI IDEs and Models

**Repo link:** https://github.com/7desks/skills.git

Reference this repo when setting up skills. Use the `install-7desks-skills` skill for installation instructions into `.cursor/skills/`, `.windsurf/skills/`, `.cline/skills/`, or `~/.codex/skills/`.

**Install via AI:** Paste the repo link and ask the AI to install the skills (e.g., "Install skills from https://github.com/7desks/skills.git into my Cursor skills folder").

---

## Skills

| Skill | Description |
|-------|-------------|
| **install-7desks-skills** | Install 7desks skills from the repo into Cursor, Windsurf, Cline, or Codex. Use when the user asks to install 7desks skills or references the repo link. |
| **solid-principles** | Applies SOLID principles when building or refactoring React/Next.js/Remix components. Use for better code quality, reusable UI, maintainable architecture. |
| **design-to-frontend-code** (pixel-perfect-responsive-ui) | Converts Figma, Sketch, or Adobe XD designs into pixel-perfect, responsive, accessible UI using Tailwind, design tokens, and WCAG semantics. Use for design handoff, Tailwind components, design trends. |

---

## Installation

### Manual

```bash
# Clone the repo
git clone https://github.com/7desks/skills.git
cd skills

# Copy skills into Cursor

# Global (all projects):
cp -r solid-principles design-to-frontend-code ~/.cursor/skills/

# Project (this repo only):
mkdir -p .cursor/skills
cp -r solid-principles design-to-frontend-code .cursor/skills/
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/7desks/skills.git $env:TEMP\7desks-skills
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.cursor\skills
Copy-Item -Recurse $env:TEMP\7desks-skills\solid-principles, $env:TEMP\7desks-skills\design-to-frontend-code -Destination $env:USERPROFILE\.cursor\skills
```

### Install from GitHub

Install a single skill via its path:

- solid-principles: https://github.com/7desks/skills/tree/main/solid-principles
- design-to-frontend-code: https://github.com/7desks/skills/tree/main/design-to-frontend-code
- install-7desks-skills: https://github.com/7desks/skills/tree/main/install-7desks-skills

Restart your IDE after installing to pick up new skills.

---

## Usage

Reference skills with `@solid-principles`, `@design-to-frontend-code`, or `@install-7desks-skills`. Skills auto-activate when your request matches their trigger scenarios (e.g., installing skills, building components, design handoff, refactoring).

---

## License

MIT
