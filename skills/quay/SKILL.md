---
name: quay
description: Search Quay.io repositories, list image tags, inspect tag metadata, and resolve pullable quay.io image references for public or token-visible containers.
compatibility: Requires Python 3 and network access to the Quay API; set QUAY_TOKEN for private or restricted repositories.
metadata:
  skit:
    version: 0.1.0
    requires:
      bins:
        - python3
    keywords:
      - quay
      - containers
      - registry
      - image-tags
---

# Quay Skill

Query the Quay.io API through the bundled CLI for repository discovery, tag
inspection, and pull reference resolution.

## When To Use

Use this skill for generic Quay.io registry tasks: searching repositories,
checking whether `quay.io/<namespace>/<repo>` exists, listing tags, inspecting a
specific tag, and reporting image digests or pull commands.

## Workflow

1. Resolve this skill directory and run the bundled `scripts/quay` helper from there; do not assume `quay` is already on `PATH`.
2. Use `search <query>` when the namespace or repository name is uncertain.
3. Use `inspect <namespace>/<repo>` for repository metadata and visibility.
4. Use `tags <namespace>/<repo>` to list active tags and their digests.
5. Use `inspect <namespace>/<repo>:<tag>` when the user needs an exact pullable image reference or manifest digest.

## Commands

| Command | Description |
|---------|-------------|
| `scripts/quay search <query> [--namespace <name>] [--limit <n>]` | Search public or token-visible repositories. |
| `scripts/quay inspect <namespace>/<repo>` | Show repository metadata. |
| `scripts/quay inspect <namespace>/<repo>:<tag>` | Show tag metadata, digest, and pull command. |
| `scripts/quay tags <namespace>/<repo> [--limit <n>] [--page <n>] [--all]` | List active repository tags. |

## Examples

```bash
scripts/quay search samtools --namespace biocontainers --limit 10
scripts/quay inspect biocontainers/samtools
scripts/quay tags biocontainers/samtools --limit 5
scripts/quay inspect biocontainers/samtools:1.23.1--ha83d96e_0
```

## Rules

- Prefer the `biocontainers` skill for BioContainers tool discovery, upstream version resolution, and GA4GH TRS workflows.
- Use this skill when the task is registry-level Quay work: namespace/repository search, tag lists, tag timestamps, image sizes, manifest digests, or pull references.
- Report `quay.io/<namespace>/<repo>:<tag>` and `manifest_digest` exactly as returned by the API.
- Set `QUAY_TOKEN` only when private or restricted repositories must be queried; do not write tokens into this repository.
- If the API endpoint must be overridden for Quay Enterprise, set `QUAY_API_URL`; otherwise use `https://quay.io/api/v1`.

## Output

Report the matching repository, relevant tag metadata, digest, and the exact
`docker pull` or `podman pull` command the user can run next. Include ambiguity
when search returns multiple plausible repositories.
