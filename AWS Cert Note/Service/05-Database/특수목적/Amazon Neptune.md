---
type: aws-service
service_name: "Amazon Neptune"
category: "05-Database/특수목적"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Neptune"]
tags: [aws, sap-c02, database, graph]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Neptune

> [!summary] 한 줄 요약
> 복잡한 관계와 연결 탐색을 Gremlin/openCypher/SPARQL로 빠르게 질의하는 완전관리형 그래프 데이터베이스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 그래프 관계 분석, 추천, fraud detection, knowledge graph, network topology |
| 핵심 의사결정 | 데이터의 핵심이 행/문서가 아니라 관계와 경로 탐색이면 Neptune |
| 대표 키워드 | graph database, Gremlin, openCypher, SPARQL, relationships, traversal, knowledge graph |
| 자주 비교되는 서비스 | [[Amazon DynamoDB]], [[Amazon RDS]], [[Amazon Redshift]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 노드와 엣지 관계를 저장하고 탐색하는 관리형 그래프 데이터베이스.
- **왜 쓰는가?**: 추천, 부정 탐지, 소셜 그래프, 네트워크/보안 관계, 지식 그래프를 빠르게 탐색하기 위해 사용한다.
- **관리형 여부**: DB 클러스터 운영은 관리형이지만 그래프 모델링, 쿼리 언어, 인덱스/데이터 로딩은 설계해야 한다.
- **리전/글로벌**: 리전 클러스터 기반이며 read replica와 백업/스냅샷을 사용한다.
- **핵심 제약/한계**: 일반 OLTP SQL/문서/키-값 저장소가 아니라 관계 traversal이 핵심일 때 선택한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Property graph/RDF | 두 가지 그래프 모델 지원 | Gremlin/openCypher 또는 SPARQL 단서. |
| Graph traversal | 관계 경로 탐색 | multi-hop relationship 문제에 적합. |
| Read replica | 읽기 확장 | 분석/탐색 쿼리 확장. |
| Bulk load | S3에서 데이터 로딩 | 대규모 그래프 적재 패턴. |
| ML/analytics integration | 그래프 기반 ML/분석 연동 | 추천/부정탐지 시나리오. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Neptune]] | 그래프 관계 DB | 관계/경로 탐색이 핵심 | 단순 key lookup에는 과함 |
| [[Amazon DynamoDB]] | 키-값/문서 NoSQL | 대규모 단순 access pattern | multi-hop relationship query는 복잡 |
| [[Amazon RDS]] | 관계형 SQL DB | 정형 SQL, join, 트랜잭션 | 깊은 graph traversal은 비효율적일 수 있음 |
| [[Amazon Redshift]] | 분석용 데이터 웨어하우스 | 대규모 BI/OLAP | 실시간 그래프 탐색 DB가 아님 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 부정 거래 탐지

- **요구사항**: 계정·기기·카드·IP 관계를 여러 단계로 추적
- **정답 단서**: fraud, connected data, graph traversal
- **선택할 구성**: Amazon Neptune
- **오답 함정**: RDS join으로 깊은 관계 탐색을 반복하면 복잡/비효율적일 수 있다.

### 패턴 2: 추천/지식 그래프

- **요구사항**: 사용자-상품-속성 관계 기반 추천
- **정답 단서**: recommendation, knowledge graph, relationships
- **선택할 구성**: Neptune + Gremlin/openCypher/SPARQL
- **오답 함정**: DynamoDB는 단순 key-value 조회에 강하지만 그래프 탐색은 직접 구현해야 한다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Neptune은 관계형 DB의 “relationship”이 아니라 그래프 traversal을 위한 서비스다.
- 그래프가 필요 없고 단순 조회면 DynamoDB/RDS가 더 단순하다.
- 쿼리 언어 선택(Gremlin/openCypher/SPARQL)이 데이터 모델과 연결된다.

## 6. 암기 문장

- 관계와 경로 탐색이 문제의 핵심이면 Neptune이다.
- BI 분석은 Redshift, 키-값 조회는 DynamoDB와 구분한다.

## 참고 링크

- [What is Amazon Neptune?](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html)
- [Neptune graph models](https://docs.aws.amazon.com/neptune/latest/userguide/feature-overview-data-models.html)
- [Neptune bulk load](https://docs.aws.amazon.com/neptune/latest/userguide/bulk-load.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
