---
type: aws-service
service_name: "Amazon Kendra"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Kendra"]
tags: [aws, sap-c02, enterprise-search, ml]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Kendra

> [!summary] 한 줄 요약
> 기업 문서와 지식 베이스에 대한 ML 기반 의미 검색을 제공한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | enterprise search, semantic search, connectors |
| 대표 키워드 | Kendra, enterprise-search, ml |
| 자주 비교되는 서비스 | [[Amazon OpenSearch Service]], [[Amazon Comprehend]], [[Amazon Lex]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 커넥터로 문서를 인덱싱하고 자연어 질의에 답한다.
- **왜 쓰는가?**: 사내 문서 검색/FAQ/지식 검색에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 로그 전문 검색은 OpenSearch와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Connectors | S3/SharePoint 등 소스 연결 | 문서 인덱싱 |
| Natural language query | 의미 기반 검색 | 사용자 검색 경험 |
| Relevance tuning | 관련도 조정 | 검색 품질 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Kendra`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon OpenSearch Service]] | 검색/로그 분석 엔진 | 커스텀 검색/관측성 | ML 기반 엔터프라이즈 검색과 다름 |
| [[Amazon Comprehend]] | 텍스트 분석 | 엔터티/감정 | 검색 서비스 아님 |
| [[Amazon Lex]] | 챗봇 | 대화 UI | 지식 검색 소스와 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Kendra는 `엔터프라이즈 검색` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 로그 전문 검색은 OpenSearch와 구분한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Kendra`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| enterprise search, semantic search, connectors | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Kendra]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `엔터프라이즈 검색`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 기업 문서 의미 검색은 Kendra다.
- 로그/전문 검색 엔진은 OpenSearch와 비교한다.

## 참고 링크

- [Amazon Kendra 공식 문서](https://docs.aws.amazon.com/kendra/latest/dg/what-is-kendra.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
