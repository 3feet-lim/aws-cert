---
name: aws-sap-service-notes
description: Use when creating or revising AWS service concept notes for SAP-C02 exam prep. Apply the repository service template flexibly: choose, merge, rename, or omit sections based on each service's exam-relevant characteristics instead of forcing every heading.
---

# AWS SAP Service Notes

## Purpose

Create SAP-C02-focused AWS service notes under `Service/` by using `Templates/AWS Service Template.md` as a flexible checklist, not a rigid form.

The output should help answer exam questions: **when to choose the service, what tradeoffs matter, what similar services are distractors, and which architecture constraints change the answer.**

## Core rule

Do not force every template section into every service note.

For each service, first classify the service type, then select only the sections that improve exam understanding. Rename or merge headings when that makes the note clearer.

## Workflow

1. Read `Templates/AWS Service Template.md` and the target service file.
2. Identify the service's SAP-C02 role:
   - networking foundation
   - security/governance control
   - compute/runtime platform
   - storage/database/data platform
   - integration/messaging/orchestration
   - migration/modernization tool
   - observability/operations tool
   - cost/optimization tool
   - edge/global service
3. Build the note around exam decisions, not product documentation.
4. Keep required sections minimal:
   - 한 줄 요약
   - SAP-C02 시험 포커스
   - 핵심 개념
   - 주요 기능과 시험 포인트
   - 비교/선택 기준
   - 헷갈리는 포인트 또는 오답 함정
   - 암기 문장
   - 참고 링크
5. Add optional sections only when relevant.
6. Prefer concise tables and decision rules over long descriptions.
7. Verify important claims against AWS official docs when the service behavior could be version-sensitive or easy to misstate.

## Section selection guide

### Usually useful for most services

- SAP-C02 시험 포커스
- 핵심 개념
- 주요 기능과 시험 포인트
- 다른 서비스와 비교
- 헷갈리는 포인트
- 암기 문장

### Use only when meaningful

- `언제 사용하는가`: useful for substitutable services such as ECS vs EKS, SQS vs SNS/EventBridge, EFS vs FSx, Direct Connect vs VPN. For foundational services like VPC, convert it to `설계 시 고려사항` or omit.
- `언제 사용하지 않는가`: useful when common distractors exist. Omit or merge into comparison for broad foundation services.
- `아키텍처 그림`: use only when a diagram clarifies traffic flow, trust boundary, HA/DR, or integration. Do not require images for every service. When adding one, keep a draw.io source file and export a PNG for Obsidian embedding.
- `동작 흐름`: use for event-driven, pipeline, auth, migration, deployment, or data-flow services. Omit for static resource concepts.
- `DR 전략`: use for stateful, regional, backup, migration, database, storage, or workload continuity topics. Omit for services where DR is not an exam decision.
- `비용 포인트`: keep when pricing changes architecture choices. Otherwise one short bullet is enough.

## Diagram convention

Use draw.io / diagrams.net as the source format for service diagrams.

- Source file: `attachments/aws/{{service-slug}}-architecture.drawio`
- Embedded export: `attachments/aws/{{service-slug}}-architecture.png`
- Link from notes with Obsidian image syntax: `![[attachments/aws/{{service-slug}}-architecture.png]]`
- Keep diagrams SAP-C02-oriented, not product-architecture exhaustive.
- Prefer AWS official icon shapes when available.
- Use left-to-right flow unless a hub-and-spoke or layered architecture is clearer.
- Use light backgrounds and minimal colors:
  - blue: AWS managed service/control plane
  - green: private VPC/subnet/data path
  - orange: internet/edge/external user
  - red: risk, failure, or exam trap callout
- Include only labels that help exam recall: HA boundary, Region/AZ/account boundary, trust boundary, routing path, replication path, or migration flow.
- Do not create a diagram just to satisfy the template.

## Service-specific adaptation examples

- **Amazon VPC**: Replace `언제 사용하는가/사용하지 않는가` with `설계 시 고려사항`, `연결 옵션`, `보안 경계`, `라우팅/엔드포인트`, and `하이브리드/멀티계정 패턴`.
- **AWS IAM**: Emphasize policy evaluation, identity vs resource policies, cross-account access, federation, permission boundaries, SCP interaction, and least privilege. Architecture diagram is optional.
- **Amazon S3**: Keep storage class comparison, lifecycle, replication, encryption, access control, consistency, event integration, and DR/cost tradeoffs.
- **Amazon ECS/EKS**: Keep `언제 사용하는가/사용하지 않는가`, runtime model comparison, networking, scaling, deployment, operations burden, and cost.
- **AWS DMS / Migration Hub**: Focus on source/target constraints, migration patterns, downtime, replication, validation, and cutover.
- **CloudWatch / CloudTrail / Config**: Focus on observability vs audit vs compliance differences and exam distractors.

## Style

- Korean notes are preferred.
- Keep service notes practical for exam review, not exhaustive product manuals.
- Use `[[Service Name]]` wiki links for related AWS services.
- If a template placeholder does not fit the service, delete it rather than filling it awkwardly.
- Mark uncertain details clearly or verify from official AWS docs.

## Completion check

Before finishing a service note, confirm:

- The note explains why this service is the answer in an SAP-C02 scenario.
- At least one common wrong-answer trap or comparison is included.
- Irrelevant template sections were omitted or renamed.
- Official AWS links are included for high-risk or detail-heavy claims.
