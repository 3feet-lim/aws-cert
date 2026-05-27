---
type: aws-service
service_name: "Amazon Textract"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Textract"]
tags: [aws, sap-c02, ml, ocr, document-ai]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Textract

> [!summary] 한 줄 요약
> 문서 이미지에서 텍스트뿐 아니라 양식과 표 구조를 추출하는 관리형 문서 분석 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | OCR, forms, tables, document extraction |
| 대표 키워드 | Textract, ml, ocr, document-ai |
| 자주 비교되는 서비스 | [[Amazon Rekognition]], [[Amazon Comprehend]], [[Amazon SageMaker AI]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 스캔 문서/PDF에서 key-value, tables, text를 추출한다.
- **왜 쓰는가?**: 문서 자동화와 데이터 입력 자동화에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 단순 이미지 객체 인식은 Rekognition이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Text extraction | 문자 추출 | OCR |
| Forms/Tables | Key-value/표 구조 | 업무 문서 자동화 |
| Async analysis | 대용량 문서 처리 | 배치 처리 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Textract`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Rekognition]] | 이미지/비디오 분석 | 객체/얼굴/콘텐츠 | 문서 표/양식 추출에는 부적합 |
| [[Amazon Comprehend]] | 텍스트 의미 분석 | 감정/엔터티 | OCR 자체가 아님 |
| [[Amazon SageMaker AI]] | 커스텀 모델 | 특수 문서 모델 | 기본 OCR에는 과함 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Textract는 `문서 OCR/구조 추출` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 단순 이미지 객체 인식은 Rekognition이다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Textract`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| OCR, forms, tables, document extraction | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Textract]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `문서 OCR/구조 추출`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 문서에서 텍스트·표·양식을 뽑으면 Textract다.
- 추출 후 의미 분석은 Comprehend와 조합할 수 있다.

## 참고 링크

- [Amazon Textract 공식 문서](https://docs.aws.amazon.com/textract/latest/dg/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
