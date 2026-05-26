---
type: aws-service
service_name: "AWS Cost Explorer"
category: "Financial Management"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Cost Explorer", "AWS CE"]
tags: [aws, sap-c02, cost, financial-management, analysis]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Cost Explorer

> [!summary] 한 줄 요약
> AWS 비용과 사용량을 서비스, 계정, 태그, 기간별로 시각화하고 추세·예측·약정 할인 추천을 확인하는 비용 분석 도구다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 비용 가시화, 사용량 추세 분석, Forecast, Savings Plans/RI 추천, Organizations 비용 분해 |
| 핵심 의사결정 | “왜 비용이 증가했는지”, “어느 서비스/계정/태그가 비용을 쓰는지” 분석해야 하면 Cost Explorer |
| 대표 키워드 | cost analysis, usage trend, group by service/account/tag, forecast, recommendations |
| 자주 비교되는 서비스 | [[AWS Budgets]], [[AWS Cost and Usage Report (CUR)]], [[Savings Plans]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 비용과 사용량 데이터를 그래프와 필터로 탐색하는 비용 분석 서비스.
- **왜 쓰는가?**: 비용 증가 원인을 찾고, 계정/서비스/태그별 비용 분해와 미래 비용 예측을 확인한다.
- **관리형 여부**: 관리형 콘솔/API 기반 분석 도구.
- **리전/글로벌**: Billing/Cost Management 영역의 계정 단위 기능이며 Organizations payer/management 계정 관점이 중요하다.
- **핵심 제약**: 가장 상세한 원천 데이터가 필요하면 CUR, 임계치 알림은 Budgets가 더 직접적이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Cost and usage analysis | 기간, 서비스, 계정, 태그 기준 분석 | 비용 증가 원인 파악 |
| Group/Filter | Linked account, service, tag, Cost Category 등 | 멀티계정 chargeback/showback |
| Forecast | 과거 사용량 기반 예측 | 예산 초과 사전 감지 |
| Recommendations | RI/Savings Plans 추천 | 약정 할인 최적화 시작점 |
| Reports | 저장된 비용 분석 뷰 | 반복 비용 리뷰 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-financial-management-cost-flow.png]]

1. AWS 서비스 사용량, linked account, cost allocation tag, Cost Categories가 비용 데이터의 분석 축이 된다.
2. Cost Explorer로 서비스/계정/태그별 비용 추세와 forecast를 확인한다.
3. 예산 초과 감시는 Budgets로, 상세 원천 분석은 CUR + S3 + Athena/QuickSight로 확장한다.
4. 안정적인 사용량은 Cost Explorer 추천을 참고해 Savings Plans 약정을 검토한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 비용 추세와 원인 분석 | Cost Explorer | 알림/차단이 핵심이면 Budgets |
| 상세 원천 청구 데이터 분석 | CUR | Cost Explorer는 집계/시각화 중심 |
| 예산 초과 알림 | AWS Budgets | Cost Explorer forecast만으로 운영 알림 부족 |
| 약정 할인 추천 | Cost Explorer + Savings Plans | 추천을 자동 구매로 오해 금지 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Cost Explorer는 분석 도구다. 비용 초과 알림/액션은 Budgets, 가장 상세한 데이터 파이프라인은 CUR가 더 적합하다.

- Cost allocation tags를 활성화해야 태그 기반 비용 분석이 의미 있다.
- Organizations에서는 payer/management 계정과 member account의 비용 가시성 차이를 고려한다.
- 예측은 과거 패턴 기반이므로 대규모 출시/마이그레이션 같은 이벤트는 별도 고려한다.

## 6. 암기 문장

- 비용이 “왜/어디서” 늘었는지 보는 것은 Cost Explorer다.
- 알림은 Budgets, 원천 상세 데이터는 CUR, 할인 약정은 Savings Plans와 연결한다.

## 참고 링크

- [Analyzing your costs with Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
- [AWS Cost Explorer API](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-api.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
