---
type: aws-service
service_name: "Amazon Redshift"
category: "05-Database/특수목적"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Redshift", "Amazon Redshift Serverless"]
tags: [aws, sap-c02, database, analytics, data-warehouse]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Redshift

> [!summary] 한 줄 요약
> 대규모 구조화/반구조화 데이터를 SQL로 분석하는 AWS 관리형 데이터 웨어하우스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 데이터 웨어하우스, BI/OLAP, 대규모 분석, lake house, Redshift Spectrum |
| 핵심 의사결정 | 운영 트랜잭션이 아니라 대규모 분석 SQL/BI가 핵심이면 Redshift |
| 대표 키워드 | data warehouse, OLAP, columnar, MPP, Spectrum, RA3, Serverless, BI |
| 자주 비교되는 서비스 | [[Amazon RDS]], [[Amazon Aurora]], [[Amazon Athena]], [[Amazon EMR]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 대규모 분석 질의를 위한 columnar/MPP 기반 관리형 데이터 웨어하우스.
- **왜 쓰는가?**: BI, 리포팅, 데이터 마트, 대규모 집계/조인 분석을 빠르게 수행하기 위해 사용한다.
- **관리형 여부**: 클러스터/서버리스 운영은 관리형이지만 배포 방식, 데이터 모델, sort/distribution, workload management는 설계해야 한다.
- **리전/글로벌**: 리전 서비스이며 Redshift Serverless 또는 provisioned cluster로 사용한다.
- **핵심 제약/한계**: OLTP 트랜잭션 처리 DB가 아니며 운영 앱의 primary database로 선택하면 오답일 가능성이 높다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Columnar storage/MPP | 분산 병렬 분석 처리 | OLAP/집계/BI 단서. |
| RA3 managed storage | compute/storage 분리 성격 | 확장성과 비용 설계. |
| Redshift Spectrum | S3 데이터 직접 질의 | 데이터 레이크 연동. |
| Redshift Serverless | 서버리스 분석 용량 | 간헐적/예측 어려운 분석 워크로드. |
| Materialized view | 반복 분석 쿼리 가속 | BI 성능 최적화. |
| Data sharing/Zero-ETL | 다른 데이터 소스와 통합 | 최신 AWS 분석 통합 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Redshift]] | 데이터 웨어하우스/OLAP | 대규모 SQL 분석과 BI | 트랜잭션 앱 DB로 사용하면 안 됨 |
| [[Amazon RDS]] | OLTP 관계형 DB | 운영 앱 트랜잭션 | 대규모 분석 부하를 OLTP DB에 직접 주면 성능 영향 |
| [[Amazon Athena]] | S3 데이터 serverless query | 간헐적 ad-hoc S3 분석 | 지속적 고성능 DW는 Redshift |
| [[Amazon EMR]] | Spark/Hadoop 빅데이터 처리 | 커스텀 분산 처리/ETL | BI SQL DW는 Redshift가 단순 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 전사 BI 데이터 웨어하우스

- **요구사항**: 여러 소스 데이터를 모아 SQL 리포팅과 대시보드 제공
- **정답 단서**: data warehouse, BI, OLAP, aggregate
- **선택할 구성**: Amazon Redshift
- **오답 함정**: RDS는 OLTP라 분석 부하에 취약하다.

### 패턴 2: S3 데이터 레이크와 DW 결합

- **요구사항**: S3 원천 데이터를 SQL로 함께 분석
- **정답 단서**: Spectrum, data lake, SQL analytics
- **선택할 구성**: Redshift + Spectrum 또는 Athena 비교
- **오답 함정**: 짧은 ad-hoc 쿼리만 있으면 Athena가 더 단순할 수 있다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Redshift는 PostgreSQL 호환처럼 보여도 운영 OLTP DB가 아니라 분석 DW다.
- Athena는 서버리스 쿼리, Redshift는 고성능/지속적 DW 성격이 강하다.
- 분산 키/sort key/workload 관리가 성능에 영향을 준다.

## 6. 암기 문장

- BI/OLAP 데이터 웨어하우스는 Redshift다.
- 운영 트랜잭션은 RDS/Aurora, S3 ad-hoc SQL은 Athena와 비교한다.

## 참고 링크

- [Introduction to Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/dg/welcome.html)
- [Amazon Redshift Serverless](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-whatis.html)
- [Querying external data using Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-using-spectrum.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
