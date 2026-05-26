---
type: aws-service
service_name: "Amazon API Gateway"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["API Gateway", "REST API", "HTTP API", "WebSocket API"]
tags: [aws, sap-c02, application-integration, api]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon API Gateway

> [!summary] 한 줄 요약
> REST, HTTP, WebSocket API의 front door로 인증, throttling, 로깅, WAF, backend 통합을 제공하는 완전관리형 API 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 서버리스 API, API front door, auth/throttling, private integration, WebSocket, edge/regional endpoint |
| 핵심 의사결정 | 클라이언트가 호출할 HTTP/REST/WebSocket API를 안전하게 노출하고 Lambda/VPC/AWS 서비스와 연결해야 하면 API Gateway |
| 대표 키워드 | REST API, HTTP API, WebSocket, throttling, usage plan, Lambda authorizer, VPC Link |
| 자주 비교되는 서비스 | [[AWS AppSync]], [[Amazon Appflow]], [[Elastic Load Balancer (ELB)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: API 요청을 받아 인증·권한·제한·변환·로깅 후 backend로 전달하는 managed API front door.
- **왜 쓰는가?**: Lambda 기반 서버리스 API, private ALB/NLB 연계, WebSocket 실시간 API를 빠르게 구성한다.
- **핵심 제약**: GraphQL 데이터 집계/real-time subscription은 AppSync, SaaS 데이터 이동은 AppFlow와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| REST/HTTP API | HTTP API 노출 | 서버리스/마이크로서비스 front door |
| WebSocket API | 양방향 연결 | 실시간 앱 API |
| Authorizers | IAM/Cognito/Lambda authorizer | 인증/권한 통제 |
| Throttling/Usage plans | 호출 제한과 API key | 남용 방지/고객별 제한 |
| VPC Link | private ALB/NLB 통합 | 프라이빗 backend 노출 |
| Logging/metrics | CloudWatch/X-Ray 연동 | 운영 가시성 |

## 3. API / 데이터 통합 맵

![[attachments/aws/aws-api-data-integration-map.png]]

## 4. 이벤트 기반 예시

![[attachments/aws/aws-event-driven-serverless-order-flow.png]]

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| REST/HTTP/WebSocket API front door | API Gateway | AppFlow는 API gateway가 아님 |
| GraphQL + real-time subscriptions | AppSync | REST API만 필요하면 API Gateway가 단순 |
| SaaS 데이터 정기 이동 | AppFlow | API Gateway는 데이터 동기화 서비스가 아님 |
| L7 load balancing | ALB | API 관리/usage plan/auth 기능 요구면 API Gateway |

## 6. 헷갈리는 포인트

> [!warning] 주의
> API Gateway는 “사용자/API traffic front door”다. 이벤트 내부 라우팅은 EventBridge, 워크플로우 orchestration은 Step Functions다.

- HTTP API는 단순/저비용, REST API는 고급 API 관리 기능이 더 풍부하다.
- Private integration은 VPC Link와 private ALB/NLB 패턴을 기억한다.
- Lambda authorizer/Cognito/IAM 중 인증 모델을 문제 요구에 맞춘다.

## 7. 암기 문장

- REST/HTTP/WebSocket API 입구는 API Gateway다.
- GraphQL은 AppSync, SaaS 데이터 이동은 AppFlow다.

## 참고 링크

- [What is Amazon API Gateway?](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [Choosing between HTTP APIs and REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
