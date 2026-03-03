# superpowers-Antigravity

A collection of **Antigravity-compatible skills** adapted from the [Superpowers](https://github.com/NeilARaman/superpowers) framework — a set of structured, reusable behavioral skills that guide AI agents to follow disciplined software engineering workflows.

## What is This?

[Superpowers](https://github.com/NeilARaman/superpowers) is a skills framework originally designed for Claude. This repository contains the same skills **rewritten and adapted for [Antigravity](https://antigravity.google/)** — Google DeepMind's agentic AI coding assistant.

Each skill is a `SKILL.md` file that:
- Defines **when** the skill should be invoked (via YAML `description` frontmatter)
- Explains **how** the agent should behave when the skill is active
- Is automatically surfaced to the Antigravity agent based on the task context

## Skills

| Skill | Description |
|-------|-------------|
| [`brainstorming`](./skills/brainstorming/SKILL.md) | Structured creative exploration before any implementation or planning |
| [`dispatching-parallel-agents`](./skills/dispatching-parallel-agents/SKILL.md) | Safely dispatch multiple subagents in parallel for independent subtasks |
| [`executing-plans`](./skills/executing-plans/SKILL.md) | Systematically execute a written plan step-by-step |
| [`finishing-a-development-branch`](./skills/finishing-a-development-branch/SKILL.md) | Complete a feature branch with proper review, tests, and merge prep |
| [`receiving-code-review`](./skills/receiving-code-review/SKILL.md) | Gracefully receive, process, and apply code review feedback |
| [`requesting-code-review`](./skills/requesting-code-review/SKILL.md) | Prepare and request a thorough code review from collaborators |
| [`subagent-driven-development`](./skills/subagent-driven-development/SKILL.md) | Architect complex tasks by delegating to focused subagents |
| [`systematic-debugging`](./skills/systematic-debugging/SKILL.md) | Debug methodically with root-cause tracing instead of guessing |
| [`test-driven-development`](./skills/test-driven-development/SKILL.md) | Write tests before implementation following the RED-GREEN-REFACTOR cycle |
| [`using-git-worktrees`](./skills/using-git-worktrees/SKILL.md) | Use Git worktrees for parallel development without branch switching |
| [`using-superpowers`](./skills/using-superpowers/SKILL.md) | Meta-skill: how to find and invoke other skills correctly |
| [`verification-before-completion`](./skills/verification-before-completion/SKILL.md) | Verify all requirements are met before declaring a task done |
| [`writing-plans`](./skills/writing-plans/SKILL.md) | Write clear, structured implementation plans before coding |
| [`writing-skills`](./skills/writing-skills/SKILL.md) | Create new skills using the TDD-adapted skill development lifecycle |

## How It Works

Antigravity surfaces skills automatically based on their YAML `description` field. When a relevant skill appears in the agent's context, the agent **must** use `view_file` to read the full `SKILL.md` before taking any action.

```yaml
# Example SKILL.md frontmatter
---
name: systematic-debugging
description: Use when diagnosing unexpected behavior, failing tests, or unclear errors - before making any code changes
---
```

The `using-superpowers` skill enforces a strict rule: **if there is even a 1% chance a skill applies, the agent must read and follow it.**

## Usage

### Option 1: Copy skills into your project

Copy the `skills/` directory into your project root. Antigravity will automatically detect and surface the skills.

```
your-project/
├── skills/
│   ├── systematic-debugging/
│   │   └── SKILL.md
│   ├── test-driven-development/
│   │   └── SKILL.md
│   └── ...
└── your code...
```

### Option 2: Clone and reference

```bash
git clone https://github.com/YOUR_USERNAME/superpowers-Antigravity.git
```

Then copy or symlink the `skills/` directory into your working project.

## Differences from the Original Superpowers

The original Superpowers repository is designed for Claude's tool-calling model. This adaptation makes the following changes for Antigravity:

- **Tool references updated**: All tool invocations reference Antigravity's specific tools (`view_file`, `browser_subagent`, `run_command`, `task_boundary`, `notify_user`, etc.)
- **Subagent model**: Rewritten to use Antigravity's `browser_subagent` dispatching pattern instead of Claude's native parallel tool calls
- **Task tracking**: Integrated with Antigravity's `task_boundary` and `task.md` workflow
- **File access**: Updated to use Antigravity's `view_file` skill-loading convention

## Contributing

If you adapt, improve, or create new skills for Antigravity, contributions are welcome! Please follow the `writing-skills` skill guide when creating new skills.

## Credits

- Original [Superpowers](https://github.com/NeilARaman/superpowers) framework by the Superpowers contributors
- Antigravity adaptation maintained in this repository

## License

MIT
