<!--
Default PR template for all mevriklabs repositories.
Lives in .github/.github/pull_request_template.md and is inherited by every repo
unless that repo overrides it with its own .github/pull_request_template.md.
-->

## What this PR does

<!-- Brief description of the change. One or two sentences. -->

## Why this change is needed

<!-- Context. Link to ticket, design doc, ADR, or discussion. -->

## How to test

<!-- Step-by-step verification a reviewer can follow without asking you. -->

## Product × Edition impact

- [ ] Affects Mevrik AI Agent · Cloud
- [ ] Affects Mevrik AX · Cloud+
- [ ] Affects Mevrik AX · Private Cloud
- [ ] Affects Mevrik AX · Sovereign

## Layer impact

- [ ] Touches `services/_harness/primitives/`      (founder review required)
- [ ] Touches `services/_trust/`                   (founder review required)
- [ ] Touches `services/_foundation/auth/`         (founder review required)
- [ ] Touches `services/_foundation/tenancy/`      (founder review required)
- [ ] Touches `packages/license/`                  (founder review required)
- [ ] Touches `packages/capabilities/`             (matrix snapshot review)
- [ ] Touches `services/_models/spark-cx/`         (founder review required)

## Checklist

- [ ] Tests added or updated
- [ ] Documentation updated if needed (same PR — not "later")
- [ ] No secrets committed
- [ ] License key impact considered
- [ ] Audit trail emission added (if user-facing action)
- [ ] Cortex contract changes documented (if cross-repo)
- [ ] Tenant isolation tests pass (if schema or query change)
- [ ] Commits are signed
- [ ] No `TIER` references outside `packages/capabilities/`
- [ ] No imports from `_saas-only/` in shared code
- [ ] No cloud SDKs (`aws-sdk`, etc.) outside `packages/adapters/`

## Related

<!-- Issue numbers, design docs, dependent PRs in other repos. -->

Closes #
