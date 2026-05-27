---
type: aws-service
service_name: "Amazon EMR"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["EMR", "Elastic MapReduce"]
tags: [aws, sap-c02, big-data, spark, hadoop]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon EMR

> [!summary] 한 줄 요약
> Spark/Hadoop/Hive 등 빅데이터 프레임워크를 관리형 클러스터로 실행한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | 대규모 분산 처리, 커스텀 프레임워크, 비용/성능 튜닝 |
| 대표 키워드 | EMR, Elastic MapReduce, big-data, spark, hadoop |
| 자주 비교되는 서비스 | [[Amazon Athena]], [[AWS Glue]], [[Amazon Redshift]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: EC2/EKS/Serverless 옵션으로 Spark·Hadoop 생태계를 실행한다.
- **왜 쓰는가?**: 복잡한 ETL/ML/분산 처리 워크로드를 유연하게 운영한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 간단한 SQL 조회만이면 Athena가 더 단순하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Spark/Hadoop | 분산 처리 프레임워크 | 대규모 배치 처리 |
| EMR on EKS/Serverless | 실행 모델 선택 | 운영 부담/격리/확장성 |
| Spot/Auto Scaling | 비용 최적화 | 장기 배치 작업 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon EMR`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Athena]] | 서버리스 SQL | S3 ad-hoc 쿼리 | EMR은 클러스터 운영 필요 |
| [[AWS Glue]] | 서버리스 ETL | 관리형 ETL | 커스텀 프레임워크는 EMR |
| [[Amazon Redshift]] | 웨어하우스 | BI/SQL 분석 | 범용 Spark 처리는 EMR |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon EMR는 `관리형 빅데이터 클러스터` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 간단한 SQL 조회만이면 Athena가 더 단순하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon EMR`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| 대규모 분산 처리, 커스텀 프레임워크, 비용/성능 튜닝 | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon EMR]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 빅데이터 클러스터`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 커스텀 Spark/Hadoop 빅데이터 처리면 EMR, S3 SQL 조회면 Athena다.
- EMR은 유연하지만 운영·튜닝 부담이 시험 함정이다.

## 참고 링크

- [Amazon EMR 공식 문서](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
