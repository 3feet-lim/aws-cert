---
type: aws-service
service_name: "AWS IoT Device Defender"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT Device Defender"]
tags: [aws, sap-c02, iot, security]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT Device Defender

> [!summary] 한 줄 요약
> IoT 디바이스와 계정 설정을 감사하고 비정상 동작을 탐지하는 IoT 보안 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | IoT security audit, detect, alerts |
| 대표 키워드 | IoT Device Defender, iot, security |
| 자주 비교되는 서비스 | [[Amazon GuardDuty]], [[AWS IoT Device Management]], [[AWS Security Hub]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 보안 모범 사례 감사와 디바이스 행동 지표 기반 탐지를 제공한다.
- **왜 쓰는가?**: 디바이스 fleet 보안 상태와 이상 통신을 관리한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 일반 AWS 계정 위협 탐지는 GuardDuty와 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Audit | 정책/인증서/설정 검사 | 보안 구성 |
| Detect | 행동 지표 이상 탐지 | 위협 탐지 |
| Alerts/actions | SNS/CloudWatch/IoT Jobs 연동 | 대응 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT Device Defender`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon GuardDuty]] | AWS 계정/워크로드 위협 탐지 | VPC/DNS/CloudTrail 기반 | IoT 디바이스 보안 특화 아님 |
| [[AWS IoT Device Management]] | fleet 운영 | 작업/인덱싱 | 보안 감사 아님 |
| [[AWS Security Hub]] | 보안 결과 집계 | 중앙 대시보드 | IoT 행동 탐지 자체 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT Device Defender는 `IoT 보안 감사/탐지` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 일반 AWS 계정 위협 탐지는 GuardDuty와 구분한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT Device Defender`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| IoT security audit, detect, alerts | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT Device Defender]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `IoT 보안 감사/탐지`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- IoT 디바이스 보안 감사와 이상 탐지는 Device Defender다.
- AWS 계정 위협 탐지 GuardDuty와 범위를 구분한다.

## 참고 링크

- [AWS IoT Device Defender 공식 문서](https://docs.aws.amazon.com/iot-device-defender/latest/devguide/what-is-dd.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
