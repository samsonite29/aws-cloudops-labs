# Diagrams

Architecture diagrams for the labs in this repo.

## Naming

Match the lab path, flattened with hyphens, plus the diagram format:

```
<domain-number>-<domain>-<lab>.<ext>
```

Examples:

- `04-security-iam-baseline.drawio` — editable source
- `04-security-iam-baseline.png` — exported image referenced from the lab README
- `05-networking-vpc-endpoints.mmd` — Mermaid source

## Conventions

- Keep both the **source** (`.drawio`, `.mmd`, etc.) and the **exported image** (`.png` / `.svg`) so diagrams stay editable.
- Prefer `.svg` exports where the tool supports it — they render crisply on GitHub and stay diff-friendly.
- Only diagram labs where the wiring isn't obvious from the code. A single CloudWatch alarm doesn't need a picture; a VPC with interface and gateway endpoints does.
- Reference the diagram from the relevant lab README, e.g. `![IAM baseline](../../diagrams/04-security-iam-baseline.svg)`.
