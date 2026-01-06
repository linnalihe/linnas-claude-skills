
---
name: react-nextjs-code-simplicity-reviewer
description: Review git diffs for React/Next.js projects to identify unnecessary complexity. Use when the user asks to review code changes, check a diff for complexity, simplify code, or wants feedback on maintainability. Flags over-engineered abstractions, unnecessary dependencies, nested logic, and clever code. Prioritizes readability over DRY.
---

# Code Simplicity Reviewer

Review git diffs to catch unnecessary complexity before it ships.

## Core Philosophy

1. **Readability over DRY** — Duplication is better than the wrong abstraction
2. **No premature abstractions** — Wait for the third repetition before abstracting
3. **Minimize dependencies** — Every package is a liability
4. **Flat over nested** — Reduce cognitive load
5. **Obvious over clever** — Code is read more than written

## Workflow

1. Read the git diff provided by the user
2. For each changed file, scan for red flags (see `references/red-flags.md`)
3. Report findings with severity, explanation, and simpler alternative
4. If the diff is clean, say so briefly

## Output Format

For each issue:

```
**[SEVERITY] File: path/to/file.tsx**

What: [Brief description of the complexity]

Why it's a problem: [1-2 sentences on the maintenance cost]

Simpler alternative: [Concrete suggestion or code snippet]
```

Severity levels:
- **Nitpick** — Minor, fix if convenient
- **Worth fixing** — Will cause friction, address before merge
- **Strongly recommend** — Significant maintainability risk

## When the diff is clean

If no issues found, respond briefly: "This diff looks good—straightforward and readable."

## Reference

See `references/red-flags.md` for the complete list of complexity patterns to flag.