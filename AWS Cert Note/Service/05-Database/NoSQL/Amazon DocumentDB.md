---
type: aws-service
service_name: "Amazon DocumentDB"
category: "05-Database/NoSQL"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["DocumentDB", "Amazon DocumentDB with MongoDB compatibility"]
tags: [aws, sap-c02, database, nosql, document]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon DocumentDB

> [!summary] 한 줄 요약
> MongoDB 호환 API를 제공하는 완전관리형 문서 데이터베이스로 JSON-like 문서 모델 애플리케이션을 AWS에서 운영한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 문서 모델, MongoDB 호환 앱 마이그레이션, 관리형 클러스터 |
| 핵심 의사결정 | MongoDB API/드라이버 호환을 유지하면서 AWS 관리형 문서 DB로 운영하려면 DocumentDB |
| 대표 키워드 | MongoDB compatibility, document database, JSON documents, cluster, instance, replica |
| 자주 비교되는 서비스 | [[Amazon DynamoDB]], [[Amazon Aurora]], [[Amazon RDS]], [[Amazon Keyspaces]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 문서 지향 데이터 모델과 MongoDB 호환 API를 제공하는 관리형 데이터베이스.
- **왜 쓰는가?**: MongoDB 기반 애플리케이션을 큰 코드 변경 없이 AWS 관리형 환경으로 이전하기 위해 사용한다.
- **관리형 여부**: 클러스터 운영/백업/복제는 관리형이지만 호환 기능, 인덱스, 쿼리 패턴, 마이그레이션 검증은 필요하다.
- **리전/글로벌**: 리전 클러스터 기반이며 여러 AZ에 복제본을 둘 수 있다.
- **핵심 제약/한계**: MongoDB 자체와 100% 동일하다고 가정하면 안 되며 지원 API/기능 호환성을 확인해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Document model | JSON-like 문서 저장 | 유연한 스키마와 nested document 단서. |
| MongoDB-compatible API | MongoDB 드라이버/도구 사용 | 기존 MongoDB 앱 이전 단서. |
| Cluster/instances | 스토리지와 compute 분리된 클러스터 구조 | reader 확장과 failover 이해. |
| Replication/backup | 관리형 복제와 백업 | 운영 부담 감소. |
| TLS/KMS/VPC | 보안 네트워크와 암호화 | private database 설계 포인트. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon DocumentDB]] | MongoDB 호환 문서 DB | 기존 MongoDB 앱/문서 모델 유지 | MongoDB 모든 기능 완전 호환으로 가정 금지 |
| [[Amazon DynamoDB]] | AWS-native 서버리스 NoSQL | 키 기반 초대규모/운영 최소화 | MongoDB API 호환 요구에는 부적합 |
| [[Amazon Aurora]] | 관계형 MySQL/PostgreSQL 호환 | SQL/트랜잭션/관계형 모델 | 문서 API 호환이 목적이면 부적합 |
| [[Amazon Keyspaces]] | Cassandra 호환 wide-column | Cassandra 워크로드 이전 | 문서 모델/MongoDB API와 다름 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: MongoDB 앱 관리형 이전

- **요구사항**: 기존 MongoDB 드라이버와 문서 모델을 유지해야 함
- **정답 단서**: MongoDB-compatible, document, managed
- **선택할 구성**: Amazon DocumentDB cluster
- **오답 함정**: DynamoDB로 바꾸면 데이터 모델과 API 변경이 커진다.

### 패턴 2: 유연한 제품 카탈로그 문서

- **요구사항**: 속성이 다양한 JSON 문서 저장과 조회
- **정답 단서**: JSON document, flexible schema
- **선택할 구성**: DocumentDB 또는 DynamoDB 중 API/access pattern 기준 선택
- **오답 함정**: 복잡한 관계형 join이 필요하면 RDS/Aurora가 맞다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- DocumentDB는 MongoDB 호환 API 서비스이지 MongoDB Community/Enterprise 자체를 그대로 호스팅하는 것이 아니다.
- 서버리스 키-값 scale만 보고 DocumentDB와 DynamoDB를 혼동하지 않는다.
- 인덱스 설계가 부실하면 문서 DB도 성능 문제가 난다.

## 6. 암기 문장

- MongoDB 호환 문서 DB는 DocumentDB다.
- AWS-native NoSQL 신규 설계는 DynamoDB와 먼저 비교한다.

## 참고 링크

- [What is Amazon DocumentDB?](https://docs.aws.amazon.com/documentdb/latest/developerguide/what-is.html)
- [Amazon DocumentDB how it works](https://docs.aws.amazon.com/documentdb/latest/developerguide/how-it-works.html)
- [Amazon DocumentDB compatibility](https://docs.aws.amazon.com/documentdb/latest/developerguide/compatibility.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
