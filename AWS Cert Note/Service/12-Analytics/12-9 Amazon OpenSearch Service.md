---
type: aws-service
service_name: "Amazon OpenSearch Service"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["OpenSearch", "Elasticsearch Service"]
tags: [aws, sap-c02, search, log-analytics, observability]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon OpenSearch Service

> [!summary] 한 줄 요약
> 검색·로그 분석·시각화를 위한 OpenSearch 클러스터를 관리형으로 제공한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | full-text search, log analytics, observability, dashboards |
| 대표 키워드 | OpenSearch, Elasticsearch Service, search, log-analytics, observability |
| 자주 비교되는 서비스 | [[Amazon CloudWatch]], [[Amazon QuickSight]], [[Amazon Athena]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: OpenSearch 도메인/서버리스 컬렉션으로 검색과 분석을 제공한다.
- **왜 쓰는가?**: 전문 검색, 로그 분석, 대시보드가 필요할 때 쓴다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 정형 SQL BI에는 Redshift/QuickSight가 더 적합할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Full-text search | 역색인 기반 검색 | 검색 애플리케이션 |
| Log analytics | CloudWatch/Firehose 연동 | 운영 분석 |
| Dashboards | 시각화 | 관측성 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon OpenSearch Service`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon CloudWatch]] | 메트릭/로그 기본 관측 | AWS 운영 모니터링 | 전문 검색 엔진과 다름 |
| [[Amazon QuickSight]] | BI 대시보드 | 비즈니스 분석 | 검색 엔진 아님 |
| [[Amazon Athena]] | S3 SQL 조회 | ad-hoc 분석 | 검색/인덱싱과 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon OpenSearch Service는 `관리형 검색/로그 분석` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 정형 SQL BI에는 Redshift/QuickSight가 더 적합할 수 있다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon OpenSearch Service`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| full-text search, log analytics, observability, dashboards | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon OpenSearch Service]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 검색/로그 분석`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 검색/로그 분석/관측성 색인이 필요하면 OpenSearch다.
- BI 리포팅 도구나 데이터 웨어하우스와 혼동하지 않는다.

## 참고 링크

- [Amazon OpenSearch Service 공식 문서](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
