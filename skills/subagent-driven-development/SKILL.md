---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# Subagent-Driven Development

Execute plan by dispatching fresh browser subagents or breaking work into isolated task boundaries per task, with two-stage review after each: spec compliance review first, then code quality review.

**Core principle:** Fresh context per task + two-stage review (spec then quality) = high quality, fast iteration

## When to Use

```dot
digraph when_to_use {
    "Have implementation plan?" [shape=diamond];
    "Tasks mostly independent?" [shape=diamond];
    "Stay in this session?" [shape=diamond];
    "subagent-driven-development" [shape=box];
    "executing-plans" [shape=box];
    "Manual execution or brainstorm first" [shape=box];

    "Have implementation plan?" -> "Tasks mostly independent?" [label="yes"];
    "Have implementation plan?" -> "Manual execution or brainstorm first" [label="no"];
    "Tasks mostly independent?" -> "Stay in this session?" [label="yes"];
    "Tasks mostly independent?" -> "Manual execution or brainstorm first" [label="no - tightly coupled"];
    "Stay in this session?" -> "subagent-driven-development" [label="yes"];
    "Stay in this session?" -> "executing-plans" [label="no - parallel session"];
}
```

## The Process (Antigravity)

In Antigravity, you manage the orchestration loop directly:

```dot
digraph process {
    rankdir=TB;

    "Read plan, extract all tasks with full text, note context, create task.md" [shape=box];
    "Pick next task" [shape=box];
    "Implement task using task_boundary EXECUTION mode" [shape=box];
    "Run verification commands" [shape=box];
    "Spec compliance self-review: does code match spec?" [shape=diamond];
    "Fix spec gaps" [shape=box];
    "Code quality self-review: clean, no debt, good names?" [shape=diamond];
    "Fix quality issues" [shape=box];
    "Mark task complete in task.md" [shape=box];
    "More tasks remain?" [shape=diamond];
    "Use finishing-a-development-branch skill" [shape=box style=filled fillcolor=lightgreen];

    "Read plan, extract all tasks with full text, note context, create task.md" -> "Pick next task";
    "Pick next task" -> "Implement task using task_boundary EXECUTION mode";
    "Implement task using task_boundary EXECUTION mode" -> "Run verification commands";
    "Run verification commands" -> "Spec compliance self-review: does code match spec?";
    "Spec compliance self-review: does code match spec?" -> "Fix spec gaps" [label="no"];
    "Fix spec gaps" -> "Spec compliance self-review: does code match spec?" [label="re-review"];
    "Spec compliance self-review: does code match spec?" -> "Code quality self-review: clean, no debt, good names?" [label="yes"];
    "Code quality self-review: clean, no debt, good names?" -> "Fix quality issues" [label="no"];
    "Fix quality issues" -> "Code quality self-review: clean, no debt, good names?" [label="re-review"];
    "Code quality self-review: clean, no debt, good names?" -> "Mark task complete in task.md" [label="yes"];
    "Mark task complete in task.md" -> "More tasks remain?";
    "More tasks remain?" -> "Pick next task" [label="yes"];
    "More tasks remain?" -> "Use finishing-a-development-branch skill" [label="no"];
}
```

## In Antigravity: How to Orchestrate

Since you are the orchestrator in Antigravity (rather than spawning separate agent processes), follow this pattern per task:

1. **Announce:** "Implementing Task N: [description]"
2. **Set task_boundary to EXECUTION mode** for this specific task
3. **Implement** following the plan step-by-step (use TDD skill)
4. **Verify:** Run all commands specified in plan, check output
5. **Spec Review:** Re-read the task spec. Does code do exactly what spec says? Nothing more, nothing less?
6. **Quality Review:** Is the code clean? Good names? No magic numbers? No duplication?
7. **Fix and re-verify** if either review fails
8. **Update task.md** marking the task complete
9. **Move to next task**

## Prompt Templates for Reference

The original prompt templates are in this directory:
- `./implementer-prompt.md` — Use as a self-checklist when implementing each task
- `./spec-reviewer-prompt.md` — Use as a spec compliance checklist  
- `./code-quality-reviewer-prompt.md` — Use as a code quality checklist

## Red Flags

**Never:**
- Start implementation on main/master branch without explicit user consent
- Skip spec compliance review before quality review
- Proceed with unfixed issues
- Make parallel changes that could conflict

**Always:**
- Read the full task description from the plan (don't rely on memory)
- Run verification commands after implementation
- Complete spec review BEFORE quality review (order matters)
- Fix issues from each review before moving to next task

## Integration

**Required workflow skills:**
- **using-git-worktrees** — REQUIRED: Set up isolated workspace before starting
- **writing-plans** — Creates the plan this skill executes
- **requesting-code-review** — Code review checklist for each task
- **finishing-a-development-branch** — Complete development after all tasks
- **test-driven-development** — Follow TDD for each implementation step
