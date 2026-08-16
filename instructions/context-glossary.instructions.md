---
description: 'CONTEXT.md convention — per-repo domain glossary that agents use for consistent naming, reduced verbosity, and shared understanding. Use when creating or maintaining domain glossaries in any repo.'
applyTo: '**/CONTEXT.md'
---

## CONTEXT.md — Domain Glossary Convention

Every non-trivial repo should have a `CONTEXT.md` at its root. This is a glossary — nothing else. Not a spec, not a scratch pad, not a TODO list.

### Purpose

A shared vocabulary between you and the agent. Benefits:
- Variables, functions, and files named consistently
- Agent uses fewer tokens (one precise term vs 20-word explanations)
- Codebase easier for agents to navigate
- Reduces misalignment across sessions

### Format

```markdown
# {Project Name}

{One sentence: what this project is}

## Language

{Term}: {Precise definition — what it IS, what it ISN'T}. Avoid: {alternative terms that might confuse}

{Term}: {Definition}. Avoid: {confusing alternatives}

## Relationships

• {Term A} contains many {Term B}s
• {Term C} belongs to exactly one {Term D}

## Flagged Ambiguities

• "{word}" was previously used to mean both X and Y — resolved: {which meaning wins}
```

### Rules

1. **Glossary only.** No implementation details, no architecture, no specs. If it describes HOW something is built, it doesn't belong here.
2. **Precise terms with "Avoid" lists.** Every term should say what NOT to call it: `User: The authenticated person. Avoid: account, customer, member`
3. **Living document.** Update during `/grill-me` sessions, during coding when you notice a fuzzy term, and during architecture reviews.
4. **Create lazily.** Don't create an empty `CONTEXT.md` preemptively. Create it the first time you have a term to define (usually during `/grill-with-docs`).
5. **Keep it short.** If it's longer than 50 terms, the project has too many concepts — that's a design smell.

### When to Update CONTEXT.md

- During `/grill-me` or `/grill-with-docs` when a term is resolved
- When you notice the agent using a different word for the same thing
- When you introduce a new domain concept
- When renaming something in code — update the glossary first

### Multi-Context Repos

If a repo has multiple bounded contexts (e.g. monorepo with `ordering/` and `billing/`), use a `CONTEXT-MAP.md` at root pointing to per-context glossaries:

```markdown
# Context Map

| Context | Glossary | Description |
|---------|----------|-------------|
| Ordering | src/ordering/CONTEXT.md | Order intake and fulfillment |
| Billing | src/billing/CONTEXT.md | Payments and invoicing |
```

### ADR (Architecture Decision Record) Convention

When hard-to-reverse decisions come up during grilling or coding, record them in `docs/adr/`. Only create an ADR when ALL three criteria are met:

1. **Hard to reverse** — changing later is expensive
2. **Surprising without context** — a future reader would wonder "why?"
3. **Real trade-off** — genuine alternatives existed

#### ADR Format

```markdown
# ADR-{NNNN}: {Decision Title}

**Status:** accepted | superseded by ADR-{NNNN}
**Date:** {YYYY-MM-DD}

## Context

{What prompted this decision — the forces at play}

## Decision

{What we decided and why}

## Consequences

{What follows — positive, negative, and neutral}
```

Don't create ADRs for obvious choices, ephemeral decisions, or things that are trivial to change.
