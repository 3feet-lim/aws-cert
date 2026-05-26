---
type: aws-service
service_name: "Amazon SNS"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["SNS", "Simple Notification Service"]
tags: [aws, sap-c02, application-integration, pubsub]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon SNS

> [!summary] 한 줄 요약
> 하나의 메시지를 topic에 게시하면 여러 구독자에게 push 방식으로 fanout하는 완전관리형 pub-sub 알림 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | pub-sub, fanout, 모바일/이메일/SMS/HTTP 알림, SQS fanout, filter policy |
| 핵심 의사결정 | 한 이벤트를 여러 시스템이나 사용자에게 동시에 전달해야 하면 SNS |
| 대표 키워드 | topic, publish-subscribe, fanout, subscription, filter policy, SMS/email |
| 자주 비교되는 서비스 | [[Amazon SQS]], [[Amazon Eventbridge]], [[Amazon MQ]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: publisher가 topic에 메시지를 게시하고 topic 구독자에게 push 전달하는 pub-sub 서비스.
- **왜 쓰는가?**: Lambda, SQS, HTTP/S, email, SMS 등 여러 대상에 이벤트를 동시에 전달한다.
- **핵심 제약**: 장기 버퍼링/consumer pull은 SQS, 패턴 기반 이벤트 라우팅은 EventBridge가 더 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Topic | 메시지 발행 대상 | fanout 중심 단위 |
| Subscription | SQS/Lambda/HTTP/S/email/SMS 등 | 다양한 endpoint 알림 |
| Filter policy | 속성 기반 구독 필터 | 불필요한 처리 감소 |
| SNS FIFO | 순서와 중복 제거 | FIFO SQS와 조합 가능 |
| Message delivery retry | endpoint별 재시도 | 장애 시 전달 신뢰성 |

## 3. 선택 맵

![[attachments/aws/aws-application-integration-selection-map.png]]

## 4. 이벤트 기반 예시

![[attachments/aws/aws-event-driven-serverless-order-flow.png]]

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 여러 구독자에게 동시 알림 | SNS | SQS는 단일 queue 소비 패턴 |
| producer-consumer 버퍼링 | SQS | SNS는 영구 작업 큐가 아님 |
| SaaS/AWS 이벤트 라우팅 | EventBridge | SNS는 복잡한 event bus 라우팅보다 단순 fanout |
| 모바일 push/SMS/email | SNS | EventBridge는 사용자 알림 채널이 아님 |

## 6. 헷갈리는 포인트

> [!warning] 주의
> SNS는 “알림 fanout” 서비스다. 메시지를 consumer가 처리할 때까지 안정적으로 작업 큐에 쌓아두려면 SQS와 함께 설계한다.

- SNS → SQS fanout은 각 consumer별 독립 버퍼를 제공한다.
- filter policy로 구독자별 필요한 메시지만 받을 수 있다.
- FIFO 요구사항이 있으면 SNS FIFO + SQS FIFO 조합을 검토한다.

## 7. 암기 문장

- 한 메시지를 여러 구독자에게 push하면 SNS다.
- 버퍼링은 SQS, fanout은 SNS, 이벤트 라우팅은 EventBridge다.

## 참고 링크

- [What is Amazon SNS?](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
- [Amazon SNS message filtering](https://docs.aws.amazon.com/sns/latest/dg/sns-message-filtering.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
