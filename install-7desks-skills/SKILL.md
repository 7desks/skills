---
name: install-7desks-skills
description: Install 7desks frontend skills (solid-principles, design-to-frontend-code) from https://github.com/7desks/skills.git into .cursor/skills/, .windsurf/skills/, .cline/skills/, or ~/.codex/skills/. Use when the user asks to install 7desks skills, set up skills from the 7desks repo, or references https://github.com/7desks/skills.
---

# Install 7desks Skills

## When to Activate

Activate when the user:
- Asks to install 7desks skills
- References `https://github.com/7desks/skills` or `https://github.com/7desks/skills.git`
- Wants to set up `.cursor/skills`, `.windsurf/skills`, `.cline/skills`, or Codex skills

## Repo and Available Skills

- **Repo:** https://github.com/7desks/skills.git
- **Skills:** `solid-principles`, `design-to-frontend-code`

## IDE Install Paths

| IDE | Project scope | Global scope |
|-----|---------------|--------------|
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` |
| Windsurf | `.windsurf/skills/` | `~/.windsurf/skills/` |
| Cline | `.cline/skills/` | `~/.cline/skills/` |
| Codex | N/A | `~/.codex/skills/` or `$CODEX_HOME/skills` |

## Installation Commands

### Bash (Unix/macOS/Linux)

**Project scope (Cursor):**
```bash
git clone https://github.com/7desks/skills.git /tmp/7desks-skills
mkdir -p .cursor/skills
cp -r /tmp/7desks-skills/solid-principles /tmp/7desks-skills/design-to-frontend-code .cursor/skills/
rm -rf /tmp/7desks-skills
```

**Global scope (Cursor):**
```bash
git clone https://github.com/7desks/skills.git /tmp/7desks-skills
mkdir -p ~/.cursor/skills
cp -r /tmp/7desks-skills/solid-principles /tmp/7desks-skills/design-to-frontend-code ~/.cursor/skills/
rm -rf /tmp/7desks-skills
```

**Codex:**
```bash
git clone https://github.com/7desks/skills.git /tmp/7desks-skills
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -r /tmp/7desks-skills/solid-principles /tmp/7desks-skills/design-to-frontend-code "${CODEX_HOME:-$HOME/.codex}/skills/"
rm -rf /tmp/7desks-skills
```

For Windsurf or Cline, replace `.cursor` with `.windsurf` or `.cline` in the paths above.

### PowerShell (Windows)

**Project scope (Cursor):**
```powershell
git clone https://github.com/7desks/skills.git $env:TEMP\7desks-skills
New-Item -ItemType Directory -Force -Path .cursor\skills
Copy-Item -Recurse $env:TEMP\7desks-skills\solid-principles, $env:TEMP\7desks-skills\design-to-frontend-code -Destination .cursor\skills
Remove-Item -Recurse -Force $env:TEMP\7desks-skills
```

**Global scope (Cursor):**
```powershell
git clone https://github.com/7desks/skills.git $env:TEMP\7desks-skills
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.cursor\skills
Copy-Item -Recurse $env:TEMP\7desks-skills\solid-principles, $env:TEMP\7desks-skills\design-to-frontend-code -Destination $env:USERPROFILE\.cursor\skills
Remove-Item -Recurse -Force $env:TEMP\7desks-skills
```

## After Install

Restart the IDE to pick up new skills.
