# OpenSpec Superpowers Skill

A lightweight coordinator skill for Codex that combines OpenSpec with Superpowers.

Use OpenSpec for the product-change record: proposals, designs, specs, tasks, validation, and PR/archive conventions. Use Superpowers for the engineering discipline: brainstorming, TDD, systematic debugging, review handling, and verification before completion.

This repository does not vendor OpenSpec or Superpowers. It provides one coordinator skill that tells Codex when and how to load those more specific skills together.

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
- The `openspec-workflow` skill
- Superpowers skills, especially `using-superpowers`, `brainstorming`, `test-driven-development`, `systematic-debugging`, and `verification-before-completion`
- OpenSpec CLI for repositories that use OpenSpec
- `git`
- GitHub CLI (`gh`) if you want PR publishing
- Claude Code CLI if your `openspec-workflow` setup delegates implementation through Claude Code

If some dependencies are missing, Codex can still read this skill, but it will behave as a high-level guide instead of loading the detailed workflow skills.

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
