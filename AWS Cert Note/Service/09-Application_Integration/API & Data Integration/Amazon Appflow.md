---
type: aws-service
service_name: "Amazon AppFlow"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["AppFlow", "Amazon AppFlow"]
tags: [aws, sap-c02, application-integration, saas-integration]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon AppFlow

> [!summary] 한 줄 요약
> Salesforce, ServiceNow, Slack 같은 SaaS와 AWS 서비스 사이의 데이터 흐름을 코드 없이 안전하게 자동화하는 관리형 SaaS 데이터 통합 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | SaaS 데이터 통합, scheduled/event/on-demand flow, S3/Redshift/Snowflake target, PrivateLink, KMS |
| 핵심 의사결정 | SaaS 애플리케이션 데이터를 S3/Redshift/EventBridge 등 AWS로 정기·이벤트 기반 이동해야 하면 AppFlow |
| 대표 키워드 | SaaS integration, Salesforce, ServiceNow, Slack, flow, connector, PrivateLink |
| 자주 비교되는 서비스 | [[Amazon API Gateway]], [[AWS AppSync]], [[AWS Glue]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: SaaS와 AWS 서비스 간 데이터 전송 flow를 구성하는 관리형 통합 서비스.
- **왜 쓰는가?**: 커스텀 ETL/커넥터 코드를 줄이고 SaaS 데이터를 분석/이벤트 처리/저장소로 이동한다.
- **핵심 제약**: 사용자 API traffic을 처리하는 front door가 아니다. 앱 API는 API Gateway/AppSync와 비교한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Connectors | Salesforce, ServiceNow 등 SaaS 연결 | SaaS 데이터 수집 |
| Flow trigger | on-demand, scheduled, event-based | 자동화 주기 선택 |
| Targets | S3, Redshift, Snowflake, EventBridge 등 | 분석/이벤트 통합 |
| Data mapping/filter | 필드 매핑과 필터 | ETL 전처리 |
| Security | KMS, PrivateLink 지원 | 보안 데이터 이동 |

## 3. API / 데이터 통합 맵

![[attachments/aws/aws-api-data-integration-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| SaaS ↔ AWS 데이터 이동 | AppFlow | API Gateway는 데이터 통합 flow가 아님 |
| REST API 노출 | API Gateway | AppFlow는 client API endpoint가 아님 |
| GraphQL client API | AppSync | AppFlow는 GraphQL API 서비스가 아님 |
| 복잡한 ETL/대용량 변환 | Glue | AppFlow는 SaaS connector 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> AppFlow는 SaaS 데이터 통합 서비스다. 애플리케이션 API를 보호·노출하는 API Gateway와 혼동하지 않는다.

- SaaS 데이터를 S3로 보내 data lake를 만들거나 EventBridge로 SaaS 이벤트를 연계한다.
- PrivateLink 지원 connector는 인터넷 노출을 줄일 수 있다.
- 변환이 복잡하면 Glue/EMR/Step Functions와 조합한다.

## 6. 암기 문장

- SaaS 데이터를 AWS로 코드 없이 흐르게 하면 AppFlow다.
- API front door는 API Gateway, GraphQL은 AppSync, SaaS data flow는 AppFlow다.

## 참고 링크

- [What is Amazon AppFlow?](https://docs.aws.amazon.com/appflow/latest/userguide/what-is-appflow.html)
- [Amazon AppFlow supported source and destination applications](https://docs.aws.amazon.com/appflow/latest/userguide/supported-source-destination-applications.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
