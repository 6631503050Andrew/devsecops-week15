# DevSecOps — Week 15 (Software Security, KOSEN69)

Standalone repo for the Week 15 DevSecOps lab — **Break the Build** (Red vs Blue).

## Security gate
`.github/workflows/security-ci.yml` runs on every push / PR to `main`:

| Job | Tool | Scans for |
|-----|------|-----------|
| `semgrep`  | Semgrep  | Insecure code patterns (SAST) |
| `trivy`    | Trivy    | Vulnerable deps (SCA) + IaC/Dockerfile misconfig + secrets |
| `gitleaks` | Gitleaks | Hard-coded secrets in code + git history |

Each tool runs **report-then-gate**: a report step uploads SARIF to the GitHub
**Security** tab (`if: always()`), then a gate step **fails the build** on
HIGH/CRITICAL findings (or any secret / any Semgrep finding).

## Services
- `secure_service.py` — fail-**closed** `/admin` + structured security logging (OWASP A09 / A10, CWE-636).
- `sample-service.py` — logging + fail-closed demo.

The deliberately **insecure** counterpart (fail-open) is run locally from the
course lab folder for the Break-the-Build demo (not committed here, so the gate
can go green).

---
*Student: Andrew Dicesare — 6631503050 · KOSEN69 Software Security Week 15.*
