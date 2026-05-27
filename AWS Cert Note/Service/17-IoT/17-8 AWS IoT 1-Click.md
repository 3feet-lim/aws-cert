---
type: aws-service
service_name: "AWS IoT 1-Click"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT 1-Click"]
tags: [aws, sap-c02, iot, legacy]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT 1-Click

> [!summary] 한 줄 요약
> 간단한 IoT 버튼/디바이스 클릭 이벤트로 Lambda 같은 작업을 실행하던 서비스이며 최신 사용 가능 여부를 확인해야 한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | simple device trigger, one-click actions, legacy awareness |
| 대표 키워드 | IoT 1-Click, iot, legacy |
| 자주 비교되는 서비스 | [[AWS IoT Core]], [[AWS Lambda]], [[Amazon EventBridge]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 사전 등록된 간단 디바이스의 클릭 이벤트를 액션으로 연결한다.
- **왜 쓰는가?**: 복잡한 디바이스 플랫폼 없이 단순 트리거를 빠르게 구성하는 용도였다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 최신 서비스 상태 변화가 있으므로 신규 설계에서는 대체 서비스를 검토한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Simple trigger | 버튼/단순 디바이스 이벤트 | 간단 자동화 |
| Actions | Lambda/SNS 등 액션 | 이벤트 처리 |
| Legacy awareness | 서비스 상태 확인 | 최신 설계 주의 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT 1-Click`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IoT Core]] | 범용 IoT 연결 | MQTT/Rules | 복잡한 디바이스 플랫폼 |
| [[AWS Lambda]] | 이벤트 처리 | 서버리스 액션 | 디바이스 관리 아님 |
| [[Amazon EventBridge]] | 이벤트 라우팅 | 범용 이벤트 버스 | 디바이스 등록 기능 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT 1-Click는 `간단 IoT 트리거(레거시 주의)` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 최신 서비스 상태 변화가 있으므로 신규 설계에서는 대체 서비스를 검토한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT 1-Click`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| simple device trigger, one-click actions, legacy awareness | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT 1-Click]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `간단 IoT 트리거(레거시 주의)`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 단순 IoT 버튼 트리거는 IoT 1-Click로 출제될 수 있지만 최신 설계에서는 서비스 상태를 확인한다.
- 범용 IoT는 IoT Core가 기본이다.

## 참고 링크

- [AWS IoT 1-Click 공식 문서](https://docs.aws.amazon.com/iot-1-click/latest/developerguide/what-is-1click.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
