---
type: aws-service
service_name: "Amazon CloudWatch"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["CloudWatch"]
tags: [aws, sap-c02, monitoring, observability]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon CloudWatch

> [!summary] 한 줄 요약
> AWS 리소스와 애플리케이션의 metrics, alarms, dashboards, 이벤트 기반 자동화를 제공하는 운영 모니터링 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 운영 가시성, 성능/가용성 알람, 자동 대응, 대시보드 |
| 핵심 의사결정 | 리소스 상태·성능 지표를 실시간 모니터링하고 임계치 기반 알림/자동화를 해야 하면 CloudWatch |
| 대표 키워드 | metrics, alarms, dashboards, anomaly detection, EventBridge, agent |
| 자주 비교되는 서비스 | [[AWS CloudTrail]], [[Amazon CloudWatch Logs]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 리소스와 앱의 운영 지표를 수집·시각화·알람화하는 서비스.
- **왜 쓰는가?**: 장애 징후를 빠르게 감지하고 SNS/Lambda/EventBridge로 자동 대응한다.
- **핵심 제약**: API 감사는 CloudTrail, 구성 변경 컴플라이언스는 Config와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Metrics | CPU, Network, ALB, Lambda 등 지표 | 성능/가용성 모니터링 |
| Alarms | 임계치/복합 알람 | 자동 복구, SNS 알림 |
| Dashboards | 지표/로그 시각화 | NOC/운영 대시보드 |
| Agent | EC2/온프레미스 OS 지표와 로그 수집 | 메모리/디스크는 agent 필요 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 성능 지표와 알람 | CloudWatch | 누가 API를 호출했는지는 CloudTrail |
| 로그 저장·검색 | CloudWatch Logs | Metrics 서비스 자체와 구분 |
| 구성 변경 규정 준수 | AWS Config | CloudWatch alarm만으로 규정 준수 이력 부족 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> CloudWatch는 “운영 상태와 성능” 중심이다. 계정 활동 감사 요구사항은 CloudTrail을 먼저 본다.

- EC2 기본 지표에는 메모리/디스크 사용률이 없다. CloudWatch Agent를 배포한다.
- EventBridge와 연계해 알람 이후 조치를 자동화할 수 있다.
- 로그 분석은 CloudWatch Logs Insights와 연결해 생각한다.

## 6. 암기 문장

- 성능/운영 지표는 CloudWatch, API 감사는 CloudTrail, 구성 준수는 Config다.
- 알람이 나오면 SNS/Lambda/EventBridge로 대응한다.

## 참고 링크

- [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [AWS Decision Guide: CloudTrail or CloudWatch](https://docs.aws.amazon.com/pdfs/decision-guides/latest/cloudtrail-or-cloudwatch/cloudtrail-or-cloudwatch.pdf)
