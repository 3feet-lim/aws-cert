---
type: aws-service
service_name: "Amazon SageMaker AI"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["SageMaker", "SageMaker AI"]
tags: [aws, sap-c02, ml, model-training, mlops]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon SageMaker AI

> [!summary] 한 줄 요약
> 커스텀 ML 모델의 데이터 준비·학습·배포·MLOps를 관리형으로 수행하는 플랫폼이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | custom model training, model hosting, MLOps, notebooks |
| 대표 키워드 | SageMaker, SageMaker AI, ml, model-training, mlops |
| 자주 비교되는 서비스 | [[Amazon Rekognition]], [[Amazon Comprehend]], [[Amazon EMR]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Notebook/Studio, training jobs, endpoints, pipelines로 ML 수명주기를 관리한다.
- **왜 쓰는가?**: 자체 모델을 만들고 운영할 때 ML 인프라 부담을 줄인다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 이미 완성된 AI 기능은 Rekognition/Textract/Comprehend 같은 AI API가 더 단순하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Training/Hosting | 모델 학습과 endpoint 배포 | 커스텀 모델 |
| Pipelines | ML 워크플로 자동화 | MLOps |
| Feature/Model governance | 재사용/승인/모니터링 | 엔터프라이즈 운영 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon SageMaker AI`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Rekognition]] | 관리형 비전 API | 이미지/비디오 분석 | 커스텀 학습 플랫폼 아님 |
| [[Amazon Comprehend]] | 관리형 NLP API | 텍스트 분석 | 모델 운영 부담 없음 |
| [[Amazon EMR]] | 분산 처리 | 데이터 처리 프레임워크 | ML 플랫폼 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon SageMaker AI는 `커스텀 ML 플랫폼` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 이미 완성된 AI 기능은 Rekognition/Textract/Comprehend 같은 AI API가 더 단순하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon SageMaker AI`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| custom model training, model hosting, MLOps, notebooks | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon SageMaker AI]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `커스텀 ML 플랫폼`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 커스텀 ML 모델 수명주기는 SageMaker AI다.
- 미리 학습된 기능 API로 충분하면 SageMaker보다 AI managed service가 단순하다.

## 참고 링크

- [Amazon SageMaker AI 공식 문서](https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
