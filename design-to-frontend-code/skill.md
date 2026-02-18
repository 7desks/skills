---
name: design-to-frontend-code
description: Translates provided UI/UX designs (Figma link / screenshots / PDF / prototype) into a frontend implementation plan and executes development section-by-section. Use when the user mentions UI/UX, Figma, design handoff, pixel-perfect, responsive UI, components, design system, or asks to build screens from designs.
---

#  UI/UX design → Frontend Code (section-by-section)

## Goal
Implement the UI exactly as designed provided while staying maintainable: reusable components, responsive behavior, correct states, and accessibility.

## Inputs to request
- Design source: Figma link / screenshots / PDF / prototype
- Target stack: framework (React/Next/Vue), styling (Tailwind/CSS modules/SCSS), component lib (MUI/Chakra/etc)
- Breakpoints to support + layout rules
- Design system tokens (colors, typography, spacing, radius, shadows)
- Component inventory (buttons, inputs, cards, navbar, sidebar, table, modals, etc)
- States list: hover/active/disabled/focus, loading, empty, error, success
- Data assumptions: API shape, placeholders, pagination, auth, permissions
- Acceptance rules: “pixel-perfect” tolerance, browser support, performance constraints