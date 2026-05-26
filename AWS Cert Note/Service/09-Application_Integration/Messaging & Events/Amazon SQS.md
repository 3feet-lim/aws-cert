---
type: aws-service
service_name: "Amazon SQS"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["SQS", "Simple Queue Service", "SQS FIFO"]
tags: [aws, sap-c02, application-integration, queue]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon SQS

> [!summary] 한 줄 요약
> 생산자와 소비자 사이에 메시지를 큐로 버퍼링해 비동기 처리, backpressure 흡수, 장애 격리를 제공하는 관리형 queue 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 느슨한 결합, 비동기 처리, 버퍼링, 재시도, DLQ, FIFO ordering |
| 핵심 의사결정 | 처리 속도가 다른 컴포넌트 사이에 작업 큐/버퍼가 필요하면 SQS |
| 대표 키워드 | queue, pull, visibility timeout, DLQ, standard, FIFO, at-least-once |
| 자주 비교되는 서비스 | [[Amazon SNS]], [[Amazon Eventbridge]], [[Amazon MQ]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 메시지를 큐에 저장하고 consumer가 poll/pull해서 처리하는 완전관리형 메시지 큐.
- **왜 쓰는가?**: 요청 급증을 버퍼링하고 consumer 장애/지연이 upstream에 전파되지 않게 한다.
- **핵심 제약**: pub-sub fanout은 SNS/EventBridge, 복잡한 워크플로우 상태 관리는 Step Functions와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Standard queue | 높은 처리량, at-least-once, best-effort ordering | 대부분 비동기 작업 큐 |
| FIFO queue | 순서 보장과 exactly-once processing 지원 | 순서/중복 제어 요구 |
| Visibility timeout | 처리 중 메시지 재노출 지연 | 중복 처리/재시도 설계 핵심 |
| Dead-letter queue | 실패 메시지 격리 | 장애 분석과 poison message 처리 |
| Long polling | 빈 응답 감소 | 비용/효율 개선 |

## 3. 선택 맵

![[attachments/aws/aws-application-integration-selection-map.png]]

## 4. 이벤트 기반 예시

![[attachments/aws/aws-event-driven-serverless-order-flow.png]]

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| consumer가 pull하는 작업 큐 | SQS | SNS는 구독자에게 push/fanout |
| 여러 구독자 알림 | SNS | SQS 하나만으로 fanout 구성 복잡 |
| 이벤트 패턴 기반 라우팅 | EventBridge | SQS는 라우팅 규칙 엔진이 아님 |
| 기존 JMS/AMQP broker 호환 | Amazon MQ | SQS는 AWS native queue API |

## 6. 헷갈리는 포인트

> [!warning] 주의
> SQS는 메시지 큐다. 메시지를 받는 consumer가 처리할 때까지 버퍼링하지만 워크플로우 상태 머신은 아니다.

- visibility timeout이 너무 짧으면 중복 처리가 늘고, 너무 길면 재시도가 늦어진다.
- Standard queue는 중복 가능성을 고려해 idempotent consumer를 설계한다.
- DLQ는 실패를 숨기는 곳이 아니라 운영자가 분석할 격리 공간이다.

## 7. 암기 문장

- 버퍼링, pull, 작업 큐, DLQ가 나오면 SQS다.
- Fanout은 SNS, event routing은 EventBridge, orchestration은 Step Functions다.

## 참고 링크

- [What is Amazon SQS?](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [Amazon SQS visibility timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
