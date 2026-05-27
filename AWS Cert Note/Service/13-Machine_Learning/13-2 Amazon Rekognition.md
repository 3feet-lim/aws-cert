---
type: aws-service
service_name: "Amazon Rekognition"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Rekognition"]
tags: [aws, sap-c02, ml, vision]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Rekognition

> [!summary] 한 줄 요약
> 이미지와 비디오에서 객체·얼굴·텍스트·부적절 콘텐츠 등을 분석하는 관리형 비전 API다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | image/video analysis, face/object detection, moderation |
| 대표 키워드 | Rekognition, ml, vision |
| 자주 비교되는 서비스 | [[Amazon Textract]], [[Amazon SageMaker AI]], [[Amazon Comprehend]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: API 호출로 이미지/영상 분석 결과를 반환한다.
- **왜 쓰는가?**: 비전 모델 구축 없이 콘텐츠 분석을 수행한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 문서의 양식/표 추출은 Textract가 더 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Labels/Moderation | 객체/장면/콘텐츠 감지 | 이미지 분류 |
| Face analysis | 얼굴 비교/검색 | 주의 깊은 개인정보 요구 |
| Video analysis | 동영상 분석 | 미디어 처리 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Rekognition`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Textract]] | 문서 OCR/양식/표 | 문서 데이터 추출 | 일반 이미지 객체 분석과 다름 |
| [[Amazon SageMaker AI]] | 커스텀 모델 | 특수 모델 학습 | 관리형 API보다 운영 부담 |
| [[Amazon Comprehend]] | 텍스트 NLP | 텍스트 의미 분석 | 이미지 분석 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Rekognition는 `관리형 컴퓨터 비전 API` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 문서의 양식/표 추출은 Textract가 더 적합하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Rekognition`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| image/video analysis, face/object detection, moderation | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Rekognition]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 컴퓨터 비전 API`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 이미지·비디오 분석은 Rekognition, 문서 구조 추출은 Textract다.
- 관리형 AI API는 모델 학습/호스팅 부담을 줄인다.

## 참고 링크

- [Amazon Rekognition 공식 문서](https://docs.aws.amazon.com/rekognition/latest/dg/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
