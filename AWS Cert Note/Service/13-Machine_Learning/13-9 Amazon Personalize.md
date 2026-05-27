---
type: aws-service
service_name: "Amazon Personalize"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Personalize"]
tags: [aws, sap-c02, recommendation, ml]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Personalize

> [!summary] 한 줄 요약
> 사용자 행동 데이터를 기반으로 개인화 추천을 제공하는 관리형 ML 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | recommendation, personalization, user behavior |
| 대표 키워드 | Personalize, recommendation, ml |
| 자주 비교되는 서비스 | [[Amazon Kendra]], [[Amazon SageMaker AI]], [[Amazon QuickSight]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 사용자·아이템·상호작용 데이터로 추천 모델을 생성한다.
- **왜 쓰는가?**: 이커머스/콘텐츠 추천을 빠르게 구현한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 일반 BI나 검색 서비스가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Recipes | 추천 알고리즘 유형 | 시나리오별 추천 |
| Campaign/Recommender | 추천 제공 endpoint | 앱 연동 |
| Event tracking | 행동 데이터 수집 | 모델 개선 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Personalize`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Kendra]] | 엔터프라이즈 검색 | 문서 검색 | 추천 엔진 아님 |
| [[Amazon SageMaker AI]] | 커스텀 ML | 자체 추천 모델 | 운영 부담 증가 |
| [[Amazon QuickSight]] | BI | 분석 대시보드 | 개인화 추천 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Personalize는 `추천 API` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 일반 BI나 검색 서비스가 아니다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Personalize`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| recommendation, personalization, user behavior | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Personalize]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `추천 API`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 개인화 추천은 Personalize다.
- 커스텀 추천 알고리즘이 필요하면 SageMaker를 고려한다.

## 참고 링크

- [Amazon Personalize 공식 문서](https://docs.aws.amazon.com/personalize/latest/dg/what-is-personalize.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
