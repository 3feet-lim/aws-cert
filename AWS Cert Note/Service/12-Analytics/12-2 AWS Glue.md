---
type: aws-service
service_name: "AWS Glue"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Glue", "Data Catalog", "Glue ETL"]
tags: [aws, sap-c02, etl, data-catalog, serverless]
created: 2026-05-27
updated: 2026-05-27
---

# AWS Glue

> [!summary] 한 줄 요약
> 데이터 카탈로그와 서버리스 ETL로 데이터 레이크의 수집·변환·스키마 관리를 담당한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | ETL, schema discovery, crawler, Data Catalog, 서버리스 Spark |
| 대표 키워드 | Glue, Data Catalog, etl, data-catalog, serverless |
| 자주 비교되는 서비스 | [[Amazon Athena]], [[AWS Lake Formation]], [[Amazon EMR]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Crawler, Data Catalog, Glue jobs로 데이터 처리 파이프라인을 구성한다.
- **왜 쓰는가?**: ETL 서버와 Spark 클러스터 운영 부담을 줄인다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 작업 시작 지연과 비용 모델을 고려해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Data Catalog | 테이블/스키마/파티션 메타데이터 | Athena/EMR/Redshift Spectrum과 연계 |
| Crawler | 데이터 구조 자동 탐지 | 스키마 발견 |
| Glue Job | Spark/Ray/Python 기반 ETL | 서버리스 변환 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `AWS Glue`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Athena]] | SQL 쿼리 엔진 | 조회 중심 | ETL 서비스가 아님 |
| [[AWS Lake Formation]] | 권한/거버넌스 | 세밀한 데이터 접근 통제 | ETL 엔진이 아님 |
| [[Amazon EMR]] | 관리형 클러스터 | 커스텀 빅데이터 프레임워크 | 운영 부담 증가 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS Glue는 `서버리스 ETL/Data Catalog` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 작업 시작 지연과 비용 모델을 고려해야 한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS Glue`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| ETL, schema discovery, crawler, Data Catalog, 서버리스 Spark | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS Glue]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `서버리스 ETL/Data Catalog`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- ETL과 Catalog는 Glue, 데이터 레이크 권한 거버넌스는 Lake Formation으로 구분한다.
- Glue Data Catalog는 여러 분석 서비스의 공통 메타스토어로 자주 등장한다.

## 참고 링크

- [AWS Glue 공식 문서](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
