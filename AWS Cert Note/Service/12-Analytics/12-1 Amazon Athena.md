---
type: aws-service
service_name: "Amazon Athena"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Athena", "serverless SQL"]
tags: [aws, sap-c02, query, data-lake, analytics]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Athena

> [!summary] 한 줄 요약
> S3 데이터 레이크의 파일을 서버리스 SQL로 즉시 조회할 때 선택하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | S3 기반 ad-hoc SQL, 로그/데이터 레이크 분석, 인프라 운영 최소화 |
| 대표 키워드 | Athena, serverless SQL, query, data-lake, analytics |
| 자주 비교되는 서비스 | [[Amazon EMR]], [[Amazon Redshift]], [[Amazon QuickSight]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: S3 객체를 테이블처럼 조회한다. Glue Data Catalog와 함께 쓰는 경우가 많다.
- **왜 쓰는가?**: 클러스터 운영 없이 표준 SQL로 분석한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 스캔 데이터량 기반 비용이므로 파티션/컬럼형 포맷이 중요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| S3 쿼리 | S3의 CSV/Parquet/JSON 등을 SQL로 조회 | 데이터 레이크 조회 |
| Glue Catalog | 스키마/메타데이터 관리 | 테이블 정의와 파티션 |
| Federated query | 일부 외부 데이터 소스 질의 | 분산 조회 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon Athena`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EMR]] | 클러스터 기반 Spark/Hadoop 처리 | 복잡한 분산 처리/커스텀 런타임 | 간단 SQL에 EMR은 과함 |
| [[Amazon Redshift]] | 데이터 웨어하우스 | 고성능 반복 BI/웨어하우스 | S3 ad-hoc 조회만이면 과함 |
| [[Amazon QuickSight]] | BI 시각화 | 대시보드/리포팅 | 쿼리 엔진 자체가 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Athena는 `서버리스 SQL 쿼리` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 스캔 데이터량 기반 비용이므로 파티션/컬럼형 포맷이 중요하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Athena`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| S3 기반 ad-hoc SQL, 로그/데이터 레이크 분석, 인프라 운영 최소화 | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Athena]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `서버리스 SQL 쿼리`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- S3 데이터 레이크를 빠르게 SQL로 조회하면 Athena다.
- 대용량 스캔 비용은 파티션·압축·Parquet/ORC로 줄인다.

## 참고 링크

- [Amazon Athena 공식 문서](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
