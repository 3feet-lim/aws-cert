---
type: aws-service
service_name: "Amazon Keyspaces"
category: "05-Database/NoSQL"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Keyspaces", "Amazon Keyspaces for Apache Cassandra"]
tags: [aws, sap-c02, database, nosql, cassandra]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Keyspaces

> [!summary] 한 줄 요약
> Apache Cassandra 호환 API를 서버리스 관리형으로 제공해 기존 Cassandra 애플리케이션을 운영 부담 없이 AWS에서 실행하는 wide-column 데이터베이스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | Cassandra 워크로드 마이그레이션, wide-column, 서버리스 NoSQL, 고가용성 |
| 핵심 의사결정 | Cassandra Query Language와 기존 Cassandra 코드/도구 호환이 핵심이면 Keyspaces |
| 대표 키워드 | Apache Cassandra compatible, CQL, serverless, wide-column, multi-Region replication |
| 자주 비교되는 서비스 | [[Amazon DynamoDB]], [[Amazon DocumentDB]], [[Amazon RDS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Apache Cassandra와 호환되는 CQL 기반 관리형 wide-column 데이터베이스.
- **왜 쓰는가?**: Cassandra 운영 부담을 줄이고 기존 애플리케이션 코드/도구를 유지하기 위해 사용한다.
- **관리형 여부**: 서버/패치/복제는 관리형이지만 파티션 키, CQL 모델, 처리량/일관성 옵션 설계는 필요하다.
- **리전/글로벌**: 리전 서비스이며 multi-Region replication 기능을 사용할 수 있다.
- **핵심 제약/한계**: Cassandra 호환성이 목적이 아닌 신규 AWS-native NoSQL이면 DynamoDB가 더 자주 정답이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| CQL compatibility | Cassandra Query Language 사용 | 기존 Cassandra 앱 이전 단서. |
| Serverless capacity | 용량 관리 부담 감소 | 운영 복잡도 제거. |
| Multi-Region replication | 여러 리전 복제 | 글로벌 고가용성/DR 요구. |
| PITR/backup | 복구 기능 | 운영 실수 복구. |
| Encryption/IAM | KMS와 IAM 통합 | AWS 보안 통제와 결합. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Keyspaces]] | Cassandra 호환 wide-column | Cassandra 코드/도구 유지 | DynamoDB와 API/모델이 다름 |
| [[Amazon DynamoDB]] | AWS-native key-value/document | 신규 서버리스 NoSQL, global tables | CQL 호환 요구에는 부적합 |
| [[Amazon DocumentDB]] | MongoDB 호환 문서 DB | 문서 모델/MongoDB API | Cassandra wide-column과 다름 |
| Self-managed Cassandra on EC2 | 전체 Cassandra 제어 | 특수 설정/버전/플러그인 필요 | 운영 부담과 HA 책임이 큼 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: Cassandra 클러스터 운영 제거

- **요구사항**: 기존 CQL 앱은 유지하면서 패치/노드 운영을 줄임
- **정답 단서**: Cassandra-compatible, CQL, managed, serverless
- **선택할 구성**: Amazon Keyspaces
- **오답 함정**: DynamoDB로 이전하면 코드와 데이터 모델 변경이 필요할 수 있다.

### 패턴 2: 글로벌 Cassandra 스타일 워크로드

- **요구사항**: 여러 리전 고가용성과 낮은 지연시간 필요
- **정답 단서**: multi-Region, CQL, high availability
- **선택할 구성**: Keyspaces multi-Region replication
- **오답 함정**: Aurora Global Database는 관계형 read replica 중심 패턴이다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Keyspaces의 핵심은 Cassandra 호환성이다.
- DynamoDB와 둘 다 NoSQL이지만 API, 데이터 모델, 설계 방식이 다르다.
- 기존 Cassandra 기능이 모두 동일하게 동작한다고 가정하지 말고 호환 범위를 확인해야 한다.

## 6. 암기 문장

- Cassandra 호환 관리형 DB는 Keyspaces다.
- 신규 AWS-native NoSQL이면 DynamoDB와 비교한다.

## 참고 링크

- [What is Amazon Keyspaces?](https://docs.aws.amazon.com/keyspaces/latest/devguide/what-is-keyspaces.html)
- [Amazon Keyspaces multi-Region replication](https://docs.aws.amazon.com/keyspaces/latest/devguide/multiRegion-replication.html)
- [Amazon Keyspaces capacity modes](https://docs.aws.amazon.com/keyspaces/latest/devguide/ReadWriteCapacityMode.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
