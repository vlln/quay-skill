---
name: quay
description: Use this skill when you need to search Quay.io repositories, list image tags, inspect tag metadata, or resolve pullable quay.io image references for public or token-visible containers.
license: MIT
metadata:
  author: vlln
  version: "0.1.0"
requires:
  bins:
    - python3
---

# Quay Skill

Query the Quay.io container registry API for repository discovery, tag
inspection, and pull reference resolution.

## Trigger Keywords

quay, quay.io, container registry, image tags, container images, docker pull,
podman pull, manifest digest, image digest, repository search

## When To Use

Use for generic Quay.io registry operations: search repositories, list tags,
inspect tag metadata, resolve pull references.

Prefer the `biocontainers` skill for BioContainers tool discovery, upstream
version resolution, and GA4GH TRS workflows.

## Capabilities

- **Search** repositories by name or keyword, optionally scoped to a namespace.
- **Inspect** a repository to see metadata, visibility, and description.
- **List tags** for a repository, showing tag names, sizes, modification dates,
  and digests.
- **Inspect a tag** to get the full manifest digest and pull commands.

All operations are available through the `scripts/quay` CLI. Run
`scripts/quay help` for complete usage.

## Configuration

- `QUAY_TOKEN` — Bearer token for authenticating to private or restricted
  repositories.
- `QUAY_API_URL` — Override the API base URL for Quay Enterprise deployments.
  Default: `https://quay.io/api/v1`.

## Output

Always include the exact `quay.io/<namespace>/<repo>:<tag>` reference and the
full manifest digest when reporting results. If a search returns multiple
plausible repositories, present the ambiguity explicitly rather than guessing.

## Gotchas

- Tag listing is paginated. Use `--all` to fetch every page, or `--page` to
  target a specific page.
- Tag inspection scans tags sequentially (no direct tag-lookup API endpoint).
  It can be slow for repositories with thousands of tags.
- Manifest digests shown in the tag listing table are truncated for readability.
  Use tag inspection (`<namespace>/<repo>:<tag>`) for the full digest.
- Search results only include public repositories unless `QUAY_TOKEN` is set
  and the token grants access to private repos.
- Enterprise Quay instances may use different API paths. Set `QUAY_API_URL`
  correctly for self-hosted deployments.