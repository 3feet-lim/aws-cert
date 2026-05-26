---
type: aws-service
service_name: "AWS Step Functions"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Step Functions", "SFN", "State Machine"]
tags: [aws, sap-c02, application-integration, workflow]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Step Functions

> [!summary] 한 줄 요약
> 여러 AWS 서비스와 애플리케이션 단계를 state machine으로 오케스트레이션하고 재시도, 분기, 오류 처리를 관리하는 서버리스 워크플로우 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 워크플로우 오케스트레이션, 상태 관리, 재시도/보상, Standard vs Express, human approval |
| 핵심 의사결정 | 여러 단계와 분기/재시도/상태가 있는 비즈니스 프로세스를 안정적으로 실행해야 하면 Step Functions |
| 대표 키워드 | state machine, workflow, task, retry, catch, parallel, map, Standard, Express |
| 자주 비교되는 서비스 | [[Amazon Eventbridge]], [[Amazon SQS]], [[Amazon SNS]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: JSON/ASL 기반 state machine으로 Lambda, ECS, Batch, Glue, API Gateway, SNS/SQS 등 작업을 조합한다.
- **왜 쓰는가?**: 복잡한 비즈니스 흐름을 코드 안에 숨기지 않고 시각적·선언적으로 관리한다.
- **핵심 제약**: 단순 이벤트 라우팅은 EventBridge, 단순 작업 큐는 SQS가 더 간단하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Standard workflow | 장기 실행, 정확한 실행 이력 | 결제/주문/승인 같은 중요 프로세스 |
| Express workflow | 고처리량·짧은 실행 | 이벤트/스트리밍성 워크로드 |
| Retry/Catch | 오류 재시도와 예외 분기 | 복원력 설계 |
| Parallel/Map | 병렬 처리와 반복 | 대량 작업 orchestration |
| Service integrations | Lambda 없이 AWS 서비스 호출 | 코드 감소와 운영 단순화 |
| Human approval | callback/task token 패턴 | 승인 워크플로우 |

## 3. 선택 맵

![[attachments/aws/aws-application-integration-selection-map.png]]

## 4. 이벤트 기반 예시

![[attachments/aws/aws-event-driven-serverless-order-flow.png]]

## 5. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 단계/분기/재시도 워크플로우 | Step Functions | EventBridge rule만으로 상태 관리 불가 |
| producer-consumer 큐 | SQS | Step Functions는 queue 서비스가 아님 |
| 단순 fanout 알림 | SNS | Step Functions는 orchestration용 |
| 초고속 짧은 워크플로우 | Express | 감사/장기 실행 중요하면 Standard |

## 6. 헷갈리는 포인트

> [!warning] 주의
> Step Functions는 orchestration 서비스다. 서비스 간 이벤트를 느슨하게 흘려보내는 것만 필요하면 EventBridge가 더 단순하다.

- Standard는 정확한 이력과 장기 실행, Express는 대량 짧은 실행에 적합하다.
- Lambda 안에 복잡한 상태/재시도 코드를 넣는 선택지는 Step Functions로 단순화할 수 있다.
- timeout, retry, catch, idempotency를 함께 설계한다.

## 7. 암기 문장

- 단계가 있고 상태와 재시도가 있으면 Step Functions다.
- EventBridge는 이벤트 라우팅, Step Functions는 비즈니스 프로세스 오케스트레이션이다.

## 참고 링크

- [What is AWS Step Functions?](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [Standard vs Express workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
