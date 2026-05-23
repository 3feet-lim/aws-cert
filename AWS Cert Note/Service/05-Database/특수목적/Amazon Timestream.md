---
type: aws-service
service_name: "Amazon Timestream"
category: "05-Database/특수목적"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Timestream", "Timestream for LiveAnalytics", "Timestream for InfluxDB"]
tags: [aws, sap-c02, database, time-series, iot]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Timestream

> [!summary] 한 줄 요약
> 시간 순서로 발생하는 IoT/운영/애플리케이션 메트릭 데이터를 수집·저장·분석하기 위한 관리형 시계열 데이터베이스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | IoT telemetry, observability metrics, time-series analytics, lifecycle tiering |
| 핵심 의사결정 | 데이터가 시간 축 기반이고 최근/과거 데이터를 효율적으로 저장·질의해야 하면 Timestream |
| 대표 키워드 | time series, timestamp, measure, retention, memory store, magnetic store, IoT metrics |
| 자주 비교되는 서비스 | [[Amazon DynamoDB]], [[Amazon Redshift]], [[Amazon CloudWatch]], [[Amazon RDS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 시간(timestamp)과 측정값 중심의 데이터를 저장/분석하는 관리형 시계열 DB.
- **왜 쓰는가?**: 센서, 로그 메트릭, 애플리케이션 성능 지표처럼 시간 기반 집계와 추세 분석을 위해 사용한다.
- **관리형 여부**: 수집/저장/쿼리 엔진은 관리형이지만 retention, partitioning, ingest, query 비용은 설계해야 한다.
- **리전/글로벌**: 리전 서비스이며 Timestream for LiveAnalytics와 Timestream for InfluxDB 선택지가 있다.
- **핵심 제약/한계**: 일반 OLTP/문서/그래프 데이터 모델이 아니라 시간 기반 측정 데이터에 특화되어 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Time-series model | time, dimension, measure 기반 | IoT/metrics 단서. |
| Memory/Magnetic store | 최근 데이터와 장기 데이터 tier | retention/cost 최적화. |
| Scheduled query | 반복 집계 사전 계산 | 대시보드/장기 집계 가속. |
| SQL query | 시계열 함수와 SQL 분석 | 윈도우/집계/추세 분석. |
| InfluxDB option | InfluxDB 호환 워크로드 | 기존 InfluxDB 앱 이전 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Timestream]] | 시계열 DB | timestamp 기반 telemetry/metrics | 일반 key-value/relational workload에는 부적합 |
| [[Amazon DynamoDB]] | 범용 NoSQL | 단순 key lookup과 대규모 이벤트 저장 | 시계열 함수/retention 계층은 직접 설계 필요 |
| [[Amazon CloudWatch]] | 모니터링 메트릭/로그 서비스 | AWS 리소스 관찰성 | 애플리케이션 도메인 시계열 분석 DB와 다름 |
| [[Amazon Redshift]] | DW/OLAP | 대규모 BI 분석 | 실시간 시계열 ingest와 retention 최적화는 Timestream |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: IoT 센서 데이터 분석

- **요구사항**: 수백만 센서의 시간별 측정값 저장과 최근/장기 조회
- **정답 단서**: IoT, telemetry, time-series, retention
- **선택할 구성**: Amazon Timestream
- **오답 함정**: RDS에 모든 시계열을 저장하면 scale/비용/쿼리 최적화가 어렵다.

### 패턴 2: 운영 메트릭 추세 분석

- **요구사항**: 애플리케이션 지표를 시간 창으로 집계
- **정답 단서**: metrics, trend, window query
- **선택할 구성**: Timestream scheduled query + dashboard
- **오답 함정**: CloudWatch는 AWS 모니터링 중심이고 도메인 데이터 분석 DB와 구분한다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Timestream은 “시간 축”이 핵심 단서다.
- 단순 이벤트 로그 저장만이면 S3/Athena 또는 DynamoDB와 비교한다.
- 최근 데이터와 장기 데이터 retention 정책이 비용과 성능에 직접 영향 준다.

## 6. 암기 문장

- timestamp 기반 측정 데이터는 Timestream이다.
- BI DW는 Redshift, AWS 모니터링은 CloudWatch와 구분한다.

## 참고 링크

- [Amazon Timestream documentation](https://docs.aws.amazon.com/timestream/)
- [How Timestream works](https://docs.aws.amazon.com/timestream/latest/developerguide/how-it-works.html)
- [Timestream scheduled queries](https://docs.aws.amazon.com/timestream/latest/developerguide/scheduledqueries.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
