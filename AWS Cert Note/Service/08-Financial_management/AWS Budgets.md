---
type: aws-service
service_name: "AWS Budgets"
category: "Financial Management"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Budgets", "AWS Budget Actions"]
tags: [aws, sap-c02, cost, financial-management, alert]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Budgets

> [!summary] 한 줄 요약
> 비용, 사용량, RI/Savings Plans 활용률·커버리지에 대한 임계치를 설정하고 실제/예측 기준 알림과 일부 자동 액션을 수행하는 예산 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 비용 초과 알림, forecast 기반 사전 경고, budget action, 약정 활용률/커버리지 감시 |
| 핵심 의사결정 | 특정 비용/사용량/약정 지표가 임계치를 넘기 전에 알림 또는 조치를 해야 하면 AWS Budgets |
| 대표 키워드 | budget threshold, actual vs forecast, SNS alert, budget actions, utilization, coverage |
| 자주 비교되는 서비스 | [[AWS Cost Explorer]], [[AWS Cost and Usage Report (CUR)]], [[Savings Plans]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 예산 임계치와 알림 수신자를 설정해 비용/사용량/약정 지표를 관리하는 서비스.
- **왜 쓰는가?**: 비용 초과를 사전에 감지하고 운영팀/재무팀에 알리며, 일부 IAM/SCP/SSM 기반 action을 실행한다.
- **관리형 여부**: 관리형 비용 알림/액션 서비스.
- **리전/글로벌**: Billing 계정 단위이며 Organizations 멀티계정 비용 관리와 함께 사용한다.
- **핵심 제약**: 기본 역할은 알림이다. 모든 리소스를 자동으로 중지하거나 비용을 즉시 차단하는 만능 킬스위치가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Cost budget | 비용 기준 예산 | 월별/프로젝트별 비용 초과 감지 |
| Usage budget | 사용량 기준 예산 | 데이터 전송량, 특정 서비스 사용량 관리 |
| RI/Savings Plans budget | utilization/coverage 감시 | 약정 할인 낭비 또는 부족 감지 |
| Actual/Forecast alerts | 실제 또는 예측 값 기준 알림 | 사전 대응 |
| Budget Actions | IAM/SCP/SSM 등 액션 | 자동화 가능하지만 승인/범위 설계 필요 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-financial-management-cost-flow.png]]

1. 비용/사용량/약정 활용률 기준으로 budget을 만든다.
2. 실제 비용 또는 forecast가 임계치에 도달하면 SNS/email 등으로 알림을 보낸다.
3. 필요 시 Budget Actions로 IAM 정책 적용, SCP 적용, SSM Automation 실행 등을 구성한다.
4. Cost Explorer와 CUR로 원인을 분석하고 리소스/약정 정책을 조정한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 비용/사용량 임계치 알림 | AWS Budgets | Cost Explorer는 분석 중심 |
| 비용 증가 원인 분석 | Cost Explorer | Budgets는 원인 분석 UI가 주목적이 아님 |
| 상세 데이터 웨어하우스 분석 | CUR | Budgets는 집계 임계치 관리 중심 |
| 약정 활용률/커버리지 알림 | Budgets | Savings Plans 자체는 할인 모델 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Budgets는 “임계치 기반 알림/액션” 서비스다. 자동으로 모든 초과 비용을 막아주는 서비스가 아니다.

- forecast alert는 비용이 실제로 초과되기 전에 대응할 수 있게 한다.
- Budget Actions는 권한과 승인 흐름을 잘못 설계하면 운영 장애를 만들 수 있다.
- Tag/Cost Category 기반 budget은 태깅 전략이 전제다.

## 6. 암기 문장

- 비용이 특정 선을 넘으면 알려달라는 요구는 AWS Budgets다.
- 분석은 Cost Explorer, 상세 원천 데이터는 CUR, 임계치 알림은 Budgets다.

## 참고 링크

- [Managing your costs with AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)
- [Configuring AWS Budget actions](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-controls.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
