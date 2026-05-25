# Contributing to Mevrik

You're reading this because you have access to a Mevrik repository. This is the working contract for every change.

The rules are short. They are also non-negotiable — they encode the GitHub Plan v2.0, which is paired with the Engineering Blueprint v2.0.

## Before your first PR

1. Read the **Engineering Blueprint v2.0** (`ax-docs/Mevrik_AX_3.0_Engineering_Blueprint.md`). Don't skim. The architecture and rules below only make sense in that context.
2. Read the **GitHub Plan v2.0** (`ax-docs/Mevrik_AX_3.0_GitHub_Plan.md`). Especially §10 (daily workflow), §11 (security), §12 (CODEOWNERS), §16 (do's and don'ts).
3. Read `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and `SECURITY.md` in this org.
4. Configure your local git for signed commits (see Setup section below).
5. Ask any clarifying questions in `#engineering` on Slack. Better to ask before coding than to rework after review.

## Setup — one time

```bash
# 1. GPG signing — required for every commit
gpg --full-generate-key   # RSA 4096, no expiry on the work key
gpg --armor --export <YOUR_EMAIL> | gh gpg-key add -

git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true
git config --global tag.gpgsign true

# 2. Pre-commit hook — enforces the Blueprint ↔ GitHub Plan version contract
git config core.hooksPath .githooks   # run from repo root after clone

# 3. Conventional Commits — pick a linter
brew install commitlint     # or your platform equivalent
```

## Working on a change

### Branch naming

Five prefixes. Match Conventional Commits:

- `feat/short-kebab-description`
- `fix/short-kebab-description`
- `chore/...`
- `refactor/...`
- `docs/...`

Max branch lifetime: **2 days**. If you need longer, the work is too big — split it behind a feature flag.

### Commit messages

Conventional Commits. `type(scope): subject` — subject under 72 chars. Body explains the **why**.

```
feat(conversations): add bulk reassign action for inbox

Adds Cmd+R keyboard shortcut to bulk-reassign selected conversations
to a different agent. Adds /v1/conversations/batch-assign endpoint.

Closes #234
```

Every commit must be **signed** (`-S` is implied by the global config above). Unsigned commits are rejected by branch protection.

### Pull requests

- Use the template in `.github/pull_request_template.md`. Fill it out — the Product × Edition impact and Layer impact checkboxes matter.
- One approving review minimum. Two on CODEOWNERS-protected paths.
- All CI checks must pass. No exceptions.
- All review conversations resolved before merge.
- **Squash merge only.** Merge commits and rebase-merges are disabled at the repo level.
- Reviews within 24 hours during the work week. Stale PRs (>48h) get pinged in Slack.

### Code review etiquette

- Comment on the code, not on the engineer.
- Suggest with code blocks (` ```suggestion `) when you can.
- "nit:" for taste-level comments — never a blocker by themselves.
- Approve when you'd be happy to maintain the change. Request changes when something needs to change before merge.
- If you're a CODEOWNER and the PR sits without your review for 24h, the author will (correctly) ping you.

## The six rules — repeated here because they matter

From the Blueprint, encoded in every CI pipeline:

1. **One codebase.** No forks. Editions differ in config, never in code.
2. **Tenant-first data.** Every business table has `tenant_id`. Postgres RLS is on.
3. **Same image, four editions.** No per-edition Dockerfile. Configuration alone decides the mode.
4. **Engine independence.** The six Mevrik primitives (`MevrikTool`, `MevrikSkill`, `MevrikHook`, `MevrikMemory`, `MevrikContextCurator`, `MevrikModelHub`) are the contract. Write against them, never against the SDK underneath.
5. **Schema-first contracts.** gRPC + Protocol Buffers for inter-service. REST + OpenAPI for external. No tRPC.
6. **Capability matrix is law.** No tier checks outside `packages/capabilities/`. Linters block this at commit time.

## Things that will get your PR rejected

- Unsigned commits.
- Pushing to `main` directly. You can't; branch protection blocks it. Don't try.
- Adding yourself as a temporary reviewer to bypass CODEOWNERS.
- Referencing `TIER` directly in code instead of using `caps('feature').propertyName`.
- Importing from `_saas-only/` in shared code.
- Using `AWS_S3_CLIENT` (or any cloud SDK) directly instead of the adapter in `packages/adapters/`.
- Committing secrets. (Secret scanning push protection blocks this at the push, but don't rely on the safety net.)
- Touching `services/_trust/`, `services/_harness/primitives/`, `services/_foundation/auth/`, `services/_foundation/tenancy/`, `packages/license/`, or `services/_models/spark-cx/` without `@princemojumder` review.
- Schema or query changes without tenant isolation tests passing.

## Things that will make your reviewers happy

- Tests in the same PR as the code.
- Documentation updates in the same PR as the code.
- An ADR (`ax-docs/adrs/`) for any decision that's hard to reverse.
- An audit event emitted from any user-facing state change.
- A clear "How to test" section in the PR description.

## Cross-repo changes

Changes that span repos (e.g., a Cortex contract change that ax-platform depends on):

1. Open the PR on the lower repo first (e.g., `ax-cortex`).
2. Reference the dependent PR in `ax-platform` ("Depends on mevriklabs/ax-cortex#456").
3. Merge order: lower repo first, then the dependent one.
4. Document the contract change in `ax-docs/adrs/`.

## Working with AI in code review

We use Claude internally. You can ask Claude to help write code, explain code, review your own draft, or suggest test cases. You **cannot** paste customer data, secrets, or unreleased pricing into a chat. Treat Claude as a smart, leaky pair-programmer. Same rules as a public forum.

We may add CodeRabbit (or similar) as a non-blocking PR reviewer. Its comments are advisory; humans still decide.

## Questions

- Code questions: `#engineering` in Slack.
- Process or this contributing guide: `#meta` in Slack.
- Disputes: escalate to `@princemojumder` or, for code of conduct issues, `conduct@mevrik.com`.

Welcome aboard.
