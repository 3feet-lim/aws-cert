---
type: aws-service
service_name: "Amazon DynamoDB"
category: "05-Database/NoSQL"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["DynamoDB", "DDB"]
tags: [aws, sap-c02, database, nosql, serverless]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon DynamoDB

> [!summary] 한 줄 요약
> 키-값/문서 데이터 모델을 단일 자릿수 ms 지연시간으로 모든 규모에서 처리하는 완전관리형 서버리스 NoSQL 데이터베이스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 서버리스 앱, 초대규모 키 기반 access pattern, 글로벌 테이블, 이벤트 스트림 |
| 핵심 의사결정 | access pattern이 명확한 키-값/문서 워크로드에서 운영 부담 없이 매우 큰 scale이 필요하면 DynamoDB |
| 대표 키워드 | partition key, sort key, single-digit millisecond, on-demand, provisioned capacity, GSI, Streams, Global Tables |
| 자주 비교되는 서비스 | [[Amazon RDS]], [[Amazon Aurora]], [[Amazon ElastiCache]], [[Amazon Keyspaces]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 파티션 키 기반으로 데이터를 분산 저장하는 서버리스 NoSQL 데이터베이스.
- **왜 쓰는가?**: 서버/클러스터 관리 없이 예측 가능한 낮은 지연시간과 자동 확장이 필요한 애플리케이션에 사용한다.
- **관리형 여부**: 인프라/스케일/복제는 관리형이지만 키 설계, access pattern, 인덱스, hot partition 방지는 사용자 책임이다.
- **리전/글로벌**: 리전 서비스이며 Global Tables로 multi-Region active-active 복제를 구성할 수 있다.
- **핵심 제약/한계**: ad-hoc join/복잡한 SQL 질의보다 미리 정의한 access pattern에 최적화되어 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Partition key / sort key | 테이블 기본 키 설계 | 성능과 확장성의 핵심. hot key를 피해야 한다. |
| GSI/LSI | 보조 access pattern 지원 | 인덱스 남발은 비용/일관성/용량에 영향. |
| On-demand capacity | 요청 기반 과금/자동 처리량 | 예측 어려운 트래픽에 적합. |
| Provisioned + Auto Scaling | 설정한 RCU/WCU 기반 | 예측 가능한 트래픽 비용 최적화. |
| DynamoDB Streams | 항목 변경 이벤트 스트림 | Lambda/EventBridge/Kinesis 연동 시나리오. |
| Global Tables | multi-Region replica | 낮은 지연시간 글로벌 읽기/쓰기와 DR 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon DynamoDB]] | 서버리스 키-값/문서 NoSQL | 초대규모, 낮은 지연시간, 단순 access pattern | SQL join/복잡한 ad-hoc query에는 부적합 |
| [[Amazon RDS]] | 관계형 SQL DB | 정규화, join, 복잡한 트랜잭션 | 수평 확장/운영 부담이 더 큼 |
| [[Amazon ElastiCache]] | 인메모리 캐시/데이터스토어 | DB 앞 캐시, 세션, 초저지연 | 영구 원장 DB 대체로 오해하면 위험 |
| [[Amazon Keyspaces]] | Cassandra 호환 관리형 DB | 기존 Cassandra 코드/도구 유지 | 새 AWS-native key-value 앱은 DynamoDB가 더 자연스러움 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 서버리스 쇼핑카트/세션 저장

- **요구사항**: 사용자별 단순 key lookup과 높은 트래픽
- **정답 단서**: key-value, single-digit millisecond, serverless
- **선택할 구성**: DynamoDB on-demand + TTL + Streams
- **오답 함정**: RDS로 세션을 저장하면 scale/운영 부담이 커질 수 있다.

### 패턴 2: multi-Region active-active 앱

- **요구사항**: 여러 리전에서 로컬 읽기/쓰기와 자동 복제 필요
- **정답 단서**: global table, multi-active, low latency
- **선택할 구성**: DynamoDB Global Tables
- **오답 함정**: Aurora Global Database secondary는 기본 read-only라 쓰기 패턴이 다르다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- DynamoDB는 쿼리를 자유롭게 나중에 정하는 DB가 아니라 access pattern을 먼저 설계하는 DB다.
- Global Tables는 충돌/last writer wins와 복제 지연을 고려해야 한다.
- DAX/ElastiCache는 캐시이고 DynamoDB 자체와 역할이 다르다.

## 6. 암기 문장

- 키 설계가 명확한 초대규모 서버리스 NoSQL은 DynamoDB다.
- 글로벌 active-active 키-값은 DynamoDB Global Tables를 떠올린다.

## 참고 링크

- [What is Amazon DynamoDB?](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [DynamoDB global tables](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html)
- [DynamoDB capacity modes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
