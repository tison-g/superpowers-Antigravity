# superpowers-Antigravity

A collection of **Antigravity-compatible skills** adapted from the [Superpowers](https://github.com/NeilARaman/superpowers) framework — a set of structured, reusable behavioral skills that guide AI agents to follow disciplined software engineering workflows.

[中文版本](#中文说明) | [English](#english)

---

## English

### What is This?

[Superpowers](https://github.com/NeilARaman/superpowers) is a skills framework originally designed for Claude. This repository contains the same skills **rewritten and adapted for [Antigravity](https://antigravity.google/)** — Google DeepMind's agentic AI coding assistant.

Each skill is a `SKILL.md` file that:
- Defines **when** the skill should be invoked (via YAML `description` frontmatter)
- Explains **how** the agent should behave when the skill is active
- Is automatically surfaced to the Antigravity agent based on the task context

### Skills

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

### How It Works

Antigravity surfaces skills automatically based on their YAML `description` field. When a relevant skill appears in the agent's context, the agent **must** use `view_file` to read the full `SKILL.md` before taking any action.

```yaml
# Example SKILL.md frontmatter
---
name: systematic-debugging
description: Use when diagnosing unexpected behavior, failing tests, or unclear errors - before making any code changes
---
```

The `using-superpowers` skill enforces a strict rule: **if there is even a 1% chance a skill applies, the agent must read and follow it.**

### Usage

#### Option 1: Copy skills into your project

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

#### Option 2: Clone and reference

```bash
git clone https://github.com/tison-g/superpowers-Antigravity.git
```

Then copy or symlink the `skills/` directory into your working project.

### Differences from the Original Superpowers

The original Superpowers repository is designed for Claude's tool-calling model. This adaptation makes the following changes for Antigravity:

- **Tool references updated**: All tool invocations reference Antigravity's specific tools (`view_file`, `browser_subagent`, `run_command`, `task_boundary`, `notify_user`, etc.)
- **Subagent model**: Rewritten to use Antigravity's `browser_subagent` dispatching pattern instead of Claude's native parallel tool calls
- **Task tracking**: Integrated with Antigravity's `task_boundary` and `task.md` workflow
- **File access**: Updated to use Antigravity's `view_file` skill-loading convention

### Contributing

If you adapt, improve, or create new skills for Antigravity, contributions are welcome! Please follow the `writing-skills` skill guide when creating new skills.

### Credits

- Original [Superpowers](https://github.com/NeilARaman/superpowers) framework by the Superpowers contributors
- Antigravity adaptation maintained in this repository

### License

MIT

---

## 中文说明

本仓库收录了一套**适配 Antigravity 的技能（Skills）**，改编自 [Superpowers](https://github.com/NeilARaman/superpowers) 框架 —— 一套结构化、可复用的行为技能，用于引导 AI Agent 遵循严谨的软件工程工作流。

### 这是什么？

[Superpowers](https://github.com/NeilARaman/superpowers) 原本是为 Claude 设计的技能框架。本仓库将其中的所有技能**重写并适配为 [Antigravity](https://antigravity.google/)** 专用版本 —— Antigravity 是 Google DeepMind 推出的智能体 AI 编程助手。

每个技能都是一个 `SKILL.md` 文件，包含：
- **何时**调用该技能（通过 YAML `description` 字段声明触发条件）
- **如何**根据该技能调整 Agent 的行为
- 技能会由 Antigravity 根据任务上下文自动识别并推送给 Agent

### 技能列表

| 技能 | 说明 |
|------|------|
| [`brainstorming`](./skills/brainstorming/SKILL.md) | 在任何实现或规划之前进行结构化的创意探索 |
| [`dispatching-parallel-agents`](./skills/dispatching-parallel-agents/SKILL.md) | 安全地并行派发多个子 Agent 执行独立子任务 |
| [`executing-plans`](./skills/executing-plans/SKILL.md) | 按步骤系统地执行已写好的计划 |
| [`finishing-a-development-branch`](./skills/finishing-a-development-branch/SKILL.md) | 规范地完成功能分支（评审、测试、合并准备） |
| [`receiving-code-review`](./skills/receiving-code-review/SKILL.md) | 优雅地接收、处理并应用代码评审反馈 |
| [`requesting-code-review`](./skills/requesting-code-review/SKILL.md) | 准备并向协作者发起全面的代码评审请求 |
| [`subagent-driven-development`](./skills/subagent-driven-development/SKILL.md) | 通过向专注子 Agent 委派任务来架构复杂工作 |
| [`systematic-debugging`](./skills/systematic-debugging/SKILL.md) | 用根因追踪法系统调试，而非盲目猜测 |
| [`test-driven-development`](./skills/test-driven-development/SKILL.md) | 先写测试再实现，遵循 RED-GREEN-REFACTOR 循环 |
| [`using-git-worktrees`](./skills/using-git-worktrees/SKILL.md) | 用 Git worktree 实现并行开发，无需频繁切换分支 |
| [`using-superpowers`](./skills/using-superpowers/SKILL.md) | 元技能：如何正确查找和调用其他技能 |
| [`verification-before-completion`](./skills/verification-before-completion/SKILL.md) | 在宣布任务完成前验证所有需求均已满足 |
| [`writing-plans`](./skills/writing-plans/SKILL.md) | 在编码前写出清晰、结构化的实现计划 |
| [`writing-skills`](./skills/writing-skills/SKILL.md) | 使用 TDD 适配的技能开发生命周期创建新技能 |

### 工作原理

Antigravity 会根据 YAML `description` 字段自动识别相关技能。当某个技能出现在 Agent 的上下文中时，Agent **必须**先用 `view_file` 工具读取完整的 `SKILL.md` 文件，再采取任何行动。

```yaml
# SKILL.md frontmatter 示例
---
name: systematic-debugging
description: Use when diagnosing unexpected behavior, failing tests, or unclear errors - before making any code changes
---
```

`using-superpowers` 技能执行一条严格规则：**只要有哪怕 1% 的可能性某个技能适用，Agent 就必须读取并遵循它。**

### 使用方式

#### 方式一：将 skills 复制到你的项目中

将 `skills/` 目录复制到项目根目录，Antigravity 将自动识别并激活这些技能。

```
your-project/
├── skills/
│   ├── systematic-debugging/
│   │   └── SKILL.md
│   ├── test-driven-development/
│   │   └── SKILL.md
│   └── ...
└── 你的代码...
```

#### 方式二：克隆仓库后引用

```bash
git clone https://github.com/tison-g/superpowers-Antigravity.git
```

然后将 `skills/` 目录复制或软链接到你的工作项目中。

### 与原版 Superpowers 的区别

原版 Superpowers 仓库是为 Claude 的工具调用模型设计的。本适配版针对 Antigravity 做了以下修改：

- **工具引用更新**：所有工具调用均更新为 Antigravity 的专有工具（`view_file`、`browser_subagent`、`run_command`、`task_boundary`、`notify_user` 等）
- **子 Agent 模型**：改写为使用 Antigravity 的 `browser_subagent` 派发模式，而非 Claude 的原生并行工具调用
- **任务追踪**：集成了 Antigravity 的 `task_boundary` 和 `task.md` 工作流
- **文件访问**：更新为使用 Antigravity 的 `view_file` 技能加载规范

### 贡献

如果你为 Antigravity 适配、改进或创建了新技能，欢迎提交贡献！请遵循 `writing-skills` 技能指南创建新技能。

### 致谢

- 原始 [Superpowers](https://github.com/NeilARaman/superpowers) 框架由 Superpowers 贡献者创建
- Antigravity 适配版由本仓库维护

### 许可证

MIT
