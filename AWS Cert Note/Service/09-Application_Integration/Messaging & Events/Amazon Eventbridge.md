---
type: aws-service
service_name: "Amazon EventBridge"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["EventBridge", "CloudWatch Events"]
tags: [aws, sap-c02, application-integration, events]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon EventBridge

> [!summary] 한 줄 요약
> AWS 서비스, SaaS, custom application 이벤트를 event bus에서 패턴 기반으로 라우팅하는 서버리스 이벤트 버스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 이벤트 기반 아키텍처, rule pattern matching, SaaS 통합, cross-account event bus, Scheduler/Pipes |
| 핵심 의사결정 | 이벤트를 source/detail/type 기준으로 여러 target에 라우팅하고 SaaS/AWS 서비스와 연결해야 하면 EventBridge |
| 대표 키워드 | event bus, rule, event pattern, schema registry, Pipes, Scheduler, archive/replay |
| 자주 비교되는 서비스 | [[Amazon SNS]], [[Amazon SQS]], [[AWS Step Functions]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 이벤트를 bus에 수집하고 rule이 event pattern을 평가해 Lambda, Step Functions, SQS, SNS 등 target으로 전달한다.
- **왜 쓰는가?**: 서비스 간 결합도를 낮추고 SaaS/AWS/custom 이벤트를 표준 방식으로 라우팅한다.
- **핵심 제약**: 장기 상태/순차 워크플로우는 Step Functions, 작업 큐 backpressure는 SQS와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Event bus | 이벤트 수집/라우팅 경계 | default/custom/partner bus |
| Rules | 이벤트 패턴 매칭 후 target 호출 | event-driven routing |
| Cross-account events | 계정 간 이벤트 전달 | 멀티계정 통합 |
| Archive/Replay | 이벤트 보관과 재처리 | 장애 복구/테스트 |
| Pipes | source와 target 연결·필터·보강 | SQS/Kinesis/DynamoDB Streams 통합 |
| Scheduler | 일정 기반 호출 | cron/event schedule 대체 |

## 3. 선택 맵

![[attachments/aws/aws-application-integration-selection-map.png]]

## 4. 이벤트 기반 예시

![[attachments/aws/aws-event-driven-serverless-order-flow.png]]

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 이벤트 패턴 기반 라우팅 | EventBridge | SNS는 topic fanout 중심 |
| 장기 상태 워크플로우 | Step Functions | EventBridge rule은 상태 머신이 아님 |
| 작업 큐/버퍼링 | SQS | EventBridge는 consumer backpressure 흡수용 queue가 아님 |
| SaaS 이벤트 통합 | EventBridge | API Gateway는 client API front door |

## 6. 헷갈리는 포인트

> [!warning] 주의
> EventBridge는 이벤트 라우터다. 여러 단계의 상태, 보상 트랜잭션, 재시도 분기 관리는 Step Functions가 더 적합하다.

- 이벤트는 작고 독립적인 fact로 설계한다.
- cross-account event bus 정책을 통해 중앙 이벤트 허브 패턴을 만들 수 있다.
- archive/replay는 장애 후 재처리나 신규 consumer 테스트에 유용하다.

## 7. 암기 문장

- 이벤트를 조건에 따라 여러 AWS/SaaS target으로 라우팅하면 EventBridge다.
- EventBridge는 라우팅, Step Functions는 orchestration, SQS는 queue다.

## 참고 링크

- [What is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge event buses](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-bus.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
