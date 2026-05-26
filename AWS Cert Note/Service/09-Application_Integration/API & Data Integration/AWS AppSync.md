---
type: aws-service
service_name: "AWS AppSync"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["AppSync", "GraphQL API"]
tags: [aws, sap-c02, application-integration, graphql]
created: 2026-05-26
updated: 2026-05-26
---

# AWS AppSync

> [!summary] 한 줄 요약
> GraphQL API와 real-time subscription을 제공해 웹/모바일 앱이 여러 데이터 소스를 단일 API로 조회·변경·구독하게 하는 관리형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | GraphQL, 모바일/웹 데이터 집계, real-time subscription, offline sync, resolver |
| 핵심 의사결정 | 클라이언트가 GraphQL로 여러 데이터 소스를 집계하고 실시간 업데이트를 받아야 하면 AppSync |
| 대표 키워드 | GraphQL, resolver, subscription, real-time, DynamoDB, Lambda, offline clients |
| 자주 비교되는 서비스 | [[Amazon API Gateway]], [[Amazon Eventbridge]], [[Amazon Appflow]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: GraphQL schema와 resolver를 통해 DynamoDB, Lambda, OpenSearch, HTTP 등 데이터 소스를 연결하는 관리형 API 서비스.
- **왜 쓰는가?**: 클라이언트가 필요한 데이터만 요청하고, subscriptions로 실시간 업데이트를 받는다.
- **핵심 제약**: REST/HTTP/WebSocket API front door는 API Gateway가 더 일반적이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| GraphQL schema | API 타입/쿼리/변경 정의 | 모바일/웹 데이터 모델 |
| Resolvers | 데이터 소스 연결 로직 | DynamoDB/Lambda/OpenSearch 통합 |
| Subscriptions | 실시간 push 업데이트 | 채팅/협업/상태 업데이트 |
| Authorization | IAM/Cognito/OIDC/API key/Lambda | 클라이언트 보안 |
| Caching | 응답 캐시 | latency/비용 개선 |

## 3. API / 데이터 통합 맵

![[attachments/aws/aws-api-data-integration-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| GraphQL API와 실시간 구독 | AppSync | API Gateway는 GraphQL 특화 resolver 관리가 아님 |
| REST/HTTP API | API Gateway | AppSync를 REST gateway로 오해 금지 |
| SaaS 데이터 이동 | AppFlow | AppSync는 SaaS ETL 서비스가 아님 |
| 이벤트 라우팅 | EventBridge | AppSync는 client data API 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> AppSync는 GraphQL/real-time data API에 강하다. 단순 REST API는 API Gateway가 더 직접적이다.

- Resolver가 데이터 소스 접근 경계이므로 권한과 오류 처리를 설계한다.
- 모바일 앱에서 offline/real-time 요구가 나오면 AppSync가 단서다.
- DynamoDB single-table 설계와 함께 출제될 수 있다.

## 6. 암기 문장

- GraphQL + real-time subscription은 AppSync다.
- REST/HTTP/WebSocket front door는 API Gateway와 구분한다.

## 참고 링크

- [What is AWS AppSync?](https://docs.aws.amazon.com/appsync/latest/devguide/what-is-appsync.html)
- [AWS AppSync features](https://docs.aws.amazon.com/appsync/latest/devguide/aws-appsync-real-time-data.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
