# Tailwind Color Arbitrary

Agent skill for migrating project-defined Tailwind color-token classes to equivalent literal arbitrary-value classes, checking UI equivalence, and removing unused color tokens only after verification and explicit user approval.

Built using the open [Agent Skills](https://agentskills.io) format.

## Features

- Reads project CSS and inventories defined Tailwind color tokens.
- Scans active source files and reports token usage locations and counts.
- Proposes exact class replacements using literal color values.
- Presents a complete migration plan and waits for explicit user confirmation before editing.
- Verifies remaining usages, project checks, and UI appearance before token removal.
- Removes only approved token declarations with no remaining consumers.

## Requirements

- Node.js and npm to install the skill.
- A supported agent: OpenCode, Claude Code, or Codex.

## Install

Run from the target project root:

```sh
npx skills add makkio-id/tailwind-color-arbitrary -a opencode -a claude-code -a codex -y
```

Install for one agent by specifying only that agent. For example:

```sh
npx skills add makkio-id/tailwind-color-arbitrary -a opencode -y
```

Omit `-y` to choose installation options interactively. To update the skill, run the install command again.

## Usage

Invoke the `tailwind-color-arbitrary` skill from the target project and request migration of Tailwind color tokens. The agent inventories tokens, usages, counts, and proposed literal arbitrary classes, then asks for confirmation before making changes.

## Skill contents

- `SKILL.md` — discovery, proposal and confirmation gate, migration, verification, and token-removal workflow.
