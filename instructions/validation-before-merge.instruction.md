---
description: 'Validation-before-merge convention — requires explicit verification, test evidence, and completion checks before a task is treated as done. Use for all code-change tasks prior to suggesting merge or completion.'
applyTo: '**'
---

# Validation Before Merge

Do not report a coding task as complete based on the code merely being written or "looking correct." A task is only complete once it has been verified.

## Before declaring a task done

1. **Run it.** If the change is executable (a script, a function, a build, a test suite), actually run it and report the real output — not an assumption about what it would output.

2. **Show the evidence.** State what was run and what the result was (e.g., "ran `pytest tests/test_auth.py`, 14 passed, 0 failed"). Don't just say "tests pass" without having run them in this session.

3. **Check the original request against the result.** Re-read what was actually asked for and confirm each part was addressed. If part of the request wasn't handled (e.g., an edge case, a stated constraint), say so explicitly rather than presenting a partial solution as complete.

4. **Call out what wasn't verified.** If something can't be run or tested in the current environment (e.g., it depends on a live service, credentials, or a UI that can't be exercised here), say so plainly and suggest how the human should verify it, rather than implying it was checked.

## What this means in practice

- Do not say "this should work" as a substitute for testing it.
- Do not assume a fix resolved a bug without reproducing the original failure and confirming it no longer occurs.
- Do not mark a multi-step task complete if only some steps were finished — list what's done and what's outstanding.
- If asked to make a change and no test exists for the affected behavior, either add one or explicitly flag the gap — don't silently skip verification because coverage doesn't already exist.

## Escalation

If verification reveals the change doesn't fully work, do not quietly patch around it and re-declare success. State what failed, what was tried, and what's still broken, so the human can decide how to proceed.