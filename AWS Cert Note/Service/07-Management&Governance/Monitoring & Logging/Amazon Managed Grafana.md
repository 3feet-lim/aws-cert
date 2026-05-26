---
type: aws-service
service_name: "Amazon Managed Grafana"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Managed Grafana", "Grafana"]
tags: [aws, sap-c02, observability, dashboard]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Managed Grafana

> [!summary] 한 줄 요약
> Grafana 워크스페이스를 AWS가 관리해 CloudWatch, Prometheus, OpenSearch 등 여러 데이터 소스를 통합 시각화하는 대시보드 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 멀티소스 관측성 대시보드, Prometheus/CloudWatch 시각화, SSO 기반 접근 |
| 핵심 의사결정 | 여러 관측성 데이터 소스를 한 Grafana 대시보드로 통합해야 하면 Amazon Managed Grafana |
| 대표 키워드 | managed Grafana workspace, dashboards, data sources, SSO, Prometheus |
| 자주 비교되는 서비스 | [[Amazon CloudWatch]], [[Amazon Managed Service for Prometheus]], [[Amazon CloudWatch Logs]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Grafana 서버 운영을 AWS에 맡기는 관리형 시각화 서비스.
- **왜 쓰는가?**: CloudWatch, AMP, OpenSearch, X-Ray 등 다양한 데이터 소스를 통합 대시보드로 본다.
- **핵심 제약**: 지표 저장소 자체가 아니라 주로 시각화/대시보드 계층이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Workspace | 관리형 Grafana 환경 | 서버 운영 부담 감소 |
| Data sources | CloudWatch/AMP/OpenSearch 등 연결 | 멀티소스 대시보드 |
| Authentication | IAM Identity Center/SAML 등 | 기업 접근 통제 |
| Dashboards | 시각화/알림 | 운영 가시성 |
| Plugins | Grafana plugin 생태계 | 기존 Grafana 경험 활용 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| Grafana 기반 통합 대시보드 | Managed Grafana | CloudWatch Dashboard만으로 멀티소스 요구 부족 |
| Prometheus 지표 저장/쿼리 | Managed Service for Prometheus | Grafana는 저장소가 아님 |
| AWS 리소스 metrics/alarms | CloudWatch | Grafana는 시각화 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Managed Grafana는 시각화 계층이다. metrics 수집/저장/알람 원천은 CloudWatch나 Prometheus 같은 데이터 소스다.

- Grafana 운영 부담을 줄이지만 데이터 소스 권한과 네트워크 접근 설계는 필요하다.
- CloudWatch만 쓰는 단순 요구면 CloudWatch Dashboard가 더 간단할 수 있다.
- Kubernetes/Prometheus 환경은 AMP와 함께 출제될 수 있다.

## 6. 암기 문장

- 여러 관측성 데이터 소스를 Grafana로 시각화하면 Amazon Managed Grafana다.
- Prometheus 지표 저장은 AMP, 시각화는 Managed Grafana다.

## 참고 링크

- [What is Amazon Managed Grafana?](https://docs.aws.amazon.com/grafana/latest/userguide/what-is-Amazon-Managed-Service-Grafana.html)
- [Amazon Managed Grafana data sources](https://docs.aws.amazon.com/grafana/latest/userguide/data-sources.html)
