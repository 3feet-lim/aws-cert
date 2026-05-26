---
type: aws-service
service_name: "Service Quotas"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["AWS Service Quotas", "Quotas"]
tags: [aws, sap-c02, quotas, governance]
created: 2026-05-26
updated: 2026-05-26
---

# Service Quotas

> [!summary] 한 줄 요약
> AWS 서비스별 적용 quota를 조회하고, 조정 가능한 quota의 증가 요청과 사용률 모니터링을 관리하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 한도 사전 확인, 대규모 배포 전 quota 증가, Organizations quota template |
| 핵심 의사결정 | 리소스 생성 실패를 방지하기 위해 서비스 한도를 조회/증가 요청해야 하면 Service Quotas |
| 대표 키워드 | applied quota, adjustable, quota increase request, utilization, quota template |
| 자주 비교되는 서비스 | [[AWS Trusted Advisor]], [[AWS Health Dashboard]], [[AWS License Manager]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 계정/리전별 서비스 할당량을 중앙에서 보고 증가 요청을 관리하는 서비스.
- **왜 쓰는가?**: 대규모 마이그레이션/이벤트/확장 전에 EC2, VPC, ALB, Lambda 등의 quota 부족을 예방한다.
- **핵심 제약**: 모든 quota가 조정 가능하지는 않으며 일부는 hard quota다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Applied quota | 현재 적용 한도 | 배포 전 검증 |
| Adjustable quota | 증가 요청 가능 여부 | 용량 사전 확보 |
| Increase request | Support 연계 증가 요청 | 운영 리드타임 |
| Utilization | 사용률 추적 | 한도 임박 알림 |
| Quota template | Organizations 신규 계정 기본 요청 | 멀티계정 표준화 |

## 3. 선택 맵

![[attachments/aws/aws-optimization-advisory-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| AWS 서비스 한도 조회/증가 | Service Quotas | Trusted Advisor의 Service Limits 체크와 역할 구분 |
| 계정 Best Practice 점검 | Trusted Advisor | quota 증가 요청 도구는 Service Quotas |
| 라이선스 사용 제한 | License Manager | AWS service quota와 소프트웨어 라이선스 한도는 다름 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Quota는 리전/계정별로 다를 수 있다. DR 리전과 신규 계정도 사전에 확인해야 한다.

- 대규모 배포, 마이그레이션, 이벤트 트래픽 전 quota 검토가 필수다.
- adjustable 여부와 승인 리드타임을 고려한다.
- CloudWatch alarm으로 quota 사용률을 감시할 수 있다.

## 6. 암기 문장

- “한도 때문에 배포 실패 방지”는 Service Quotas다.
- 권고 체크는 Trusted Advisor, 증가 요청/적용 한도 관리는 Service Quotas다.

## 참고 링크

- [What is Service Quotas?](https://docs.aws.amazon.com/servicequotas/latest/userguide/intro.html)
- [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html)
