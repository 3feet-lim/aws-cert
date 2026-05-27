---
type: aws-service
service_name: "AWS IoT Things Graph"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT Things Graph"]
tags: [aws, sap-c02, iot, legacy]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT Things Graph

> [!summary] 한 줄 요약
> IoT 디바이스와 웹 서비스를 시각적 워크플로로 연결하던 레거시 서비스이며, 최신 설계에서는 사용 가능 여부를 확인해야 한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | legacy IoT workflow modeling, visual orchestration |
| 대표 키워드 | IoT Things Graph, iot, legacy |
| 자주 비교되는 서비스 | [[AWS Step Functions]], [[AWS IoT Core]], [[Amazon EventBridge]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 디바이스/서비스 상호작용을 모델링하는 서비스로 소개되었다.
- **왜 쓰는가?**: 시험 범위 목록에 남아 있더라도 최신 아키텍처에서는 대체 패턴을 고려한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: AWS 서비스 지원 상태가 변경된 레거시 항목이므로 최신 공식 문서를 반드시 확인한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Visual flow | 디바이스/서비스 흐름 모델링 | 개념 이해 |
| Legacy status | 지원 상태 확인 필요 | 최신 설계 주의 |
| Alternatives | IoT Core Rules/Lambda/Step Functions | 대체 설계 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT Things Graph`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Step Functions]] | 워크플로 오케스트레이션 | 상태 머신 | IoT 특화 모델링과 다름 |
| [[AWS IoT Core]] | Rules Engine | 메시지 라우팅 | 일반 대체 패턴 |
| [[Amazon EventBridge]] | 이벤트 라우팅 | 이벤트 기반 통합 | 시각적 IoT 모델링 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT Things Graph는 `IoT 워크플로 모델링(레거시)` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- AWS 서비스 지원 상태가 변경된 레거시 항목이므로 최신 공식 문서를 반드시 확인한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT Things Graph`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| legacy IoT workflow modeling, visual orchestration | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT Things Graph]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `IoT 워크플로 모델링(레거시)`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- Things Graph는 레거시/지원 상태 확인이 필요한 IoT 워크플로 서비스로 암기한다.
- 최신 설계 정답은 IoT Core Rules, Lambda, Step Functions 등 대체 구성을 검토한다.

## 참고 링크

- [AWS IoT Things Graph 공식 문서](https://docs.aws.amazon.com/thingsgraph/latest/ug/iot-tg-whatis.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
