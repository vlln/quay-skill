# quay-skill

Agent Skills for querying Quay.io repositories, tags, digests, and pullable
container image references.

This repository stores skills under `skills/`. Each skill follows the
[Agent Skills specification](https://agentskills.io/specification) and can be
used by skills-compatible agents.

## Skills

| Skill | Description |
|-------|-------------|
| [`quay`](skills/quay) | Search Quay.io repositories, list image tags, inspect tag metadata, and resolve pullable quay.io image references for public or token-visible containers. |

## Quick Start

Paste this into your AI agent (Claude Code, Cursor, OpenAI Assistants, etc.):

```text
Install the Agent Skills from https://raw.githubusercontent.com/vlln/quay-skill/main/README.md
```

## Installation

Recommended: install these skills with
[`skit`](https://github.com/vlln/skit). It fetches skills from the published
repository, keeps a lock file, and can diagnose declared requirements.

### skit

Install `skit` with Homebrew:

```sh
brew install --cask vlln/tap/skit
```

For other platforms, see the
[`skit` installation instructions](https://github.com/vlln/skit#installation).

Install the Quay skill:

```sh
skit install --global vlln/quay-skill/skills/quay
```

Install all skills in this repository:

```sh
skit install --global vlln/quay-skill --all
```

### npx skills

```sh
npx skills add vlln/quay-skill
```

### Manual

Copy the desired skill directory from `skills/quay` into your agent's skills
directory, then restart the agent if required.

Common locations:

- Codex CLI: `~/.codex/skills`
- Claude Code: `.claude/skills` in the project, or the configured user skills directory
- OpenCode: `~/.opencode/skills/quay-skill`

## Requirements

- Python 3
- Network access to the Quay API
- Optional: `QUAY_TOKEN` for private or restricted repositories
- Optional: `QUAY_API_URL` for Quay Enterprise instances

## License

MIT
