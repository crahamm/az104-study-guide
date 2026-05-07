# AZ-104 Study Materials

This repository contains study notes, module reviews, and generated practice material for the Microsoft AZ-104: Microsoft Azure Administrator certification.

The materials are organized around the major AZ-104 exam domains and are intended for certification review, not as a replacement for the official Microsoft Learn content, product documentation, or hands-on Azure practice.

## What's Included

- Lesson notes organized by exam area and module.
- Concise `review.md` files for completed modules.
- Knowledge check answer summaries where available.
- `objectives.md`, which maps the current AZ-104 objective areas and domain weightings.
- Local workflows for generating flashcards and quizzes from the study material.

## Repository Structure

```text
.
|-- objectives.md
|-- 1-administrator-prerequisites/
|   |-- 1-intro-to-azure-cloud-shell/
|   `-- 2-create-azure-resource-manager-template-vs-code/
|-- 2-manage-identities-governance/
|   |-- 1-understand-azure-active-directory/
|   |-- 2-create-configure-manage-identities/
|   |-- 3-describe-core-architectural-components-of-azure/
|   |-- 4-sovereignty-policy-initiatives/
|   |-- 5-secure-azure-resources-with-rbac/
|   `-- 6-allow-users-reset-their-password/
|-- 3-manage-virtual-networks/
|-- 4-manage-storage/
`-- 5-manage-compute-resources/
```

Module folders contain numbered Markdown lesson files. When a module has been reviewed, it also includes a `review.md` file with exam-focused notes.

## Exam Objective Areas

The root `objectives.md` file summarizes the official AZ-104 objective areas:

| Domain | Weighting |
| --- | --- |
| Manage Azure identities and governance | 20-25% |
| Implement and manage storage | 15-20% |
| Deploy and manage Azure compute resources | 20-25% |
| Implement and manage virtual networking | 15-20% |
| Monitor and maintain Azure resources | 10-15% |

Use `objectives.md` as the main reference when deciding which topics to prioritize.

## Current Review Coverage

Completed module reviews currently include:

- Azure Cloud Shell
- ARM templates in Visual Studio Code
- Microsoft Entra ID

More folders exist for planned or in-progress coverage across identity, governance, networking, storage, and compute topics.

## How To Use These Notes

1. Start with `objectives.md` to understand the exam domains and weightings.
2. Open a module folder that matches the area you want to study.
3. Read the numbered lesson files for the full note sequence.
4. Use `review.md` for a condensed exam-review pass.
5. Pay special attention to sections such as `Exam Triggers`, command examples, service limits, and decision points.

The review files are designed for quick recall and last-pass certification preparation. For topics that involve configuration or troubleshooting, pair the notes with hands-on practice in the Azure portal, Azure CLI, or Azure PowerShell.

## Generated Study Material

This workspace includes local workflows for creating additional review assets:

- Flashcards and Anki-style cards from module content.
- Practice quizzes with answer explanations.
- Module summaries aligned to the AZ-104 objectives.

Generated material should normally live beside the source lesson files in the same module folder.

## Notes On Source Material

Some lesson notes are copied from or based on Microsoft Learn modules and then reorganized for personal certification study. Review files are written in condensed original wording for exam preparation.

For authoritative and current details, always check:

- The official AZ-104 exam page.
- Microsoft Learn training modules.
- Azure product documentation.

Azure services change over time, so verify product limits, command syntax, portal labels, and licensing details before relying on them in production.

## Contributing

Contributions are welcome if they keep the repository focused on practical AZ-104 preparation.

Good additions include:

- New module notes.
- Concise `review.md` summaries.
- Corrections to outdated Azure details.
- Practice questions with clear explanations.
- Flashcards for high-value exam facts.

When adding study content, keep it concise, exam-focused, and organized by the existing domain/module folder structure.
