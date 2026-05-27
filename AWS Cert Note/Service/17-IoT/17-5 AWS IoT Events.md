---
type: aws-service
service_name: "AWS IoT Events"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT Events"]
tags: [aws, sap-c02, iot, events, legacy]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT Events

> [!summary] 한 줄 요약
> IoT 이벤트 패턴을 감지해 상태 기반 알림/작업을 실행하던 서비스이며, 현재는 신규 설계에서 대체 서비스를 검토해야 한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | event detection, state machine, end-of-support awareness |
| 대표 키워드 | IoT Events, iot, events, legacy |
| 자주 비교되는 서비스 | [[Amazon EventBridge]], [[AWS IoT Core]], [[AWS Lambda]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 디바이스 데이터 조건을 감지하고 상태 전환에 따라 작업을 실행하는 모델이었다.
- **왜 쓰는가?**: 시험에서는 IoT 이벤트 감지/알람의 역사적 서비스로 나올 수 있다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: AWS 공지 기준 2026-05-20 지원 종료가 안내되어 최신 설계 정답으로는 주의한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Detector model | 상태/조건 기반 이벤트 감지 | 이벤트 패턴 |
| Inputs/actions | IoT 데이터 입력과 액션 | 알림/대응 |
| Legacy awareness | 지원 종료 안내 | 최신 설계 주의 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT Events`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EventBridge]] | 범용 이벤트 버스 | AWS/SaaS 이벤트 라우팅 | IoT 상태 감지 전용 아님 |
| [[AWS IoT Core]] | Rules Engine | 메시지 라우팅 | 상태 모델링과 다름 |
| [[AWS Lambda]] | 서버리스 처리 | 커스텀 로직 | 직접 구현 필요 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT Events는 `IoT 이벤트 감지(레거시 주의)` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- AWS 공지 기준 2026-05-20 지원 종료가 안내되어 최신 설계 정답으로는 주의한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT Events`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| event detection, state machine, end-of-support awareness | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT Events]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `IoT 이벤트 감지(레거시 주의)`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- IoT Events는 상태 기반 IoT 이벤트 감지 서비스였지만 최신 설계에서는 지원 종료 여부를 확인한다.
- 새 설계 문제는 IoT Core Rules, EventBridge, Lambda 등 대안을 검토한다.

## 참고 링크

- [AWS IoT Events 공식 문서](https://docs.aws.amazon.com/iotevents/latest/developerguide/what-is-iotevents.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
