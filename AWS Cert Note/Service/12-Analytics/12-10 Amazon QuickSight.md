---
type: aws-service
service_name: "Amazon QuickSight"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["QuickSight"]
tags: [aws, sap-c02, bi, dashboard, analytics]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon QuickSight

> [!summary] 한 줄 요약
> AWS의 서버리스 BI 서비스로 대시보드와 임베디드 분석을 제공한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | BI dashboard, SPICE, embedded analytics |
| 대표 키워드 | QuickSight, bi, dashboard, analytics |
| 자주 비교되는 서비스 | [[Amazon Athena]], [[Amazon OpenSearch Service]], [[Amazon Redshift]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 여러 데이터 소스를 연결해 대시보드·리포트·분석을 제공한다.
- **왜 쓰는가?**: 운영 부담 적은 BI와 공유 대시보드가 필요할 때 쓴다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 데이터 변환/저장 엔진 자체가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| SPICE | 인메모리 엔진 | 성능/비용 |
| Dashboards | 대화형 리포트 | 경영/운영 BI |
| Embedded analytics | 앱 내 분석 임베드 | SaaS/포털 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `Amazon QuickSight`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Athena]] | SQL 쿼리 | 데이터 조회 | 시각화 도구 아님 |
| [[Amazon OpenSearch Service]] | 검색/로그 분석 | 전문 검색 | BI 도구 아님 |
| [[Amazon Redshift]] | 웨어하우스 | 분석 저장/쿼리 | 대시보드만은 QuickSight |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon QuickSight는 `서버리스 BI` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 데이터 변환/저장 엔진 자체가 아니다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon QuickSight`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| BI dashboard, SPICE, embedded analytics | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon QuickSight]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `서버리스 BI`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 대시보드와 BI는 QuickSight, 쿼리 엔진은 Athena/Redshift로 구분한다.
- QuickSight는 데이터 소스를 시각화하는 서비스다.

## 참고 링크

- [Amazon QuickSight 공식 문서](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
