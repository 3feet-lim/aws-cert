---
type: aws-service
service_name: "Amazon Comprehend"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Comprehend"]
tags: [aws, sap-c02, nlp, ml]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Comprehend

> [!summary] 한 줄 요약
> 텍스트에서 감정·엔터티·키프레이즈·언어 등을 추출하는 관리형 NLP 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | NLP, sentiment, entities, key phrases |
| 대표 키워드 | Comprehend, nlp, ml |
| 자주 비교되는 서비스 | [[Amazon Translate]], [[Amazon Kendra]], [[Amazon Textract]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 텍스트 입력을 분석해 의미 정보와 분류 결과를 제공한다.
- **왜 쓰는가?**: 문서/전사/고객 피드백 분석을 모델 운영 없이 수행한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 번역은 Translate, 검색은 Kendra다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Entity/Sentiment | 엔터티/감정 분석 | 고객 피드백 |
| Key phrases | 핵심어 추출 | 문서 요약 보조 |
| Custom classification | 사용자 지정 분류 | 도메인 텍스트 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Comprehend`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Translate]] | 언어 번역 | 다국어 변환 | NLP 분석 아님 |
| [[Amazon Kendra]] | 엔터프라이즈 검색 | 질의응답/검색 | 텍스트 분석 API 아님 |
| [[Amazon Textract]] | 문서 OCR | 텍스트 추출 | 추출 후 분석은 Comprehend |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Comprehend는 `관리형 NLP API` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 번역은 Translate, 검색은 Kendra다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Comprehend`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| NLP, sentiment, entities, key phrases | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Comprehend]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 NLP API`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 텍스트 의미 분석은 Comprehend다.
- 번역은 Translate, 검색은 Kendra로 구분한다.

## 참고 링크

- [Amazon Comprehend 공식 문서](https://docs.aws.amazon.com/comprehend/latest/dg/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
