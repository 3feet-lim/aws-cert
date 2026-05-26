---
type: aws-service
service_name: "AWS CloudTrail"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["CloudTrail", "CloudTrail Lake", "Organization trail"]
tags: [aws, sap-c02, audit, governance]
created: 2026-05-26
updated: 2026-05-26
---

# AWS CloudTrail

> [!summary] 한 줄 요약
> AWS 계정에서 사용자, 역할, 서비스가 수행한 API 활동을 이벤트로 기록해 감사·거버넌스·보안 분석에 사용하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 계정 활동 감사, 규정 준수, 보안 조사, 조직 trail, data events |
| 핵심 의사결정 | 누가 언제 어떤 AWS API를 호출했는지 추적해야 하면 CloudTrail |
| 대표 키워드 | API activity, event history, trail, management events, data events, CloudTrail Lake |
| 자주 비교되는 서비스 | [[Amazon CloudWatch]], [[Amazon CloudWatch Logs]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Console, CLI, SDK, AWS 서비스가 수행한 계정 활동을 이벤트로 기록한다.
- **왜 쓰는가?**: 보안 사고 조사, 변경 추적, 감사 증적, Organizations 전체 trail을 구성한다.
- **핵심 제약**: 성능 지표 모니터링 서비스가 아니다. 운영 metrics는 CloudWatch다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Event history | 최근 management event 조회 | 기본 감사 시작점 |
| Trail | S3/CloudWatch Logs/EventBridge로 이벤트 전달 | 장기 보관과 조직 감사 |
| Organization trail | 멀티계정 이벤트 중앙 수집 | Control Tower/Organizations 환경 |
| Data events | S3 object, Lambda invoke 등 데이터 평면 | 고비용 가능, 필요한 리소스만 선택 |
| CloudTrail Lake | 이벤트 저장·쿼리 | 감사 분석과 보존 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| API 활동 감사 | CloudTrail | CloudWatch는 성능/운영 모니터링 |
| 리소스 구성 상태 평가 | AWS Config | CloudTrail은 변경 행위 기록 중심 |
| 로그 저장/검색 | CloudWatch Logs 또는 S3/Athena | CloudTrail은 이벤트 생성 원천 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> CloudTrail은 “계정 API 감사”가 핵심이다. 리소스가 현재 규정을 만족하는지 평가하는 서비스는 Config다.

- management events와 data events의 비용/범위를 구분한다.
- 멀티계정은 organization trail로 중앙화한다.
- 보안 분석은 S3 Object Lock, KMS, CloudWatch Logs, Athena와 함께 설계할 수 있다.

## 6. 암기 문장

- “누가, 언제, 무엇을 했나”는 CloudTrail이다.
- “현재 리소스 구성이 규정에 맞나”는 Config다.

## 참고 링크

- [What Is AWS CloudTrail?](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
- [CloudTrail concepts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-concepts.html)
