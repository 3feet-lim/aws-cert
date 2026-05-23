---
type: aws-service
service_name: "Amazon Aurora"
category: "05-Database/RDS"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Aurora", "Aurora MySQL", "Aurora PostgreSQL"]
tags: [aws, sap-c02, database, rds, aurora, relational]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Aurora

> [!summary] 한 줄 요약
> MySQL/PostgreSQL 호환 API를 제공하면서 분산 스토리지, 빠른 복구, read scaling, Global Database를 갖춘 AWS 클라우드 최적화 관계형 DB 엔진이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 고성능 관계형 DB, 리전 장애 대비, 읽기 확장, MySQL/PostgreSQL 현대화 |
| 핵심 의사결정 | MySQL/PostgreSQL 호환을 유지하면서 RDS보다 높은 성능/복원력/글로벌 읽기가 필요하면 Aurora |
| 대표 키워드 | Aurora cluster, writer/reader endpoint, six-way replicated storage, Global Database, fast failover |
| 자주 비교되는 서비스 | [[Amazon RDS]], [[Amazon Aurora Serverless]], [[Amazon DynamoDB]], [[Amazon Redshift]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Amazon RDS가 관리하는 AWS 네이티브 관계형 DB 엔진.
- **왜 쓰는가?**: MySQL/PostgreSQL 호환 애플리케이션을 고성능·고가용성 구조로 운영하기 위해 사용한다.
- **관리형 여부**: 제어 plane과 스토리지는 관리형이지만 스키마/쿼리/인덱스/연결/용량 선택은 설계해야 한다.
- **리전/글로벌**: 리전 클러스터 기반이며 Aurora Global Database로 여러 리전에 read-only secondary cluster를 둘 수 있다.
- **핵심 제약/한계**: 모든 RDS 엔진을 대체하지 않으며, 엔진 호환 버전과 기능 제약을 확인해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Cluster storage | 여러 AZ에 자동 복제되는 분산 스토리지 | DB 인스턴스 장애와 스토리지 복구를 분리해서 이해한다. |
| Writer/Reader endpoint | 쓰기 엔드포인트와 읽기 엔드포인트 분리 | 애플리케이션 연결과 failover 설계 포인트. |
| Aurora Replicas | 읽기 확장과 빠른 failover 후보 | read-heavy 서비스에서 중요. |
| Aurora Global Database | primary Region + 여러 secondary Region | 리전 DR과 글로벌 저지연 읽기 단서. |
| Backtrack/PITR/backup | 복구 기능 | 운영 실수 복구와 백업 보존 설계. |
| RDS Proxy | 연결 풀링 | Lambda 또는 많은 client 연결에서 유용. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Aurora]] | AWS 최적화 MySQL/PostgreSQL 호환 엔진 | 고성능/빠른 failover/Global Database | Oracle/SQL Server 호환에는 RDS |
| [[Amazon RDS]] | 표준 엔진 선택 폭이 넓음 | 상용 엔진/기존 버전 호환성 | Aurora 전용 기능을 기대하면 안 됨 |
| [[Amazon Aurora Serverless]] | Aurora 용량 자동 조정 구성 | 예측 어려운/spiky 워크로드 | 상시 고부하엔 provisioned가 비용/성능상 나을 수 있음 |
| [[Amazon DynamoDB]] | 서버리스 NoSQL | 키 기반 초대규모/단순 access pattern | 관계형 join/SQL 호환 요구에는 부적합 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 글로벌 읽기와 빠른 리전 DR

- **요구사항**: 여러 대륙 사용자의 읽기 지연시간을 낮추고 리전 장애에 대비
- **정답 단서**: global users, low-latency reads, regional outage
- **선택할 구성**: Aurora Global Database
- **오답 함정**: RDS read replica만으로 Global Database 수준의 빠른 DR을 기대하면 안 된다.

### 패턴 2: MySQL/PostgreSQL 현대화

- **요구사항**: 기존 앱 호환성을 유지하며 성능과 복원력 개선
- **정답 단서**: MySQL-compatible, PostgreSQL-compatible, high availability
- **선택할 구성**: Amazon Aurora provisioned cluster
- **오답 함정**: DynamoDB로 바꾸면 데이터 모델과 코드 변경이 필요하다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Aurora는 RDS 서비스 아래의 DB 엔진이지만 시험에서는 RDS 표준 엔진과 별도 선택지처럼 비교된다.
- Global Database의 secondary는 기본적으로 read-only이며 write 전환은 failover/switchover 절차가 필요하다.
- 읽기 복제본이 있어도 쓰기는 writer endpoint로 간다.

## 6. 암기 문장

- MySQL/PostgreSQL 호환 + 고성능/글로벌/빠른 복구는 Aurora다.
- Aurora Global Database는 글로벌 읽기와 리전 DR 단서에 강하다.

## 참고 링크

- [What is Amazon Aurora?](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
- [Using Amazon Aurora Global Database](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html)
- [Aurora DB clusters](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
