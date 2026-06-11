# AZ-104: Microsoft Azure Administrator — Study Guide

A structured study guide for the [AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/credentials/certifications/azure-administrator/) certification exam. Contains course notes, knowledge checks, summaries, and practice questions covering all five exam domains.

## Exam Overview

| Detail | Info |
|---|---|
| Duration | 100 minutes |
| Cost | $140 USD |
| Format | Proctored |
| Retake | 24 hours after first attempt |
| Languages | English, Chinese (Simplified), Korean, Japanese, French, Spanish, German, Portuguese (Brazil), Chinese (Traditional), Italian |

Schedule through [Pearson VUE](https://learn.microsoft.com/en-us/credentials/certifications/schedule-through-pearson-vue?examUid=exam.AZ-104).

## Exam Domains

| Domain | Weight |
|---|---|
| Manage Azure identities and governance | 20–25% |
| Deploy and manage Azure compute resources | 20–25% |
| Implement and manage storage | 15–20% |
| Implement and manage virtual networking | 15–20% |
| Monitor and maintain Azure resources | 10–15% |

## Repository Structure

```
├── course-materials/
│   ├── 1-administrator-prerequisites/
│   │   ├── Intro to Azure Cloud Shell
│   │   └── ARM templates with VS Code
│   ├── 2-manage-identities-governance/
│   │   ├── Microsoft Entra ID
│   │   ├── Create & manage identities
│   │   ├── Core architectural components
│   │   ├── Sovereignty & policy initiatives
│   │   ├── RBAC
│   │   └── Self-service password reset
│   ├── 3-manage-virtual-networks/
│   │   ├── Virtual networks & subnets
│   │   ├── Network security groups
│   │   ├── Azure DNS
│   │   ├── VNet peering
│   │   ├── Network traffic routing
│   │   ├── Azure Load Balancer
│   │   ├── Azure Application Gateway
│   │   └── Azure Network Watcher
│   ├── 4-manage-storage/
│   │   ├── Storage accounts
│   │   ├── Blob storage
│   │   ├── Storage security
│   │   └── Azure Files & File Sync
│   ├── 5-manage-compute-resources/
│   │   ├── Azure Virtual Machines
│   │   ├── VM availability
│   │   ├── App Service plans
│   │   ├── Azure App Services
│   │   └── Azure Container Instances
│   └── 6-monitor-backup-resources/
│       ├── Azure Backup
│       ├── Protect VMs with Azure Backup
│       └── VM monitoring & diagnostics
├── html_review/
│   ├── Module quizzes & reviews (1–6)
│   └── Practice assessment
├── objectives.md          # Full exam objective breakdown
├── overview.md            # Exam logistics & scheduling
├── question-bank.md       # Practice questions with explanations
└── index.html
```

## Key Files

- **`objectives.md`** — Complete exam objectives with sub-topics. The authoritative reference for coverage.
- **`overview.md`** — Exam logistics: duration, pricing, retake policy, and scheduling.
- **`question-bank.md`** — Practice questions with correct answers and explanations.
- **`html_review/`** — Interactive HTML quizzes and review pages for each module.

## Prerequisites

Familiarity with the following is recommended before taking the exam:

- Operating systems, networking, servers, and virtualization
- PowerShell and Azure CLI
- Azure Portal and Azure Resource Manager templates / Bicep
- Microsoft Entra ID

## License

[MIT](LICENSE)
