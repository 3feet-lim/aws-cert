---
name: aws-sap-service-notes
description: Create or revise Korean AWS service concept notes for SAP-C02 study from this repository's Templates/AWS Service Template.md and existing Service/ examples. Use when asked to generate AWS service notes, concept summaries, exam-focused service pages, or Obsidian study notes; invoke aws-exam-diagram-style-system for any needed architecture/concept PNG diagrams.
---

# AWS SAP Service Notes

## Purpose

Create SAP-C02-focused AWS service concept notes under `Service/` by using `Templates/AWS Service Template.md` and nearby existing notes as the source structure. The template is a **flexible checklist**, not a rigid form.

The note should help answer exam questions: **when to choose the service, what tradeoffs matter, what similar services are distractors, and which architecture constraints change the answer.**

## Required companion skill for images

When a note needs a new or revised image, use the project skill `aws-exam-diagram-style-system`.

- Load `.codex/skills/aws-exam-diagram-style-system/SKILL.md` before creating the image prompt.
- Produce a PNG suitable for Obsidian embedding.
- Save images under `attachments/aws/`.
- Link images with Obsidian syntax: `![[attachments/aws/{{service-slug}}-architecture.png]]`, `![[attachments/aws/{{service-slug}}-flow.png]]`, or `![[attachments/aws/{{service-slug}}-comparison.png]]`.
- Do not create `.drawio` files by default. The desired look is draw.io-like, but the artifact should be PNG.

## Workflow

1. Read `Templates/AWS Service Template.md`.
2. Read 1-3 nearby completed notes in the same `Service/<category>/` folder when available to match tone, heading depth, frontmatter, and link style.
3. Identify the service's SAP-C02 role:
   - networking foundation
   - security/governance control
   - compute/runtime platform
   - storage/database/data platform
   - integration/messaging/orchestration
   - migration/modernization tool
   - observability/operations tool
   - cost/optimization tool
   - edge/global service
4. Build the note around exam decisions, not product documentation.
5. Keep required sections minimal:
   - 한 줄 요약
   - SAP-C02 시험 포커스
   - 핵심 개념
   - 주요 기능과 시험 포인트
   - 비교/선택 기준 or service-specific decision section
   - 헷갈리는 포인트 or 오답 함정
   - 암기 문장
   - 참고 링크
6. Add optional sections only when they improve exam understanding.
7. Prefer concise tables and decision rules over long product descriptions.
8. Verify important or version-sensitive claims against AWS official docs.

## File and metadata conventions

- Place the note in the appropriate `Service/<category>/` folder.
- Preserve the repository's numbering/category convention when present, for example `01-Network/1-6 Amazon Route 53.md`.
- Use Korean-first prose while keeping official AWS service names and natural exam terms in English.
- Use YAML frontmatter compatible with `Templates/AWS Service Template.md`:
  - `type: aws-service`
  - `service_name`
  - `category`
  - `exam: SAP-C02`
  - `exam_domains`
  - `status`
  - `priority`
  - `aliases`
  - `tags`
  - `created` / `updated`
- Use the current local date for `created` and `updated` unless revising an existing note; then preserve `created` and update `updated`.
- Use `[[Service Name]]` wiki links for related services.

## Section selection guide

### Usually useful for most services

- SAP-C02 시험 포커스
- 핵심 개념
- 주요 기능과 시험 포인트
- 다른 서비스와 비교 / 선택 기준
- 헷갈리는 포인트 / 오답 함정
- SAP-C02 시나리오 패턴 when the service is often a scenario answer
- 암기 문장
- 참고 링크

### Use only when meaningful

- `언제 사용하는가`: useful for substitutable services such as ECS vs EKS, SQS vs SNS/EventBridge, EFS vs FSx, Direct Connect vs VPN.
- `언제 사용하지 않는가`: useful when common distractors exist. Omit or merge into comparison for broad foundation services.
- `아키텍처 / 동작 흐름`: use when a diagram clarifies traffic flow, trust boundary, HA/DR, integration, deployment, policy evaluation, lifecycle, or migration path.
- `보안 / 거버넌스`: keep for identity, network, encryption, audit, compliance, or org-control services.
- `가용성 / 확장성 / 복원력`: keep for stateful, multi-AZ, DR, backup, replication, routing, storage, database, or workload-continuity topics.
- `비용 / 운영 포인트`: keep when pricing or operational burden changes architecture choices. Otherwise one short bullet is enough.

## Diagram decision rules

Create a diagram only when visual memory or spatial relationships help more than a Markdown table.

Use `aws-exam-diagram-style-system` to create:

- architecture flow diagrams for VPC, hybrid, edge, app, migration, or data path services
- policy/evaluation flows for IAM-like services
- lifecycle/state diagrams for storage, deployment, migration, and backup services
- decision trees for choosing between similar services
- comparison visuals when exam distractors are hard to remember

Skip diagrams when the same concept is clearer as a concise table.

## Service-specific adaptation examples

- **Amazon VPC**: Replace `언제 사용하는가/사용하지 않는가` with `설계 시 고려사항`, `연결 옵션`, `보안 경계`, `라우팅/엔드포인트`, and `하이브리드/멀티계정 패턴`.
- **AWS IAM**: Emphasize policy evaluation, identity vs resource policies, cross-account access, federation, permission boundaries, SCP interaction, and least privilege. A policy-evaluation flow image can help.
- **Amazon S3**: Keep storage class comparison, lifecycle, replication, encryption, access control, consistency, event integration, and DR/cost tradeoffs.
- **Amazon ECS/EKS**: Keep `언제 사용하는가/사용하지 않는가`, runtime model comparison, networking, scaling, deployment, operations burden, and cost.
- **AWS DMS / Migration Hub**: Focus on source/target constraints, migration patterns, downtime, replication, validation, and cutover.
- **CloudWatch / CloudTrail / Config**: Focus on observability vs audit vs compliance differences and exam distractors.
- **SNS / SQS / EventBridge / Step Functions**: Focus on event fanout, buffering, routing, orchestration, retry/DLQ behavior, ordering, and loose coupling.

## Style

- Write in Korean for study explanations.
- Keep service notes practical for exam review, not exhaustive product manuals.
- Prefer short tables, bullets, and scenario patterns.
- Delete placeholders that do not fit the service instead of filling them awkwardly.
- Mark uncertain details clearly or verify them from official AWS docs.
- Avoid over-generating sections; the final note should feel curated.

## Completion check

Before finishing a service note, confirm:

- The note explains why this service is the answer in an SAP-C02 scenario.
- At least one common wrong-answer trap or comparison is included.
- Irrelevant template sections were omitted or renamed.
- Official AWS links are included for high-risk or detail-heavy claims.
- Any needed PNG is present in `attachments/aws/`, linked with Obsidian syntax, and follows `aws-exam-diagram-style-system`.
