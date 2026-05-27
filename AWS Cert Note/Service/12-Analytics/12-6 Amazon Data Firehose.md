---
type: aws-service
service_name: "Amazon Data Firehose"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Kinesis Data Firehose", "Firehose"]
tags: [aws, sap-c02, streaming, delivery, etl]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Data Firehose

> [!summary] 한 줄 요약
> 스트리밍 데이터를 S3·Redshift·OpenSearch 등 대상으로 거의 실시간 적재하는 관리형 전송 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | stream delivery, buffering, transformation, destination loading |
| 대표 키워드 | Kinesis Data Firehose, Firehose, streaming, delivery, etl |
| 자주 비교되는 서비스 | [[Amazon Kinesis Data Streams]], [[Amazon Managed Service for Apache Flink]], [[AWS Glue]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 버퍼링·변환·압축·암호화 후 목적지로 전송한다.
- **왜 쓰는가?**: consumer 애플리케이션 운영 없이 데이터 적재를 자동화한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 복잡한 실시간 처리나 다중 consumer 재처리는 KDS/Flink가 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Destinations | S3/Redshift/OpenSearch/Splunk 등 | 적재 요구 |
| Buffering | 크기/시간 기반 배치 | 지연/비용 균형 |
| Lambda transform | 간단 변환 | 수집 전 정제 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon Data Firehose`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Kinesis Data Streams]] | 스트림 처리 플랫폼 | 직접 consumer/재처리 | 단순 적재에는 과함 |
| [[Amazon Managed Service for Apache Flink]] | 실시간 분석 애플리케이션 | 윈도우/상태 처리 | 전송 서비스가 아님 |
| [[AWS Glue]] | 배치/ETL | 후처리 변환 | 실시간 적재와 구분 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Data Firehose는 `관리형 스트림 적재` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 복잡한 실시간 처리나 다중 consumer 재처리는 KDS/Flink가 적합하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Data Firehose`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| stream delivery, buffering, transformation, destination loading | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Data Firehose]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 스트림 적재`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 목적지로 스트리밍 데이터를 안정적으로 적재하면 Firehose다.
- Firehose는 직접 consumer 처리용 스트림 버퍼가 아니다.

## 참고 링크

- [Amazon Data Firehose 공식 문서](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
