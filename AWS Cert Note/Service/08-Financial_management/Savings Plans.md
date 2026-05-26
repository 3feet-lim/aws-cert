---
type: aws-service
service_name: "Savings Plans"
category: "Financial Management"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["AWS Savings Plans", "Compute Savings Plans", "EC2 Instance Savings Plans", "Database Savings Plans"]
tags: [aws, sap-c02, cost, financial-management, savings-plans]
created: 2026-05-26
updated: 2026-05-26
---

# Savings Plans

> [!summary] 한 줄 요약
> 1년 또는 3년 동안 시간당 사용 금액을 약정해 온디맨드 대비 할인을 받는 유연한 사용량 기반 할인 모델이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 약정 할인, 안정적 사용량, RI와 비교, coverage/utilization, 비용 최적화 |
| 핵심 의사결정 | 장기간 안정적인 컴퓨팅/DB/ML 사용량이 있고 용량 예약보다 할인 최적화가 목적이면 Savings Plans |
| 대표 키워드 | 1-year/3-year commitment, $/hour, coverage, utilization, Compute Savings Plans, EC2 Instance Savings Plans |
| 자주 비교되는 서비스 | [[AWS Cost Explorer]], [[AWS Budgets]], [[AWS Cost and Usage Report (CUR)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 특정 사용량에 대해 시간당 금액을 약정하고 적용 가능한 사용량에 자동 할인받는 가격 모델.
- **왜 쓰는가?**: 안정적 베이스라인 워크로드 비용을 줄이면서 인스턴스 변경이나 서비스 변경에 대한 유연성을 확보한다.
- **관리형 여부**: 비용/청구 할인 모델이며 Cost Explorer로 추천·coverage·utilization을 관리한다.
- **리전/글로벌**: 플랜 유형에 따라 Region, instance family, 서비스 유연성이 다르다.
- **핵심 제약**: 용량 예약이 아니며, 약정을 사용하지 않아도 약정 비용은 청구된다.

## 2. Savings Plans 유형과 시험 포인트

| 유형 | 할인/유연성 | 선택 단서 | 오답 함정 |
|---|---|---|---|
| Compute Savings Plans | 가장 유연. EC2, Fargate, Lambda 등에 적용 | Region/family/size 변경 가능성이 큰 워크로드 | 할인율은 EC2 Instance SP보다 낮을 수 있음 |
| EC2 Instance Savings Plans | 특정 Region + instance family 기준 | 특정 패밀리 사용이 안정적인 EC2 워크로드 | Region/family를 바꾸면 유연성 제한 |
| Database Savings Plans | 지원되는 AWS database 사용량 약정 | DB 사용량이 안정적이고 관리형 DB 비용 절감 필요 | DB 성능/용량 최적화 자체는 별도 |
| SageMaker AI Savings Plans | SageMaker AI 인스턴스 사용량 약정 | ML 학습/추론 사용량이 안정적 | 일반 EC2/Lambda 할인과 구분 |

## 3. 선택 맵

![[attachments/aws/aws-savings-plans-decision-map.png]]

1. Cost Explorer에서 최근 사용량과 추천 약정 규모를 확인한다.
2. 워크로드가 얼마나 안정적인지, 서비스/리전/인스턴스 family가 바뀔 가능성이 있는지 평가한다.
3. 가변성이 크면 낮은 약정 또는 Compute Savings Plans처럼 유연한 모델을 우선 검토한다.
4. 구매 후에는 coverage와 utilization을 Budgets/Cost Explorer로 지속 감시한다.

## 4. Financial Management 흐름

![[attachments/aws/aws-financial-management-cost-flow.png]]

- Cost Explorer: 추천, coverage, utilization, forecast 확인.
- Budgets: Savings Plans utilization/coverage 임계치 알림.
- CUR: 약정 적용 전후 비용을 상세 라인 아이템으로 분석.

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 안정적 사용량에 할인 적용 | Savings Plans | Auto Scaling 자체나 용량 예약이 아님 |
| 미래 비용/약정 추천 확인 | Cost Explorer | 추천을 무조건 구매하면 미사용 약정 위험 |
| 약정 활용률 알림 | Budgets | Savings Plans는 알림 도구가 아님 |
| 리소스별 비용 상세 분석 | CUR | Savings Plans는 데이터 분석 도구가 아님 |
| 용량 확보 | Capacity Reservation 또는 RI 일부 옵션 | Savings Plans는 capacity reservation이 아님 |

## 6. 헷갈리는 포인트

> [!warning] 주의
> Savings Plans는 “사용량 약정 할인”이지 “용량 예약”이 아니다. 미사용 약정도 비용이 발생한다.

- All Upfront/Partial Upfront/No Upfront는 결제 방식이며, 약정 리스크가 사라지는 것은 아니다.
- coverage는 전체 사용량 중 할인이 적용된 비율, utilization은 구매한 약정이 얼마나 쓰였는지다.
- 불확실한 워크로드는 약정을 작게 시작하고 Cost Explorer 추천을 주기적으로 검토한다.
- RI와 비교할 때 할인율, 유연성, 용량 예약 필요 여부를 분리해서 판단한다.

## 7. SAP-C02 시나리오 패턴

- **문제 상황**: EC2/Fargate/Lambda 사용량이 1년 이상 안정적이고 비용 절감이 필요하다.
- **요구사항**: 인스턴스 family와 Region 변경 가능성이 있다.
- **정답 단서**: Compute Savings Plans.
- **오답 함정**: Reserved Instance를 무조건 선택하거나 Savings Plans를 용량 예약으로 설명하는 선택지.

## 8. 암기 문장

- 안정적인 사용량에 시간당 금액을 약정해 할인받으면 Savings Plans다.
- 유연성이 중요하면 Compute Savings Plans, 특정 EC2 패밀리가 고정이면 EC2 Instance Savings Plans다.
- 용량 예약이 필요하면 Savings Plans만으로는 부족하다.

## 참고 링크

- [What are Savings Plans?](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html)
- [Understanding Savings Plans types](https://docs.aws.amazon.com/savingsplans/latest/userguide/plan-types.html)
- [Monitoring your Savings Plans](https://docs.aws.amazon.com/savingsplans/latest/userguide/monitoring-sp.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
