---
type: aws-service
service_name: "Amazon Fraud Detector"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Fraud Detector"]
tags: [aws, sap-c02, fraud, ml]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Fraud Detector

> [!summary] 한 줄 요약
> 온라인 사기 위험을 탐지하는 관리형 ML 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | fraud detection, risk score, rules |
| 대표 키워드 | Fraud Detector, fraud, ml |
| 자주 비교되는 서비스 | [[Amazon GuardDuty]], [[Amazon SageMaker AI]], [[Amazon Personalize]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 이벤트 데이터를 평가해 위험 점수와 결과를 반환한다.
- **왜 쓰는가?**: 결제/가입/계정 탈취 같은 사기 탐지에 사용한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 범용 이상 탐지나 보안 위협 탐지는 별도 서비스와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Detector/Model | 사기 탐지 모델 | 위험 평가 |
| Rules/outcomes | 점수 기반 의사결정 | 승인/검토/차단 |
| Real-time prediction | 실시간 이벤트 평가 | 거래 보호 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Fraud Detector`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon GuardDuty]] | AWS 계정/워크로드 위협 탐지 | 보안 탐지 | 비즈니스 사기 탐지 아님 |
| [[Amazon SageMaker AI]] | 커스텀 ML | 자체 fraud model | 운영 부담 |
| [[Amazon Personalize]] | 추천 | 개인화 | 사기 탐지 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Fraud Detector는 `사기 탐지 ML` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 범용 이상 탐지나 보안 위협 탐지는 별도 서비스와 구분한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Fraud Detector`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| fraud detection, risk score, rules | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Fraud Detector]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `사기 탐지 ML`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 온라인 사기 위험 평가는 Fraud Detector다.
- AWS 보안 위협 탐지와 비즈니스 사기 탐지는 구분한다.

## 참고 링크

- [Amazon Fraud Detector 공식 문서](https://docs.aws.amazon.com/frauddetector/latest/ug/what-is-frauddetector.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
