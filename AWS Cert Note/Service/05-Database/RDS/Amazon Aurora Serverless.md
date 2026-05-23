---
type: aws-service
service_name: "Amazon Aurora Serverless"
category: "05-Database/RDS"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Aurora Serverless", "Aurora Serverless v2"]
tags: [aws, sap-c02, database, aurora, serverless]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Aurora Serverless

> [!summary] 한 줄 요약
> Amazon Aurora의 용량을 ACU 단위로 자동 조정해 예측하기 어렵거나 변동이 큰 관계형 워크로드를 운영하는 구성이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | spiky/불규칙 관계형 워크로드, 용량 자동 조정, 개발/테스트, 비용 최적화 |
| 핵심 의사결정 | Aurora 호환 관계형 DB가 필요하지만 피크/유휴 변동이 커서 자동 용량 조정이 중요하면 Aurora Serverless |
| 대표 키워드 | ACU, auto scaling, variable workload, Aurora Serverless v2, capacity range |
| 자주 비교되는 서비스 | [[Amazon Aurora]], [[Amazon RDS]], [[AWS Lambda]], [[Amazon DynamoDB]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Aurora 클러스터의 DB 인스턴스 용량을 자동 조정하는 서버리스형 구성.
- **왜 쓰는가?**: 관계형 SQL/트랜잭션을 유지하면서 예측 어려운 트래픽에 대응하기 위해 사용한다.
- **관리형 여부**: 용량 조정은 관리형이지만 최소/최대 ACU, 연결, 쿼리, 비용, failover 설계는 필요하다.
- **리전/글로벌**: 리전 기반 Aurora 클러스터 구성이고 Aurora 기능 지원 범위는 버전/엔진별로 확인한다.
- **핵심 제약/한계**: 완전히 0 비용이 되는 범용 DB가 아니며, 최소 용량과 scaling 동작/제약을 이해해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| ACU | Aurora Capacity Unit 단위 용량 | 최소/최대 범위를 잘못 잡으면 비용 또는 성능 문제가 난다. |
| Autoscaling | 부하에 따라 용량 자동 조정 | spiky 워크로드와 예측 불가 트래픽 단서. |
| Compatibility | Aurora MySQL/PostgreSQL 기반 | SQL 호환성과 관계형 트랜잭션 유지. |
| Reader support | v2는 reader와 여러 Aurora 기능 지원 범위 확대 | 읽기 확장과 HA를 provisioned와 비교한다. |
| RDS Proxy/Data API | 연결 관리와 HTTP API 패턴 | 서버리스 앱과 DB 연결 폭주를 조심한다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Aurora Serverless]] | Aurora 용량 자동 조정 | 불규칙/spiky 관계형 워크로드 | 항상 고부하라면 provisioned가 단순/비용 효율적일 수 있음 |
| [[Amazon Aurora]] provisioned | 고정 인스턴스 용량 | 예측 가능하고 지속적인 고부하 | 유휴 시간 비용 최적화에는 약할 수 있음 |
| [[Amazon DynamoDB]] | 서버리스 NoSQL | 키-값 access pattern, 초대규모, 완전 관리형 scale | SQL join/관계형 제약 필요하면 Aurora |
| [[AWS Lambda]] | 함수 실행 서비스 | 이벤트 compute | 데이터베이스가 아니라 앱 실행 계층 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 트래픽이 들쭉날쭉한 SaaS DB

- **요구사항**: 업무 시간/이벤트 때만 부하가 높고 SQL 호환 필요
- **정답 단서**: variable traffic, relational, auto scaling capacity
- **선택할 구성**: Aurora Serverless v2
- **오답 함정**: DynamoDB는 모델 변경이 필요하고 provisioned Aurora는 유휴 비용이 클 수 있다.

### 패턴 2: 개발/테스트 관계형 환경

- **요구사항**: 사용 시간은 적지만 Aurora 호환 DB 필요
- **정답 단서**: intermittent, dev/test, cost aware
- **선택할 구성**: Aurora Serverless with bounded ACU
- **오답 함정**: 운영 고정 부하에 무조건 serverless가 저렴하다고 보면 안 된다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 데이터베이스 문제는 서비스 이름보다 **데이터 모델, 일관성, 지연시간, 확장 방식, 운영 책임** 단서를 먼저 읽어야 한다.

- Aurora Serverless는 Lambda 같은 함수 서비스가 아니라 Aurora DB 용량 자동 조정 구성이다.
- 최소/최대 ACU와 연결 수를 설계하지 않으면 scale이 되어도 병목이 남는다.
- 지원 기능은 Aurora Serverless v1/v2와 엔진 버전에 따라 다르다.

## 6. 암기 문장

- 관계형은 유지하고 용량만 자동 조정하면 Aurora Serverless다.
- 상시 고부하는 provisioned Aurora, 단순 키-값 초대규모는 DynamoDB와 비교한다.

## 참고 링크

- [Using Aurora Serverless v2](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html)
- [How Aurora Serverless v2 works](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html)
- [Choosing Aurora Serverless v2 capacity range](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.capacity.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
