---
type: aws-service
service_name: "Amazon MQ"
category: "Application Integration"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["MQ", "ActiveMQ", "RabbitMQ"]
tags: [aws, sap-c02, application-integration, broker]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon MQ

> [!summary] 한 줄 요약
> Apache ActiveMQ 또는 RabbitMQ 메시지 브로커를 AWS가 관리해 기존 JMS/AMQP/MQTT/OpenWire/STOMP 애플리케이션을 최소 변경으로 이전하게 해주는 관리형 broker 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 레거시 메시지 브로커 마이그레이션, 프로토콜 호환성, ActiveMQ/RabbitMQ, 코드 변경 최소화 |
| 핵심 의사결정 | 기존 broker 프로토콜과 클라이언트 코드를 유지해야 하면 Amazon MQ |
| 대표 키워드 | managed broker, ActiveMQ, RabbitMQ, JMS, AMQP, MQTT, OpenWire, STOMP |
| 자주 비교되는 서비스 | [[Amazon SQS]], [[Amazon SNS]], [[Amazon Eventbridge]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 오픈소스 메시지 브로커 엔진을 AWS 관리형으로 제공하는 서비스.
- **왜 쓰는가?**: 기존 ActiveMQ/RabbitMQ 기반 앱을 AWS native messaging API로 재작성하지 않고 이전한다.
- **핵심 제약**: 신규 cloud-native 설계는 SQS/SNS/EventBridge가 더 운영 단순할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| ActiveMQ broker | JMS/OpenWire/STOMP/MQTT 등 | Java enterprise migration |
| RabbitMQ broker | AMQP 중심 | RabbitMQ 앱 이전 |
| Managed operations | 패치/백업/모니터링 지원 | 운영 부담 감소 |
| Multi-AZ deployment | standby/cluster 옵션 | 고가용성 broker |
| VPC networking | private broker 구성 | 보안 경계 설계 |

## 3. 선택 맵

![[attachments/aws/aws-application-integration-selection-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| ActiveMQ/RabbitMQ 호환성 유지 | Amazon MQ | SQS/SNS는 프로토콜 호환 broker가 아님 |
| 신규 서버리스 queue | SQS | Amazon MQ는 broker 운영 개념 유지 |
| pub-sub fanout 알림 | SNS | MQ는 레거시 broker 호환성 중심 |
| 이벤트 버스 라우팅 | EventBridge | MQ는 SaaS/AWS event bus 통합이 주목적이 아님 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Amazon MQ는 “기존 broker 호환성”이 핵심 단서다. 신규 AWS native 비동기 설계는 SQS/SNS/EventBridge가 더 자주 정답이다.

- 프로토콜과 클라이언트 라이브러리 호환성이 요구될 때 선택한다.
- broker는 queue/topic, connection, throughput, storage 운영 한계를 설계해야 한다.
- VPC 내부 접근, 보안 그룹, 암호화, CloudWatch 모니터링을 함께 고려한다.

## 6. 암기 문장

- ActiveMQ/RabbitMQ를 거의 그대로 AWS로 가져오면 Amazon MQ다.
- 새로 만드는 서버리스 메시징은 SQS/SNS/EventBridge부터 검토한다.

## 참고 링크

- [What is Amazon MQ?](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/welcome.html)
- [Amazon MQ broker engines](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/amazon-mq-broker-engines.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
