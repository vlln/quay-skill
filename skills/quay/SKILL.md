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

Use this skill for generic Quay.io registry tasks: searching repositories,
checking whether `quay.io/<namespace>/<repo>` exists, listing tags, inspecting a
specific tag, and reporting image digests or pull commands.

## Capabilities

- **Search** for repositories by name or keyword, optionally scoped to a namespace.
- **Inspect** a repository to see metadata, visibility, and description.
- **List tags** for a repository, showing tag names, sizes, modification dates, and digests.
- **Inspect a specific tag** to get the full manifest digest and a ready-to-run pull command.

## Output

Report the matching repository, relevant tag metadata, digest, and the exact
`docker pull` or `podman pull` command the user can run next. Include ambiguity
when search returns multiple plausible repositories.

## Configuration

- Set `QUAY_TOKEN` to authenticate for private or restricted repositories. Do not write tokens into this repository.
- Set `QUAY_API_URL` to override the default `https://quay.io/api/v1` endpoint for Quay Enterprise deployments.

## Rules

- Prefer the `biocontainers` skill for BioContainers tool discovery, upstream version resolution, and GA4GH TRS workflows.
- Use this skill when the task is registry-level Quay work: namespace/repository search, tag lists, tag timestamps, image sizes, manifest digests, or pull references.
- Report `quay.io/<namespace>/<repo>:<tag>` and `manifest_digest` exactly as returned by the API.

## Gotchas

- The Quay API paginates tag listings; fetching all tags requires iterating through paginated API responses.
- Tag inspection searches through all tags sequentially (not a direct API call), so it can be slow for repositories with many tags.
- Search results are limited to public repositories unless `QUAY_TOKEN` is set and the token has access to private repositories.
- Enterprise Quay instances may have different API paths; ensure `QUAY_API_URL` is set correctly for self-hosted deployments.
- Manifest digests displayed in the tag listing table are truncated for readability; use tag inspection for the full digest.