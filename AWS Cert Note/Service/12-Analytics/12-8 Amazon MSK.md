---
type: aws-service
service_name: "Amazon MSK"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["MSK", "Managed Streaming for Apache Kafka"]
tags: [aws, sap-c02, kafka, streaming]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon MSK

> [!summary] 한 줄 요약
> Apache Kafka 호환 스트리밍 클러스터를 AWS 관리형으로 운영한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | Kafka compatibility, existing Kafka apps, cluster/serverless choice |
| 대표 키워드 | MSK, Managed Streaming for Apache Kafka, kafka, streaming |
| 자주 비교되는 서비스 | [[Amazon Kinesis Data Streams]], [[Amazon Data Firehose]], [[Amazon SQS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Kafka broker 운영을 AWS가 관리하고 기존 Kafka client/protocol을 사용한다.
- **왜 쓰는가?**: Kafka 생태계·호환성이 요구될 때 선택한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: AWS 네이티브 단순 스트림은 Kinesis가 더 단순할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Kafka compatibility | 기존 Kafka API/클라이언트 | 마이그레이션/호환성 |
| MSK Serverless | 용량 관리 감소 | 운영 단순화 |
| Connect integration | 커넥터 생태계 | 데이터 파이프라인 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon MSK`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Kinesis Data Streams]] | AWS 네이티브 스트림 | 단순 실시간 수집/처리 | Kafka 호환 요구 없으면 더 단순 |
| [[Amazon Data Firehose]] | 관리형 적재 | 목적지 전송 | Kafka broker 아님 |
| [[Amazon SQS]] | 큐 | 메시지 버퍼링 | 스트림 로그와 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon MSK는 `관리형 Kafka` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- AWS 네이티브 단순 스트림은 Kinesis가 더 단순할 수 있다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon MSK`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| Kafka compatibility, existing Kafka apps, cluster/serverless choice | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon MSK]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 Kafka`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- Kafka 호환성이 핵심 단서면 MSK다.
- MSK는 Kafka 운영 부담을 줄이지만 스트리밍 설계 책임은 남는다.

## 참고 링크

- [Amazon MSK 공식 문서](https://docs.aws.amazon.com/msk/latest/developerguide/what-is-msk.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
