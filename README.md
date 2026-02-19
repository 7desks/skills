# solid-principles-pattern

A Cursor AI skill that applies SOLID principles when building or refactoring React/Next.js frontend components. Use when you need better code quality, reusable UI, maintainable architecture, or frontend refactoring guidance.

**Keywords:** Cursor AI skills, Cursor rules, Agent Skills, SOLID principles, React, Next.js, frontend, code quality, components

---

## SOLID Frontend Rules

| Principle | Frontend rule |
| --------- | ------------- |
| **S** | One component = one concern (UI / data / logic) |
| **O** | Extend via variants, composition; avoid if/else for new types |
| **L** | Child components replaceable for parent; same contract |
| **I** | Small, specific props; avoid fat shared props |
| **D** | Depend on abstractions (hooks, services); inject data sources |

---

## When to Use

- build or refactor React / Next.js / Remix / React Native / Expo components
- improve frontend code quality
- design reusable UI components
- structure frontend folders
- add new functionality without breaking existing code
- review frontend architecture or PRs

---

## Project Rules

- Composition over inheritance
- Separate UI, logic, and data access
- Avoid god components
- Depend on abstractions, not implementations

---

## Installation

Copy the `solid-principles` folder to your Cursor skills directory:

**Project-level** (shared with the repo):

```
.cursor/skills/solid-principles/
```

**Global** (available across all projects):

```
~/.cursor/skills/solid-principles/
```

The skill auto-activates when Cursor detects relevant user intent (e.g., building components, refactoring, improving code quality).
