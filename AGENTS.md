# AZ-104 Study Workspace

This repository stores study notes and generated review material for the Microsoft Azure Administrator certification.

## Repository Layout

- Content is organized by exam area, then by module.
- Module folders contain numbered Markdown lesson files copied from or based on Microsoft Learn modules.
- Generated study material should live in the same module folder as the source lesson files unless the user asks for a different location.
- `objectives.md` at the repository root contains the Microsoft exam objectives and domain weightings for AZ-104.

## Exam Objectives Reference

Use `objectives.md` when study material should be aligned to the official exam scope, especially when:

- Creating or updating module reviews.
- Generating flashcards or quizzes.
- Identifying which exam domain a module belongs to.
- Prioritizing review notes based on domain weighting.
- Checking whether a topic is likely to be test-relevant.

## Study Review Conventions

When the user asks for a module summary or review:

- Read the module's Markdown lesson files first.
- Consult `objectives.md` when exam-scope alignment would improve the review.
- Create or update `review.md` in that module folder.
- Keep reviews exam-focused and concise.
- Prefer headings such as:
  - Core Idea
  - Key Capabilities
  - How It Works
  - When To Use
  - When Not To Use
  - Exam Triggers
  - Knowledge Check Answers
- Summarize in original wording; do not copy large passages from the source lesson.
- Preserve important numbers, limits, product names, and decision points.

## Local Skills

This workspace includes local skills under `.agents/skills`.

- Use `flashcard-creator` when the user asks for flashcards, Anki cards, cloze cards, memorization aids, or spaced repetition material.
- Use `quiz-maker` when the user asks for practice questions, quizzes, multiple choice questions, true/false questions, or answer explanations.

## Output Style

- Write study files in Markdown.
- Use ASCII unless source material requires otherwise.
- Favor practical certification-review notes over long prose.
- Include command names, Azure service names, limits, and common exam traps in backticks where helpful.

## Verification

After creating or updating a study file:

- Re-read the generated file to catch formatting issues.
- Report the absolute path of the file changed.
