<h1 align="center">quay-skill</h1>

<p align="center">
  <strong>Agent Skills for querying Quay.io container registries.</strong><br/>
  Search repositories, list image tags, inspect tag metadata, and resolve pullable
  quay.io image references — all from your AI agent.
</p>

<p align="center">
  <a href="https://github.com/vlln/quay-skill/stargazers"><img src="https://badgen.net/github/stars/vlln/quay-skill?label=%E2%98%85" alt="GitHub stars" /></a>
  <img src="https://badgen.net/badge/license/MIT/blue" alt="MIT" />
  <img src="https://badgen.net/badge/spec/Agent%20Skills/8257D0" alt="Agent Skills spec" />
</p>

---

## Installation

### [skit](https://github.com/vlln/skit) (Recommended)

```bash
skit install https://github.com/vlln/quay-skill/tree/main/skills/quay
```

To install all skills in this repository:

```bash
skit install --global vlln/quay-skill --all
```

### [skill.sh](https://github.com/vercel-labs/skills)

```bash
npx skills add vlln/quay-skill
```

### Manually

| Agent | Command |
|-------|---------|
| **Claude Code** | `cp -r skills/quay .claude/skills/` |
| **Codex** | `cp -r skills/quay ~/.codex/skills/` |
| **OpenCode** | `git clone https://github.com/vlln/quay-skill.git ~/.opencode/skills/quay-skill` |
| **Kimi** | `cp -r skills/quay ~/.kimi/skills/` |

---

## Skills

| Skill | Description |
|-------|-------------|
| [quay](skills/quay/SKILL.md) | Search Quay.io repositories, list image tags, inspect tag metadata, and resolve pullable quay.io image references for public or token-visible containers. |

## Requirements

- Python 3
- Network access to the Quay API
- Optional: `QUAY_TOKEN` for private or restricted repositories
- Optional: `QUAY_API_URL` for Quay Enterprise instances

## License

MIT