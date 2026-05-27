---
type: aws-service
service_name: "AWS Lake Formation"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Lake Formation"]
tags: [aws, sap-c02, data-lake, governance, security]
created: 2026-05-27
updated: 2026-05-27
---

# AWS Lake Formation

> [!summary] 한 줄 요약
> S3 데이터 레이크의 세밀한 접근 제어와 거버넌스를 중앙화한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | 데이터 레이크 권한, cross-account sharing, column/row-level control |
| 대표 키워드 | Lake Formation, data-lake, governance, security |
| 자주 비교되는 서비스 | [[AWS Glue]], [[AWS IAM]], [[Amazon S3]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Data Catalog 기반으로 테이블/컬럼/행 수준 권한을 관리한다.
- **왜 쓰는가?**: 데이터 레이크 구축과 보안 통제를 단순화한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 기본 저장소는 주로 S3이며 분석 엔진 자체가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| LF permissions | 테이블/컬럼/행 권한 | 세밀한 접근 제어 |
| Data lake locations | S3 위치 등록 | 권한 위임 |
| Cross-account sharing | 계정 간 데이터 공유 | 조직 거버넌스 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `AWS Lake Formation`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Glue]] | 카탈로그/ETL | 데이터 변환·메타데이터 | 권한 거버넌스 중심 아님 |
| [[AWS IAM]] | 일반 AWS 권한 | AWS API 권한 | 데이터 레이크 세밀 권한은 LF와 조합 |
| [[Amazon S3]] | 객체 저장소 | 저장 계층 | 거버넌스 기능만으로는 부족 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS Lake Formation는 `데이터 레이크 거버넌스` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 기본 저장소는 주로 S3이며 분석 엔진 자체가 아니다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS Lake Formation`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| 데이터 레이크 권한, cross-account sharing, column/row-level control | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS Lake Formation]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `데이터 레이크 거버넌스`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- S3 데이터 레이크에 세밀한 테이블/컬럼/행 권한이 나오면 Lake Formation을 떠올린다.
- Lake Formation은 저장소나 BI 도구가 아니라 데이터 레이크 거버넌스 계층이다.

## 참고 링크

- [AWS Lake Formation 공식 문서](https://docs.aws.amazon.com/lake-formation/latest/dg/what-is-lake-formation.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
