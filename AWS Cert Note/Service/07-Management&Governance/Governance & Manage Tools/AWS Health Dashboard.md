---
type: aws-service
service_name: "AWS Health Dashboard"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["AWS Health", "Personal Health Dashboard"]
tags: [aws, sap-c02, health, operations]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Health Dashboard

> [!summary] 한 줄 요약
> AWS 서비스 이벤트와 계정에 영향을 주는 예정/진행 중 이슈를 보여주고 EventBridge로 알림 자동화할 수 있는 상태 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 계정 영향 이벤트, 유지보수/서비스 장애 알림, EventBridge 자동 대응 |
| 핵심 의사결정 | AWS 서비스 이벤트가 내 계정/리소스에 미치는 영향을 추적해야 하면 AWS Health Dashboard |
| 대표 키워드 | account-specific events, planned lifecycle events, EventBridge, organizational view |
| 자주 비교되는 서비스 | [[Amazon CloudWatch]], [[AWS Trusted Advisor]], [[Service Quotas]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS 전체 서비스 상태와 내 계정 리소스에 영향을 주는 Health event를 제공한다.
- **왜 쓰는가?**: 유지보수, 성능 저하, 장애, 수명주기 이벤트에 대응한다.
- **핵심 제약**: 내 애플리케이션 metrics 알람은 CloudWatch가 담당한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Account-specific events | 내 리소스 영향 이벤트 | 운영 대응 우선순위 |
| Public service health | AWS 서비스 지역 상태 | 장애 파악 |
| EventBridge integration | 이벤트 기반 알림/자동화 | ChatOps/Incident 자동화 |
| Organizational view | 조직 전체 Health event 보기 | 멀티계정 운영 |
| Planned lifecycle events | 예정된 변경/종료 알림 | 사전 조치 |

## 3. 선택 맵

![[attachments/aws/aws-optimization-advisory-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| AWS 서비스/계정 영향 이벤트 | AWS Health Dashboard | 앱 내부 장애 알람은 CloudWatch |
| 비용/보안 best practice 추천 | Trusted Advisor | Health는 이벤트/상태 중심 |
| 한도 증가 요청 | Service Quotas | Health는 quota 관리 도구가 아님 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Health Dashboard는 AWS 측 서비스/계정 영향 이벤트를 보여준다. 애플리케이션 지표 기반 모니터링과 구분한다.

- EventBridge로 티켓 생성, Slack 알림, Lambda 대응을 자동화할 수 있다.
- Organizations 환경은 organizational view로 중앙 운영한다.
- scheduled change와 issue를 구분해 운영 runbook을 만든다.

## 6. 암기 문장

- AWS 서비스 이벤트가 내 계정에 미치는 영향은 AWS Health Dashboard다.
- 내 앱 성능 알람은 CloudWatch, AWS 측 이벤트는 Health다.

## 참고 링크

- [What is AWS Health?](https://docs.aws.amazon.com/health/latest/ug/what-is-aws-health.html)
- [Monitoring AWS Health events with EventBridge](https://docs.aws.amazon.com/health/latest/ug/cloudwatch-events-health.html)
