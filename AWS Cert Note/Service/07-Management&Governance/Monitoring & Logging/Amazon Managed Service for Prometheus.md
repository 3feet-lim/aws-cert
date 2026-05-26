---
type: aws-service
service_name: "Amazon Managed Service for Prometheus"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["AMP", "Managed Prometheus", "Amazon Managed Service for Prometheus"]
tags: [aws, sap-c02, prometheus, observability]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Managed Service for Prometheus

> [!summary] 한 줄 요약
> Prometheus 호환 지표를 서버 운영 없이 수집·저장·쿼리하는 관리형 Prometheus 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | Kubernetes/container observability, Prometheus 호환성, 고가용성 metrics 저장 |
| 핵심 의사결정 | EKS/ECS 등에서 Prometheus 지표를 관리형으로 저장·쿼리해야 하면 AMP |
| 대표 키워드 | Prometheus-compatible, remote write, PromQL, workspace, EKS metrics |
| 자주 비교되는 서비스 | [[Amazon Managed Grafana]], [[Amazon CloudWatch]], [[Amazon EKS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 오픈소스 Prometheus와 호환되는 관리형 metrics 저장/쿼리 서비스.
- **왜 쓰는가?**: Prometheus 서버의 확장성/가용성/운영 부담을 줄이고 컨테이너 지표를 장기적으로 다룬다.
- **핵심 제약**: 시각화는 Managed Grafana, AWS 리소스 기본 지표/알람은 CloudWatch와 비교한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Workspace | metrics 저장 격리 단위 | 팀/환경 분리 |
| Remote write | Prometheus agent가 지표 전송 | Kubernetes/EKS 패턴 |
| PromQL | Prometheus 쿼리 언어 | 기존 대시보드/알람 호환 |
| Managed scale/HA | 서버 운영 감소 | 운영 부담 감소 |
| Grafana integration | 대시보드 시각화 | AMP + AMG 조합 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| Prometheus 호환 metrics 저장 | AMP | Grafana는 저장소가 아니라 시각화 |
| AWS 리소스 기본 metrics/alarms | CloudWatch | AMP는 Prometheus 생태계 중심 |
| 통합 대시보드 | Managed Grafana | AMP 단독으로 사용자 대시보드 요구 충족 부족 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> AMP는 Prometheus metrics 백엔드다. 로그 저장은 CloudWatch Logs, API 감사는 CloudTrail이다.

- EKS 환경에서 Prometheus agent/collector와 remote write 구성을 떠올린다.
- 시각화는 Managed Grafana와 함께 설계하는 경우가 많다.
- CloudWatch Container Insights와의 역할 차이를 문제 요구사항으로 구분한다.

## 6. 암기 문장

- Prometheus 호환 metrics를 관리형으로 저장/쿼리하면 AMP다.
- AMP는 저장/쿼리, Managed Grafana는 시각화다.

## 참고 링크

- [What is Amazon Managed Service for Prometheus?](https://docs.aws.amazon.com/prometheus/latest/userguide/what-is-Amazon-Managed-Service-Prometheus.html)
- [Amazon Managed Service for Prometheus concepts](https://docs.aws.amazon.com/prometheus/latest/userguide/AMP-concepts.html)
