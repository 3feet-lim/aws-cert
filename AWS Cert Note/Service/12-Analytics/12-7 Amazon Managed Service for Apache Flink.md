---
type: aws-service
service_name: "Amazon Managed Service for Apache Flink"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Kinesis Data Analytics", "Managed Service for Apache Flink"]
tags: [aws, sap-c02, streaming, flink, real-time]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Managed Service for Apache Flink

> [!summary] 한 줄 요약
> Apache Flink 애플리케이션을 관리형으로 실행해 상태 기반 실시간 스트림 분석을 수행한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | windowing, stateful processing, real-time analytics |
| 대표 키워드 | Kinesis Data Analytics, Managed Service for Apache Flink, streaming, flink, real-time |
| 자주 비교되는 서비스 | [[Amazon Data Firehose]], [[Amazon Kinesis Data Streams]], [[AWS Glue]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Kinesis/MSK 등 스트림을 입력으로 받아 Flink 애플리케이션을 실행한다.
- **왜 쓰는가?**: 복잡한 실시간 집계·CEP·상태 처리를 처리한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 단순 적재는 Firehose가 더 단순하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Stateful processing | 상태/체크포인트 기반 처리 | 정확성/복구 |
| Window/Aggregation | 시간창 집계 | 실시간 지표 |
| Sources/Sinks | Kinesis/MSK/S3 등 | 스트림 파이프라인 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon Managed Service for Apache Flink`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Data Firehose]] | 전송/적재 | 목적지 로딩 | 분석 애플리케이션 아님 |
| [[Amazon Kinesis Data Streams]] | 스트림 저장/전달 | 레코드 수집과 consumer | 처리 로직은 별도 |
| [[AWS Glue]] | ETL | 배치/서버리스 변환 | Flink 실시간 상태 처리와 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Managed Service for Apache Flink는 `관리형 Flink 실행` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 단순 적재는 Firehose가 더 단순하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Managed Service for Apache Flink`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| windowing, stateful processing, real-time analytics | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Managed Service for Apache Flink]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 Flink 실행`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 실시간 윈도우 집계·상태 처리가 나오면 Managed Service for Apache Flink다.
- 수집은 KDS/MSK, 단순 적재는 Firehose로 구분한다.

## 참고 링크

- [Amazon Managed Service for Apache Flink 공식 문서](https://docs.aws.amazon.com/managed-flink/latest/java/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
