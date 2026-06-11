# AGENTS.md

This file provides guidance to AI coding agents when working with content in this repository.

## Purpose

This is a personal study guide for the **AZ-104: Microsoft Azure Administrator** certification exam. It contains structured markdown notes and course materials covering the five exam domains.

## Repository Structure

All content lives under `course-materials/`, organized by module number and topic:

- `1-administrator-prerequisites/` — Azure Cloud Shell, ARM templates with VS Code
- `2-manage-identities-governance/` — Microsoft Entra ID, RBAC, Azure Policy, SSPR
- `3-manage-virtual-networks/` — VNets, NSGs, DNS, peering, routing, load balancers, Network Watcher
- `4-manage-storage/` — Storage accounts, Blob storage, storage security, Azure Files
- `5-manage-compute-resources/` — VMs, availability, App Service, Container Instances
- `6-monitor-backup-resources/` — Azure Backup, VM protection, monitoring/diagnostics

Each submodule follows a consistent structure: numbered markdown files (`1-introduction.md`, `2-...`, ..., `knowledge-check.md`, `summary.md`).

Top-level files:
- `objectives.md` — Full exam objective breakdown with weightings (the authoritative reference for coverage gaps)
- `overview.md` — Exam logistics (duration, pricing, retake policy)

## Exam Domains and Weights

| Domain | Weight |
|--------|--------|
| Manage Azure identities and governance | 20–25% |
| Deploy and manage Azure compute resources | 20–25% |
| Implement and manage storage | 15–20% |
| Implement and manage virtual networking | 15–20% |
| Monitor and maintain Azure resources | 10–15% |

## Content Conventions

- Files are plain markdown with no build step or tooling.
- Submodule directories use kebab-case prefixed with a number (e.g., `3-host-domain-azure-dns`).
- Knowledge checks and summaries are the last two files in each submodule.
- The `objectives.md` file is the source of truth for what needs to be covered — cross-reference it when adding or reviewing content.
