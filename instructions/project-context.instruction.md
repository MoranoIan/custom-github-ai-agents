---
description: 'Project context convention — keeps repository architecture, structure, and naming conventions visible to the assistant so it stays consistent with existing patterns instead of inventing new ones. Use for all tasks that touch code, structure, or naming in this repo.'
applyTo: '**'
---

# Project Context

Before making changes, orient to how this specific repository is actually built — don't default to generic conventions or patterns from other projects.

## What to establish before non-trivial changes

1. **Structure.** Where does code, config, tests, and docs actually live in this repo? Follow the existing layout rather than introducing a new one (e.g., don't add a `src/utils/` if the project already has a `lib/helpers/` doing the same job).

2. **Naming conventions.** Match what's already there:
   - File naming (kebab-case, camelCase, snake_case — check existing files, don't assume).
   - Variable/function naming style.
   - Terminology — if the codebase consistently calls something a "workspace" and not a "project," use "workspace."

3. **Architecture and boundaries.** Identify the existing separation of concerns (e.g., where business logic lives vs. where I/O happens, how modules are expected to depend on each other) before adding new code. A new feature should fit the existing shape of the system, not introduce a parallel pattern for the same kind of problem.

4. **A repo-level glossary, if one exists** (e.g., a `CONTEXT.md` or similar domain glossary). If the repo has one, treat its terminology and definitions as authoritative over generic assumptions. If it doesn't have one and the domain has non-obvious terms, consider proposing one rather than re-deriving meaning from context every time.

## How to apply this

- When adding a new file, place it alongside files serving a similar purpose — don't create a new top-level convention for something that already has a home.
- When naming something new, check 2-3 existing examples of similar things first, and match that pattern.
- When unsure whether a pattern is intentional or incidental, prefer following it anyway for consistency, and note the assumption rather than silently deviating.
- If the existing conventions are genuinely inconsistent (different naming styles in different areas), match whichever convention dominates the immediate area being changed, not a global average.

## Boundaries

- This instruction is about consistency, not preservation for its own sake. If asked explicitly to refactor structure or naming, do that — this instruction governs default behavior when no such request has been made.
- Don't invent architectural rules the repo doesn't actually follow. If there's no clear existing pattern for a given kind of change, say so and propose one rather than presenting a guess as "the convention."