---
type: aws-service
service_name: "Amazon RDS"
category: "05-Database/RDS"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["RDS", "Relational Database Service"]
tags: [aws, sap-c02, database, rds, relational]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon RDS

> [!summary] 한 줄 요약
> MySQL, PostgreSQL, MariaDB, Oracle, SQL Server 등 관계형 데이터베이스를 백업·패치·Multi-AZ·읽기 복제본과 함께 관리형으로 운영하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 기존 관계형 DB 이전, 관리형 운영, Multi-AZ HA, read scaling, 백업/복구 |
| 핵심 의사결정 | 상용/오픈소스 RDBMS 호환성과 관리형 운영이 필요하면 RDS |
| 대표 키워드 | managed relational database, Multi-AZ, read replica, automated backup, PITR, engine compatibility |
| 자주 비교되는 서비스 | [[Amazon Aurora]], [[Amazon DynamoDB]], [[Amazon Redshift]], [[Amazon EC2]] self-managed DB |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS가 인프라 운영을 관리하는 관계형 데이터베이스 서비스.
- **왜 쓰는가?**: 기존 SQL 애플리케이션을 크게 바꾸지 않고 AWS 관리형 DB로 이전하기 위해 사용한다.
- **관리형 여부**: DB 인프라, 백업, 패치, 장애 조치는 관리형이지만 스키마/쿼리/인덱스/엔진 튜닝은 사용자 책임이다.
- **리전/글로벌**: DB 인스턴스는 리전 내 AZ에 배치하며 Multi-AZ와 read replica로 가용성과 읽기 확장을 설계한다.
- **핵심 제약/한계**: 엔진별 기능 차이, 스토리지/IOPS, 연결 수, 패치 윈도우, cross-Region DR 제약을 확인해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Multi-AZ DB instance/deployment | 동기식 standby 또는 다중 AZ 고가용성 구성 | 장애 조치/HA 단서. 읽기 확장 목적이 아니다. |
| Read replica | 비동기 복제 읽기 확장 | 읽기 부하 분산과 일부 DR에 사용. 강한 동기 HA와 다르다. |
| Automated backup/PITR | 백업 보존 기간 내 특정 시점 복구 | 운영 실수/데이터 손상 복구 단서. |
| Storage autoscaling | 할당 스토리지 자동 증가 | 용량 부족 방지. 성능 병목을 자동 해결하지 않는다. |
| RDS Proxy | 연결 풀링과 failover 개선 | Lambda/RDS 연결 폭주와 failover 시간을 줄이는 단서. |
| Performance Insights | DB 부하 분석 | 쿼리/대기 이벤트 분석과 튜닝 근거. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon RDS]] | 표준 RDBMS 엔진 관리형 | 기존 MySQL/PostgreSQL/Oracle/SQL Server 호환성이 핵심 | 대규모 글로벌 쓰기/서버리스 NoSQL에는 부적합 |
| [[Amazon Aurora]] | AWS 클라우드 최적화 MySQL/PostgreSQL 호환 엔진 | 고성능, 빠른 복구, Aurora Global Database 필요 | Oracle/SQL Server 호환이 필요하면 RDS 엔진 |
| [[Amazon DynamoDB]] | 키-값/문서 NoSQL, 서버리스 확장 | 단순 access pattern과 매우 높은 scale | 복잡한 SQL join/transaction 중심이면 RDS |
| EC2 self-managed DB | OS/DB 전체 제어 | 특수 확장/라이선스/OS 제어 필요 | 관리형 HA/백업을 직접 구현해야 함 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 기존 Oracle/SQL Server 워크로드 이전

- **요구사항**: 애플리케이션 변경 최소화와 라이선스/엔진 호환성 유지
- **정답 단서**: existing relational database, minimal code change, managed backup
- **선택할 구성**: Amazon RDS 해당 엔진 + Multi-AZ + 백업
- **오답 함정**: DynamoDB/Aurora로 바로 전환하면 앱 변경이 커질 수 있다.

### 패턴 2: 읽기 부하 증가

- **요구사항**: 쓰기보다 읽기 쿼리가 많고 지연시간을 낮춰야 함
- **정답 단서**: read-heavy, reporting queries, read replica
- **선택할 구성**: RDS read replica 또는 캐시 조합
- **오답 함정**: Multi-AZ standby를 읽기 확장용으로 착각하면 오답.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Multi-AZ는 HA, read replica는 읽기 확장이다.
- 자동 백업은 백업 보존 기간 내 PITR을 제공하지만 장기 보존/조직 정책은 AWS Backup을 함께 본다.
- RDS는 서버리스가 아니다. 인스턴스 크기, 스토리지, 연결 수를 설계해야 한다.

## 6. 암기 문장

- 기존 관계형 DB를 관리형으로 옮기면 RDS다.
- HA는 Multi-AZ, 읽기 확장은 read replica, 연결 폭주는 RDS Proxy를 떠올린다.

## 참고 링크

- [What is Amazon RDS?](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [High availability for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
- [Working with read replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
