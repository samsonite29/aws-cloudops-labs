# aws-cloudops-labs

Terraform implementations of the hands-on labs from the [AWS Certified CloudOps Engineer Associate (SOA-C03)](https://www.udemy.com/course/aws-certified-cloudops-associate/) course.

Where the course walks through a task in the AWS console, this repo does it as infrastructure-as-code instead. The goal is to treat each lab the way I'd treat real infrastructure — versioned, reproducible, and reviewable — rather than as one-off clickops. Each lab directory has its own README explaining what it provisions and, where relevant, why I'd reach for code over the console.

## Tooling

- **Terraform** `>= 1.7`
- **AWS provider** `~> 5.0`
- **AWS CLI** for authentication and out-of-band verification
- `terraform fmt` / `validate` enforced via pre-commit and CI

## Repository layout

```
.
├── modules/
├── labs/
│   ├── 01-monitoring/
│   ├── 02-reliability/
│   ├── 03-deployment/
│   ├── 04-security/
│   ├── 05-networking/
│   └── 06-cost-performance/
├── .github/workflows/      # fmt-check + validate on every push
├── .pre-commit-config.yaml
└── .gitignore
```

Each lab is self-contained: its own `main.tf`, `variables.tf`, `outputs.tf`, and `README.md`. You can `cd` into any lab and run it independently.

## Lab index

Labs are grouped by the SOA-C03 exam domains. The table fills in as I work through the course.

| Domain | Lab | What it provisions |
|---|---|---|
| Monitoring & Logging | `labs/01-monitoring/cloudwatch-alarms` | CloudWatch metric alarms, SNS notification topic |
| Monitoring & Logging | `labs/01-monitoring/log-aggregation` | CloudWatch Logs groups, metric filters, subscription |
| Reliability & Continuity | `labs/02-reliability/autoscaling` | Launch template, ASG, target tracking policy |
| Reliability & Continuity | `labs/02-reliability/backup` | AWS Backup vault, plan, and selection |
| Deployment & Automation | `labs/03-deployment/ssm-automation` | SSM documents, patch baseline, maintenance window |
| Deployment & Automation | `labs/03-deployment/cloudformation-vs-tf` | Equivalent stack expressed in Terraform |
| Security & Compliance | `labs/04-security/iam-baseline` | IAM roles, policies, permission boundaries |
| Security & Compliance | `labs/04-security/config-rules` | AWS Config recorder, managed + custom rules |
| Networking & Delivery | `labs/05-networking/vpc-endpoints` | VPC, interface/gateway endpoints, route tables |
| Networking & Delivery | `labs/05-networking/cloudfront` | CloudFront distribution, OAC, S3 origin |
| Cost & Performance | `labs/06-cost-performance/budgets` | AWS Budgets, cost anomaly detection |

## Running a lab

```bash
cd labs/01-monitoring/cloudwatch-alarms
terraform init
terraform plan
terraform apply
```

Each lab uses a local backend by default to keep setup friction low. The remote backend block (S3 + DynamoDB lock table) is included but commented in `backend.tf` so you can see how I'd wire it for shared state.

> **Cost note:** Some labs create billable resources. Run `terraform destroy` when you're done with a lab. Anything left running is on you, not the README.

## State and secrets

- `*.tfstate`, `*.tfstate.*`, and `.terraform/` are gitignored — state never lands in the repo.
- No credentials are committed. Authentication is expected via your AWS CLI profile or environment variables.
- Variables that would carry account-specific values are declared in `variables.tf` with no committed `.tfvars`.

## Conventions

- Every resource is tagged with a common tag set (`Project`, `Lab`, `ManagedBy = "terraform"`) via a shared `default_tags` block on the provider.
- Reusable patterns are pulled into `modules/` rather than copy-pasted between labs.
- `terraform fmt` and `terraform validate` pass cleanly on every commit; CI fails the build otherwise.

## Why this repo exists

The CloudOps cert covers a lot of operational ground — monitoring, patching, backup, networking, cost control. Working through it as Terraform forced me to think about each topic in terms of lifecycle, drift, and reproducibility instead of a sequence of console clicks. The per-lab notes capture those trade-offs where they came up.
