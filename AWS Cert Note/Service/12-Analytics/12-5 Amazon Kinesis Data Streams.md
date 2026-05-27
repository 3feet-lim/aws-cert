---
type: aws-service
service_name: "Amazon Kinesis Data Streams"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["KDS", "Kinesis Streams"]
tags: [aws, sap-c02, streaming, real-time, analytics]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Kinesis Data Streams

> [!summary] 한 줄 요약
> 실시간 스트리밍 데이터를 수집하고 여러 consumer가 직접 처리하게 하는 스트림 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | real-time ingest, shard/throughput, replay, multiple consumers |
| 대표 키워드 | KDS, Kinesis Streams, streaming, real-time, analytics |
| 자주 비교되는 서비스 | [[Amazon Data Firehose]], [[Amazon MSK]], [[Amazon SQS]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Shard/온디맨드 용량으로 레코드를 보관하고 consumer가 읽는다.
- **왜 쓰는가?**: 짧은 지연의 실시간 처리와 재처리가 필요할 때 쓴다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 전송 대상 적재만 필요하면 Firehose가 더 단순하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Shard/On-demand | 처리량 단위/자동 용량 | 성능 설계 |
| Retention/replay | 일정 기간 재처리 | 장애 복구 |
| Enhanced fan-out | consumer별 전용 처리량 | 다중 소비자 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon Kinesis Data Streams`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Data Firehose]] | 전송/적재 관리형 | S3/OpenSearch/Redshift 등으로 적재 | 직접 consumer 처리에는 부적합 |
| [[Amazon MSK]] | Kafka 호환 | Kafka 생태계 필요 | AWS 네이티브 단순 스트림은 KDS |
| [[Amazon SQS]] | 메시지 큐 | 작업 분리/버퍼링 | 스트림 분석/재처리 모델과 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Kinesis Data Streams는 `실시간 스트림 버퍼` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 전송 대상 적재만 필요하면 Firehose가 더 단순하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Kinesis Data Streams`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| real-time ingest, shard/throughput, replay, multiple consumers | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Kinesis Data Streams]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `실시간 스트림 버퍼`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 실시간 스트림을 직접 처리하고 재처리해야 하면 Kinesis Data Streams다.
- 목적지로 그냥 배달하면 Firehose, Kafka 호환이면 MSK다.

## 참고 링크

- [Amazon Kinesis Data Streams 공식 문서](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
