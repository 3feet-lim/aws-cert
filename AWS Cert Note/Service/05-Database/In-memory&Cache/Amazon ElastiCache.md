---
type: aws-service
service_name: "Amazon ElastiCache"
category: "05-Database/In-memory&Cache"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["ElastiCache", "ElastiCache for Redis", "ElastiCache for Valkey", "ElastiCache for Memcached"]
tags: [aws, sap-c02, database, cache, in-memory]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon ElastiCache

> [!summary] 한 줄 요약
> Valkey/Redis OSS 또는 Memcached 호환 인메모리 캐시를 관리형으로 제공해 애플리케이션 지연시간과 데이터베이스 부하를 줄이는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 캐싱, 세션 저장, 초저지연 read, DB 부하 감소, in-memory data store |
| 핵심 의사결정 | 반복 조회/세션/랭킹/카운터처럼 초저지연 인메모리 접근이 필요하면 ElastiCache |
| 대표 키워드 | cache, Redis OSS, Valkey, Memcached, session store, lazy loading, write-through, TTL |
| 자주 비교되는 서비스 | [[Amazon DynamoDB]], [[Amazon RDS]], [[Amazon MemoryDB]], [[Amazon CloudFront]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 관리형 인메모리 캐시/데이터스토어 서비스.
- **왜 쓰는가?**: DB 앞 캐시, 세션 저장, rate limiting, leaderboard 등 ms 미만/초저지연 접근을 위해 사용한다.
- **관리형 여부**: 노드/클러스터 운영은 관리형이지만 캐시 무효화, eviction, consistency, persistence 옵션은 설계해야 한다.
- **리전/글로벌**: 리전/VPC 내 클러스터로 배치하고 Multi-AZ/replication group을 구성할 수 있다.
- **핵심 제약/한계**: 영구 원장 데이터베이스가 아니라 캐시/인메모리 계층으로 이해해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Valkey/Redis OSS | 고급 자료구조, pub/sub, replication | 세션, leaderboard, counter, distributed lock 단서. |
| Memcached | 단순 분산 캐시 | 단순 object cache와 수평 확장. |
| TTL/Eviction | 캐시 만료/축출 | stale data와 메모리 부족 설계. |
| Cluster mode | 샤딩 기반 확장 | 대용량/고처리량 Redis 계열 확장. |
| Multi-AZ failover | replica와 자동 장애 조치 | 캐시 가용성 요구. |
| Cache patterns | lazy loading/write-through | DB 부하와 일관성 트레이드오프. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon ElastiCache]] | 인메모리 캐시/데이터스토어 | DB 부하 감소, 세션, 초저지연 | 영구 primary DB 대체로 오해 금지 |
| [[Amazon DynamoDB]] | 서버리스 NoSQL primary store | 영구 키-값 저장과 글로벌 테이블 | 순수 캐시 지연시간/자료구조 목적에는 ElastiCache |
| [[Amazon RDS]] | 관계형 영구 DB | SQL 트랜잭션과 영구 저장 | 반복 읽기 부하는 캐시로 완화 |
| [[Amazon CloudFront]] | edge 콘텐츠 캐시 | 정적/HTTP 콘텐츠 글로벌 캐시 | 애플리케이션 내부 데이터 캐시와 다름 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: DB 읽기 부하 완화

- **요구사항**: 상품/프로필 조회가 반복되어 RDS가 병목
- **정답 단서**: cache, repeated reads, low latency
- **선택할 구성**: ElastiCache lazy loading + RDS
- **오답 함정**: RDS read replica만으로 hot read latency를 충분히 낮추지 못할 수 있다.

### 패턴 2: 웹 세션 저장

- **요구사항**: EC2/ECS 인스턴스가 Auto Scaling되어도 세션 유지 필요
- **정답 단서**: session store, shared state, low latency
- **선택할 구성**: ElastiCache Redis/Valkey
- **오답 함정**: 로컬 메모리 세션은 scale-in/장애에 취약하다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- 캐시는 원본 데이터와 일관성 문제가 생길 수 있으므로 TTL/무효화 전략이 필요하다.
- ElastiCache는 VPC 내부 리소스이며 인터넷에서 직접 접근하는 서비스가 아니다.
- Redis 계열 persistence가 있어도 일반 영구 DB와 동일한 내구성 모델로 보면 안 된다.

## 6. 암기 문장

- 반복 읽기와 세션을 빠르게 하려면 ElastiCache다.
- 영구 저장은 RDS/DynamoDB, 글로벌 콘텐츠 캐시는 CloudFront와 구분한다.

## 참고 링크

- [What is Amazon ElastiCache?](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/WhatIs.html)
- [Caching strategies](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/Strategies.html)
- [Replication groups](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/Replication.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
