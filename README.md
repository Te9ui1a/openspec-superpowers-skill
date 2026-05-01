# OpenSpec Superpowers Skill

A lightweight coordinator skill for Codex that combines OpenSpec with Superpowers.

Use OpenSpec for the product-change record: proposals, designs, specs, tasks, validation, and PR/archive conventions. Use Superpowers for the engineering discipline: brainstorming, TDD, systematic debugging, review handling, and verification before completion.

This repository does not vendor OpenSpec or Superpowers. It provides one coordinator skill that tells Codex when and how to load those more specific skills together.

## Hard Dependencies

This skill is intentionally not standalone. It assumes these prerequisites are installed and discoverable by your agent:

- [OpenSpec](https://github.com/Fission-AI/OpenSpec), including the OpenSpec CLI for repositories that use OpenSpec.
- An OpenSpec workflow skill named `openspec-workflow`, or an equivalent local skill that teaches your agent how to create and manage OpenSpec `proposal.md`, `design.md`, `specs/*/spec.md`, and `tasks.md` artifacts.
- [Superpowers](https://github.com/obra/superpowers), including the process skills this coordinator references.

Minimum Superpowers skills expected by this coordinator:

- `using-superpowers`
- `brainstorming`
- `test-driven-development`
- `systematic-debugging`
- `verification-before-completion`

Recommended Superpowers skills for the full workflow:

- `problem-statement`
- `user-story`
- `prd-development`
- `receiving-code-review`
- `requesting-code-review`
- `finishing-a-development-branch`

If these dependencies are missing, install them first. Without them, this skill can only provide a high-level outline and cannot deliver its intended workflow.

## What This Is

- A Codex skill named `openspec-superpowers`
- A traffic controller for OpenSpec-driven product changes
- A way to make behavior-changing work consistently go through OpenSpec artifacts and Superpowers process gates

## What This Is Not

- A replacement for `openspec-workflow`
- A replacement for Superpowers skills
- A bundled OpenSpec CLI installer
- An official OpenSpec or Superpowers project

## Prerequisites

For the full workflow, install and configure:

- Codex with local skills support
- [OpenSpec](https://github.com/Fission-AI/OpenSpec) CLI for repositories that use OpenSpec
- The `openspec-workflow` skill
- [Superpowers](https://github.com/obra/superpowers) skills, especially `using-superpowers`, `brainstorming`, `test-driven-development`, `systematic-debugging`, and `verification-before-completion`
- `git`
- GitHub CLI (`gh`) if you want PR publishing
- Claude Code CLI if your `openspec-workflow` setup delegates implementation through Claude Code

If the required OpenSpec or Superpowers skills are missing, install them before using this coordinator.

## Installation

Clone this repository and copy the skill folder into your Codex skills directory:

```bash
git clone https://github.com/Te9ui1a/openspec-superpowers-skill.git
mkdir -p ~/.codex/skills
cp -R openspec-superpowers-skill/openspec-superpowers ~/.codex/skills/
```

Restart Codex or reload skills if your client requires it.

## Usage

Invoke it explicitly when a repository uses OpenSpec and the requested change may affect product behavior:

```text
Use $openspec-superpowers to implement this feature with OpenSpec and Superpowers discipline.
```

Or:

```text
This repo uses OpenSpec. For this behavior change, use $openspec-superpowers.
```

The skill will direct Codex to:

1. Load Superpowers process guidance.
2. Decide whether OpenSpec is required.
3. Use `openspec-workflow` for proposal, design, spec, task, validation, PR, and archive conventions.
4. Use Superpowers skills for TDD, debugging, review, and verification gates.
5. Report the OpenSpec change name, artifacts, implementation summary, verification commands, and any deviations.

## Repository Layout

```text
openspec-superpowers-skill/
├── openspec-superpowers/
│   ├── SKILL.md
│   └── agents/
│       └── openai.yaml
├── examples/
│   └── prompts.md
├── LICENSE
└── README.md
```

## License

MIT
