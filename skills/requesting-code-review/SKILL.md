---
name: requesting-code-review
description: Use when completing tasks, implementing major features, or before merging to verify work meets requirements
---

# Requesting Code Review

Perform a thorough self-review — or optionally request a review via browser_subagent — to catch issues before they cascade.

**Core principle:** Review early, review often.

## When to Request Review

**Mandatory:**
- After each major task in subagent-driven development
- After completing a major feature
- Before merge to main

**Optional but valuable:**
- When stuck (fresh perspective)
- Before refactoring (baseline check)
- After fixing complex bug

## How to Review in Antigravity

### Step 1: Get the diff to review

```bash
BASE_SHA=$(git rev-parse HEAD~1)  # or origin/main
HEAD_SHA=$(git rev-parse HEAD)
git diff $BASE_SHA $HEAD_SHA
```

### Step 2: Perform the Review

Read the template at `code-reviewer.md` in this directory and self-review against it.

Populate mentally:
- `{WHAT_WAS_IMPLEMENTED}` — What you just built
- `{PLAN_OR_REQUIREMENTS}` — What it should do
- `{BASE_SHA}` and `{HEAD_SHA}` — Commit range
- `{DESCRIPTION}` — Summary of changes

### Step 3: Act on Findings

- **Critical issues** → Fix immediately before proceeding
- **Important issues** → Fix before moving to next task
- **Minor issues** → Note for later
- **Wrong feedback** → Push back with reasoning

## Example

```
[Just completed Task 2: Add verification function]

BASE_SHA=$(git log --oneline | head -2 | tail -1 | awk '{print $1}')
HEAD_SHA=$(git rev-parse HEAD)

[Self-review using code-reviewer.md checklist]
Strengths: Clean architecture, real tests
Issues:
  Important: Missing progress indicators
  Minor: Magic number (100) for reporting interval
Assessment: Fix progress indicators before continuing

[Fix → Continue to Task 3]
```

## Integration with Workflows

**Subagent-Driven Development:**
- Review after EACH task
- Catch issues before they compound
- Fix before moving to next task

**Executing Plans:**
- Review after each batch (3 tasks)
- Get feedback, apply, continue

## Red Flags

**Never:**
- Skip review because "it's simple"
- Ignore Critical issues
- Proceed with unfixed Important issues

See template at: `requesting-code-review/code-reviewer.md`
