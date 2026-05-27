---
type: aws-service
service_name: "AWS IoT Device Management"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT Device Management"]
tags: [aws, sap-c02, iot, device-management]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT Device Management

> [!summary] 한 줄 요약
> 대규모 IoT 디바이스 fleet의 온보딩, 구성, 작업 배포, 인덱싱을 관리한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | fleet management, onboarding, jobs, indexing |
| 대표 키워드 | IoT Device Management, iot, device-management |
| 자주 비교되는 서비스 | [[AWS IoT Core]], [[AWS IoT Device Defender]], [[AWS Systems Manager]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 디바이스 등록, thing group, jobs, fleet indexing을 제공한다.
- **왜 쓰는가?**: 수천~수백만 디바이스의 운영 관리를 자동화한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 메시지 처리 자체는 IoT Core, 보안 감사는 Device Defender다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Fleet indexing | 디바이스 검색/상태 조회 | 운영 가시성 |
| Jobs | 원격 업데이트/작업 실행 | 대규모 배포 |
| Thing groups | 그룹별 정책/작업 | fleet 조직화 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT Device Management`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IoT Core]] | 연결/메시징 | MQTT/Rules | fleet 운영 기능과 역할 구분 |
| [[AWS IoT Device Defender]] | 보안 감사/이상 탐지 | 보안 운영 | 일반 fleet 작업 관리 아님 |
| [[AWS Systems Manager]] | 서버/엣지 운영 | EC2/하이브리드 관리 | IoT thing 모델과 다름 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT Device Management는 `IoT fleet 운영` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 메시지 처리 자체는 IoT Core, 보안 감사는 Device Defender다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT Device Management`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| fleet management, onboarding, jobs, indexing | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT Device Management]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `IoT fleet 운영`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 대규모 디바이스 fleet 운영은 IoT Device Management다.
- 연결은 IoT Core, 보안은 Device Defender와 나눈다.

## 참고 링크

- [AWS IoT Device Management 공식 문서](https://docs.aws.amazon.com/iot/latest/developerguide/iot-device-management.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
