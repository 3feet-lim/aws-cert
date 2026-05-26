---
type: aws-service
service_name: "AWS Cost and Usage Report (CUR)"
category: "Financial Management"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["AWS CUR", "Cost and Usage Reports", "Data Exports"]
tags: [aws, sap-c02, cost, financial-management, cur]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Cost and Usage Report (CUR)

> [!summary] 한 줄 요약
> AWS 비용과 사용량에 대한 가장 상세한 원천 데이터를 S3로 내보내 Athena, QuickSight, 데이터 웨어하우스에서 정교하게 분석하게 해주는 청구 데이터 리포트다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 상세 비용 데이터, chargeback/showback, S3 + Athena/QuickSight 분석, 태그/리소스 단위 비용 |
| 핵심 의사결정 | Cost Explorer보다 더 세밀한 원천 청구 데이터를 쿼리/BI/데이터 레이크에서 분석해야 하면 CUR |
| 대표 키워드 | detailed billing data, S3 delivery, Athena integration, resource IDs, cost allocation tags |
| 자주 비교되는 서비스 | [[AWS Cost Explorer]], [[AWS Budgets]], [[Savings Plans]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 비용과 사용량 라인 아이템을 정기적으로 S3에 전달하는 상세 리포트.
- **왜 쓰는가?**: 부서/제품/계정/태그/리소스 단위 비용 배분, 커스텀 리포팅, 데이터 웨어하우스 분석에 사용한다.
- **관리형 여부**: AWS가 리포트를 생성해 S3로 전달하고, 분석은 Athena/QuickSight/Glue/외부 도구로 구성한다.
- **리전/글로벌**: Billing 데이터는 계정/조직 단위이며 리포트 저장 S3 버킷과 보안 정책을 설계한다.
- **핵심 제약**: 실시간 알림 도구가 아니다. 예산 초과 알림은 Budgets를 사용한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Line item detail | 가장 상세한 비용/사용량 데이터 | 정교한 비용 배분 |
| S3 delivery | 리포트를 S3에 저장 | 데이터 레이크/보안 설계 |
| Athena integration | SQL 쿼리 분석 | 비용 분석 자동화 |
| Cost allocation tags | 태그별 비용 분해 | chargeback/showback |
| Resource IDs | 리소스 단위 비용 추적 | 비용 원인 식별 |
| QuickSight/BI | 대시보드와 리포트 | 재무/운영 보고 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-financial-management-cost-flow.png]]

1. Organizations/linked accounts에서 발생한 비용과 사용량이 CUR 라인 아이템으로 생성된다.
2. CUR는 S3 버킷으로 전달되고, Glue/Athena/QuickSight 또는 데이터 웨어하우스에서 분석한다.
3. 비용 배분 기준은 cost allocation tags, Cost Categories, 계정/OU 구조로 정교화한다.
4. 분석 결과를 기반으로 Budgets 임계치, Savings Plans 약정, 리소스 최적화를 조정한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 상세 원천 비용 데이터 쿼리 | CUR | Cost Explorer는 집계 분석 UI/API 중심 |
| 빠른 비용 추세 확인 | Cost Explorer | CUR는 데이터 파이프라인 구성 필요 |
| 예산 임계치 알림 | Budgets | CUR는 알림 서비스가 아님 |
| BI/데이터 웨어하우스 연동 | CUR + S3/Athena/QuickSight | 콘솔 UI만 필요하면 과한 구성 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> CUR는 “가장 상세한 원천 데이터”다. 사람이 빠르게 그래프로 보는 것은 Cost Explorer, 임계치 알림은 Budgets가 더 적합하다.

- S3 버킷 권한, 암호화, 수명주기 정책, Athena 비용을 함께 설계한다.
- 리소스 ID와 태그를 포함해야 정확한 chargeback/showback이 가능하다.
- 리포트 데이터는 비용 분석용이므로 실시간 운영 모니터링과 구분한다.

## 6. 암기 문장

- 정교한 비용 데이터 레이크 분석은 CUR + S3 + Athena다.
- Cost Explorer는 보기 쉬운 분석, CUR는 원천 상세 데이터다.

## 참고 링크

- [What are AWS Cost and Usage Reports?](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html)
- [Creating Cost and Usage Reports](https://docs.aws.amazon.com/cur/latest/userguide/cur-create.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
