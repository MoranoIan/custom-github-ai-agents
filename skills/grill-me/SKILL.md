---
name: grill-me
description: "Interrogate the user about their plan/design until every branch of the decision tree is resolved. Use when: '/grill-me', 'grill me', 'challenge my plan', 'stress-test this idea', 'what am I missing', 'help me think through this', 'poke holes in this', or before any non-trivial feature where requirements feel fuzzy."
---

# Grill Me

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

**Ask the questions one at a time, waiting for feedback on each question before continuing.**

If a question can be answered by exploring the codebase, explore the codebase instead of asking.

## When to Trigger

- Before any feature where the user hasn't specified edge cases
- When the user describes something vague ("make this better", "add auth", "refactor this")
- When `/grill-me` or `/grill` is typed explicitly
- When a Working Contract has 2+ ambiguous assumptions

## The Grilling Rules

1. **One question at a time.** Never batch. Wait for the answer before the next.
2. **Provide your recommended answer.** Don't just ask — propose what you'd do and why. Let the user confirm or correct.
3. **Walk the decision tree.** Each answer opens new branches. Follow them until leaf nodes (no more ambiguity).
4. **Challenge contradictions.** If the user says X but earlier said Y, call it out immediately.
5. **Stress-test with scenarios.** Invent edge cases that probe boundaries: empty input, 10x scale, concurrent users, hostile input, timezone differences.
6. **Cross-reference with code.** If the user states how something works, check whether the code agrees. Surface contradictions.
7. **Don't be polite about it.** The point is to find holes NOW, not after implementation.

## Question Categories

Work through these dimensions (skip what's obviously N/A):

### Scope & Boundaries
- What's IN scope vs explicitly NOT?
- Where does this feature end and another begins?
- Who are the users/callers? What do they expect?

### Behavior & Edge Cases
- What happens when input is empty? Enormous? Malformed?
- What's the failure mode? Silent fail? Error? Retry?
- Concurrency — what if two users hit this simultaneously?
- What state can this leave the system in if it crashes midway?

### Integration & Dependencies
- What existing code does this touch? What might break?
- External dependencies — what if they're slow or down?
- Data model — new tables? Migrations? Backward compat?

### Verification
- How will you KNOW this works? (Not "I'll test it" — what specific test?)
- What does success look like in production?
- What metrics/logs prove it's working a week later?

## Ending the Session

When all branches are resolved, summarize the decisions as a compact Working Contract or spec (depending on scope). Ask: "Ready to build, or anything else to stress-test?"

## Variants

- **`/grill-me` (standalone)** — pure interrogation, any domain (code, docs, planning, life decisions)
- **`/grill-with-docs`** — same interrogation, but also updates `CONTEXT.md` (domain glossary) and offers ADRs when decisions are hard-to-reverse. See `context-glossary.instructions.md` for the CONTEXT.md format.

### /grill-with-docs Additional Behavior

When running as `/grill-with-docs`:

1. **Challenge against the glossary.** If `CONTEXT.md` exists, check every term the user uses against it. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"
2. **Sharpen fuzzy language.** When the user uses vague or overloaded terms, propose a precise canonical term.
3. **Update CONTEXT.md inline.** When a term is resolved during the session, update `CONTEXT.md` right there. Don't batch.
4. **Offer ADRs sparingly.** Only when all three are true: (a) hard to reverse, (b) surprising without context, (c) result of a real trade-off. Format: see `docs/adr/` convention in `context-glossary.instructions.md`.
