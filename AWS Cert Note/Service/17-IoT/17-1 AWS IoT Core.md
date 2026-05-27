---
type: aws-service
service_name: "AWS IoT Core"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["IoT Core"]
tags: [aws, sap-c02, iot, mqtt]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT Core

> [!summary] 한 줄 요약
> 디바이스를 AWS에 안전하게 연결하고 MQTT 메시징·Rules Engine으로 AWS 서비스와 연동하는 IoT 허브다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | device connectivity, MQTT, Rules Engine, Device Shadow |
| 대표 키워드 | IoT Core, iot, mqtt |
| 자주 비교되는 서비스 | [[AWS IoT Greengrass]], [[Amazon Kinesis Data Streams]], [[Amazon SNS]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 디바이스 게이트웨이, 메시지 브로커, 인증서 기반 인증, Rules Engine을 제공한다.
- **왜 쓰는가?**: 대규모 디바이스 연결과 이벤트 라우팅을 관리형으로 처리한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 로컬 엣지 처리·오프라인 실행은 Greengrass가 담당한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| MQTT broker | 디바이스 pub/sub 메시징 | 대규모 연결 |
| Rules Engine | 메시지를 Lambda/Kinesis/S3 등으로 라우팅 | 서비스 통합 |
| Device Shadow | 디바이스 상태 동기화 | 간헐 연결 대응 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT Core`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IoT Greengrass]] | 엣지 런타임 | 로컬 처리/오프라인 | 클라우드 메시징 허브와 다름 |
| [[Amazon Kinesis Data Streams]] | 스트림 수집 | 실시간 데이터 파이프라인 | 디바이스 인증/관리 없음 |
| [[Amazon SNS]] | pub/sub 알림 | 앱 메시징 | IoT 프로토콜/섀도우 없음 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT Core는 `IoT 연결/메시징 허브` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 로컬 엣지 처리·오프라인 실행은 Greengrass가 담당한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT Core`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| device connectivity, MQTT, Rules Engine, Device Shadow | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT Core]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `IoT 연결/메시징 허브`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- IoT 디바이스 연결과 MQTT 메시징은 IoT Core다.
- 클라우드 연결 허브와 엣지 로컬 처리(Greengrass)를 구분한다.

## 참고 링크

- [AWS IoT Core 공식 문서](https://docs.aws.amazon.com/iot/latest/developerguide/what-is-aws-iot.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
