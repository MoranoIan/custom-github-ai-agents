---
name: release-notes
description: 'Create a structured release summary from a set of merged changes, commits, or closed issues/PRs. Use when preparing a changelog entry, a release announcement, or a version summary for tagging a new release.'
---

# Release Notes

Use this skill when someone needs a release summary built from raw inputs — a commit log, a list of merged PRs, or a diff between two tags — rather than a summary they've already drafted.

## Process

1. **Gather the raw changes.** Pull the list of commits, merged PRs, or closed issues since the last release (e.g., `git log v1.2.0..HEAD --oneline`, or a list of PR titles). Don't summarize from memory — work from the actual list.

2. **Classify each change** into categories, using only the ones that apply:
   - **Breaking changes** — anything requiring the user to change how they use the project.
   - **New features**
   - **Improvements** — changes to existing behavior that aren't new features (performance, UX polish).
   - **Bug fixes**
   - **Deprecations** — things marked for removal but not yet removed.
   - **Internal/chore** — dependency bumps, refactors, CI changes. Include only if the project's convention is to list these; otherwise omit.

3. **Rewrite each entry for the reader, not the author.** A commit message like "fix null check in parseConfig" becomes something like "Fixed a crash that occurred when a config file was missing an optional field." State user-facing impact, not implementation detail — unless the audience is explicitly internal/developers.

4. **Order within each category** by impact, most significant first. Breaking changes always lead the whole summary regardless of category ordering.

5. **Call out migration steps** for any breaking change: what the user needs to do differently. If a change is breaking but no migration path exists yet, flag that explicitly rather than omitting it.

## Output format

```
## [Version] - Date

### Breaking Changes
- ...

### New Features
- ...

### Improvements
- ...

### Bug Fixes
- ...

### Deprecations
- ...
```

Omit any section with nothing in it — don't print empty headers. Keep each bullet to one line where possible; use a second line only for a migration note.

## Boundaries

- Do not invent user-facing impact for a change you don't understand — if a commit message is too vague to classify or rewrite confidently, list it under an "Other" section verbatim and flag it for the author to clarify, rather than guessing.
- Match the project's existing changelog format and tone if one exists; don't introduce a new structure unless asked.
- This skill drafts the summary — it doesn't decide the version number. If asked to also suggest a version bump, base it on the highest-impact category present (any breaking change → major; new features → minor; fixes only → patch) and say so explicitly, per semver convention.