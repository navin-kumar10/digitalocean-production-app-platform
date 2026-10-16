# Architecture - DigitalOcean Production Application Platform

![architecture](architecture.png)

*Portfolio - low-cost production path* | DigitalOcean - DOKS - Managed DBs

## Diagram

See architecture.png (source: files/06_digitalocean_app_platform.png).

```mermaid
flowchart LR
  User --> LB --> DOKS[DOKS] --> DB[(Managed DB)]
```

## Decisions

1. Reproducibility first - infra as code is source of truth.
2. Env separation: dev < staging < prod, per-env tfvars/state, prod approval.
3. Least privilege IAM/RBAC, OIDC in CI, no checked-in secrets.
4. Defense in depth: validation + authn/z + throttling + TLS + encryption + scans.
5. Observability: structured logs, correlation IDs, RED/USE metrics, runbook-linked alerts.
6. Cost awareness: small lab sizes, retention/lifecycle limits, Budgets alerts.
7. Lab labeling: sample apps are small; verify claims via tests/.

## Troubleshooting

- plan auth error: check profile/region, sts get-caller-identity.
- state lock: confirm no active apply before force-unlock.
- smoke 4xx/5xx: check env vars/secrets.
- cost surprise: make destroy + verify console (LB/DB/cluster/bucket/zone/WAF).
