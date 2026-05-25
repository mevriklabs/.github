# Mevrik Labs

**Mevrik AX — the Agentic eXperience platform.** AI runs your customer experience. Humans supervise what matters.

This organisation hosts the engineering repositories for Mevrik AX 3.0. All repositories are private. Access is granted on a least-privilege basis to members of `@mevriklabs/ax-backend`, `@mevriklabs/ax-frontend`, and `@mevriklabs/ax-reader`.

## The codebase

One platform, two products, four editions, shipped from seven repositories:

| Repo | What lives here | Primary owner |
|---|---|---|
| [`ax-platform`](https://github.com/mevriklabs/ax-platform) | User-facing modules · foundation · trust · agent harness · channels · integrations | `@ax-backend` + `@ax-frontend` |
| [`ax-cortex`](https://github.com/mevriklabs/ax-cortex) | Intelligence orchestration · memory · multi-LLM router · Reflex · RAG · BYOK | `@ax-backend` |
| [`ax-models`](https://github.com/mevriklabs/ax-models) | Mevrik CX Model Suite — Spark CX 1.0 + 9 specialists | `@ax-backend` |
| [`ax-deploy`](https://github.com/mevriklabs/ax-deploy) | Helm · Terraform · Argo · runbooks | `@princemojumder` |
| [`ax-docs`](https://github.com/mevriklabs/ax-docs) | Blueprint · GitHub Plan · ADRs · runbooks · customer docs | everyone |
| [`ax-sdk`](https://github.com/mevriklabs/ax-sdk) | Public SDKs · empty until Phase 2 | `@ax-backend` |
| [`.github`](https://github.com/mevriklabs/.github) | This repo · org-wide policies and templates | `@princemojumder` |

## Engineering documents

The Blueprint and the GitHub Plan are paired under a strict version contract. They share a version number; changing one without the other is a CI failure. Both live in [`ax-docs`](https://github.com/mevriklabs/ax-docs).

- **Mevrik AX 3.0 Engineering Blueprint** — what & why
- **Mevrik AX 3.0 GitHub Plan** — how

## Security

Vulnerability reports: `security@mevrik.com` — see [SECURITY.md](./SECURITY.md). Do not open public issues for security vulnerabilities.

## Contact

`hello@mevrik.com` for general questions. `engineering@mevrik.com` for technical.
