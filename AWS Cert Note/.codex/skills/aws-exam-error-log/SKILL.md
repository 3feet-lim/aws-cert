---
name: aws-exam-error-log
description: Create Korean AWS SAP-C02 practice-question error notes from a provided question, choices, correct answer, explanation, or user's wrong answer. Use when Codex is asked to make an 오답노트, AWS exam error log, wrong-answer note, or review note under error_log/; link mentioned AWS services to existing Service/ notes, and update or create missing service-note content by following the project skill aws-sap-service-notes.
---

# AWS Exam Error Log

## Purpose

Create Obsidian-friendly Korean 오답노트 entries for AWS SAP-C02 practice questions under `error_log/`, then keep related `Service/` notes complete enough to explain why the correct answer wins and why distractors are wrong.

## Required companion skill

When adding or revising AWS service notes, load and follow `.codex/skills/aws-sap-service-notes/SKILL.md`.

Use the companion skill when:

- a service in the question has no matching note under `Service/`
- the existing service note lacks a concept required to explain the question
- a distractor comparison is missing from the service note
- official-doc verification is needed for a detail-heavy or version-sensitive claim

## Inputs to extract

From the user's prompt, identify:

- original question text and scenario constraints
- answer choices, if present
- correct answer and explanation, if provided
- user's selected wrong answer, if provided
- AWS services, features, limits, architecture constraints, and distractor services
- SAP-C02 decision axis: security, networking, resilience, migration, cost, operations, data, integration, or organization complexity

If the user omits some fields, still create a useful note from available information. Mark unknown fields as `미제공` only when the absence matters.

## Workflow

1. Inspect repository conventions:
   - Read `error_log/initial note.md` if it has content.
   - Read 1-3 existing `error_log/*.md` entries if present.
   - Search `Service/` for matching service notes by file name, H1 title, `service_name`, and `aliases`.
2. Build the service-link map:
   - Prefer existing note titles as wiki links, for example `[[Amazon Route 53]]`.
   - Use aliases only when the service note frontmatter defines them.
   - Link every major service or feature that maps cleanly to a service note.
3. Check service-note coverage:
   - Open each relevant service note.
   - Confirm it covers the correct-answer concept and the distractor distinction.
   - If content is missing, update the existing note or create a new one using `aws-sap-service-notes`.
4. Create one Markdown file under `error_log/`:
   - Use a concise filename: `YYYY-MM-DD {{service-or-topic}} {{short-korean-topic}}.md`.
   - Use the current local date.
   - Keep names filesystem-safe; avoid `/`, `:`, excessive punctuation, and overly long titles.
5. Write the error note using `references/error-log-format.md`.
6. Verify links and files:
   - Confirm all wiki-linked service notes exist or are intentionally alias-based.
   - Confirm added service-note content is exam-focused and not duplicated.
   - Confirm the error note states the correct answer, wrong-answer trap, and a reusable decision rule.

## Service-note update policy

When the question reveals missing service-note content:

- Add the smallest useful exam-focused section, row, or bullet.
- Prefer updating existing sections such as `주요 기능과 시험 포인트`, `비교 / 선택 기준`, `헷갈리는 포인트`, or `SAP-C02 시나리오 패턴`.
- Preserve existing frontmatter and update only `updated` to the current local date.
- Include official AWS documentation links for new high-risk claims.
- Do not create diagrams unless the companion skill determines a diagram is genuinely useful.

When creating a missing service note:

- Follow `aws-sap-service-notes` exactly.
- Put the note in the best matching `Service/<category>/` folder.
- Use Korean-first SAP-C02 exam style and Obsidian wiki links.

## Error-note style

- Write in Korean, keeping official AWS names and natural technical terms in English.
- Focus on the reasoning gap: why the selected answer is wrong, why the correct answer satisfies the constraints, and what keyword should trigger the right service next time.
- Prefer compact tables and bullets over long prose.
- Separate evidence from inference when the prompt lacks the official explanation.
- Do not copy long copyrighted question-bank text. Summarize the scenario if the prompt appears to be from a commercial practice exam; quote only short necessary fragments.

## Completion check

Before finishing:

- A new `error_log/*.md` file exists.
- The note links relevant AWS services with Obsidian wiki links.
- Any missing service-note concept from the question was added or a new service note was created through `aws-sap-service-notes` guidance.
- The note includes correct answer, wrong-answer trap, key decision rule, and review checklist.
- Important claims are verified from official AWS docs when needed.
