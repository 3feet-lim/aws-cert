---
type: aws-service
service_name: "Amazon CloudWatch Logs"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["CloudWatch Logs", "Logs Insights"]
tags: [aws, sap-c02, logs, observability]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon CloudWatch Logs

> [!summary] 한 줄 요약
> EC2, 애플리케이션, CloudTrail 등 다양한 로그를 중앙 저장·검색·분석하는 로그 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 중앙 로그 수집, 로그 검색, 보존 기간, metric filter, 감사 데이터 분석 |
| 핵심 의사결정 | 여러 시스템 로그를 한 곳에 저장하고 검색/필터/보존/알람화해야 하면 CloudWatch Logs |
| 대표 키워드 | log group, log stream, retention, Logs Insights, metric filter, subscription filter |
| 자주 비교되는 서비스 | [[Amazon CloudWatch]], [[AWS CloudTrail]], [[Amazon Managed Grafana]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 로그 이벤트를 log group/log stream 단위로 수집·저장·조회하는 서비스.
- **왜 쓰는가?**: 분산된 앱/시스템 로그를 중앙화하고 장애 분석과 보안 조사에 사용한다.
- **핵심 제약**: 장기 아카이브/대규모 SQL 분석은 S3 + Athena 조합도 고려한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Log groups/streams | 로그 보관 단위 | 앱/환경별 분리 |
| Retention | 보존 기간 설정 | 비용과 규정 준수 균형 |
| Logs Insights | 쿼리 기반 분석 | 장애 원인/패턴 검색 |
| Metric filter | 로그 패턴을 지표로 변환 | 에러율 알람 |
| Subscription filter | Lambda/Kinesis/OpenSearch 전송 | 실시간 처리/외부 SIEM |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 앱/시스템 로그 중앙화 | CloudWatch Logs | 단순 metrics 알람이면 CloudWatch |
| API 감사 로그 | CloudTrail → Logs/S3 | CloudWatch Logs 자체가 API 기록 생성자는 아님 |
| 시각화 대시보드 | Grafana/CloudWatch Dashboard | 로그 저장소와 시각화 도구 구분 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> CloudWatch Logs는 로그 저장·검색 서비스다. “누가 API를 호출했는지 기록”은 CloudTrail 이벤트가 원천이다.

- retention을 무기한으로 두면 비용이 증가한다.
- metric filter로 로그 기반 알람을 만들 수 있다.
- Logs Insights는 운영 분석에 강하지만 장기 데이터 레이크 분석은 S3/Athena와 비교한다.

## 6. 암기 문장

- 로그는 CloudWatch Logs, 지표와 알람은 CloudWatch, API 감사 원천은 CloudTrail이다.
- 로그에서 지표를 뽑을 때 metric filter를 떠올린다.

## 참고 링크

- [What is Amazon CloudWatch Logs?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
- [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
