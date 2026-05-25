# Security Policy

Mevrik treats security as a feature, not an afterthought. This policy is enforced across every repository in the `mevriklabs` organisation.

## Reporting a vulnerability

**Do not open public GitHub issues for security vulnerabilities.**

Report privately to **security@mevrik.com** with:

- A clear description of the issue.
- Steps to reproduce, or a proof-of-concept.
- Affected component(s) — repository, service, version.
- Your name and contact preference (we credit reporters who want it).

We acknowledge reports within **2 business days** and provide an initial assessment within **5 business days**.

Alternatively, use GitHub's [private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability) on the relevant repository.

## Scope

In scope:

- All `mevriklabs/ax-*` repositories.
- Mevrik AI Agent (SaaS) production endpoints.
- Mevrik AX deployments where Mevrik is the operator.
- Customer-deployed Mevrik AX (Private Cloud / Sovereign) — coordinate with the customer first.

Out of scope:

- Third-party SaaS we use (report to them directly).
- Social engineering, physical attacks, denial-of-service.
- Vulnerabilities in customer-modified forks.
- Issues requiring a privileged position already obtained by other means.

## Disclosure timeline

- We aim to patch high-severity issues within **7 days** and medium within **30 days** of confirmation.
- Public disclosure is coordinated with the reporter, typically **90 days** after confirmation or after a patch is released, whichever is sooner.
- We do not pursue legal action against good-faith researchers who respect this policy.

## Supported versions

| Product | Edition | Versions receiving security fixes |
|---|---|---|
| Mevrik AI Agent | Cloud | Always current — no version pinning for SaaS. |
| Mevrik AX | Cloud+ | Always current — no version pinning. |
| Mevrik AX | Private Cloud | Latest two quarterly releases (e.g. 26.5 and 26.8). |
| Mevrik AX | Sovereign | Latest two quarterly releases. Critical-severity patches backported to one release prior. |

## Internal controls

The engineering practices that back this policy:

- **Branch protection** on `main` and `release/*` — required PRs, signed commits, status checks, no force push, no bypass.
- **Secret scanning + push protection** on every repository.
- **Dependabot security updates** triaged within 7 days (high) / 30 days (medium).
- **CodeQL** on every PR.
- **Container scanning** (Trivy) on every built image.
- **SBOM** generated for every release build (CycloneDX).
- **Image signing** (cosign / Sigstore) on every production image.
- **SLSA Level 2** minimum for application repos; **Level 3** for Sovereign artifacts.
- **OIDC** for cloud authentication — no long-lived credentials in GitHub secrets.
- **Quarterly access reviews** — documented in `ax-docs/security/access-reviews/`.
- **Weekly audit log review** — documented in `ax-docs/security/audit-log-reviews/`.

## Compliance

Mevrik is targeting SOC 2 Type II. Control mapping is documented in `ax-docs/security/soc2-control-map.md`. GDPR-related procedures are in `ax-docs/security/gdpr/`. The trust centre at `trust.mevrik.com` publishes our current posture.

## Contact

`security@mevrik.com` · PGP key fingerprint published at `trust.mevrik.com/pgp`.
