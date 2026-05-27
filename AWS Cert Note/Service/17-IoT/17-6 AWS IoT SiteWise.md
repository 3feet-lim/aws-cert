---
type: aws-service
service_name: "AWS IoT SiteWise"
category: "IoT"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["IoT SiteWise"]
tags: [aws, sap-c02, iot, industrial]
created: 2026-05-27
updated: 2026-05-27
---

# AWS IoT SiteWise

> [!summary] 한 줄 요약
> 산업 설비 데이터를 수집·모델링·모니터링하는 관리형 industrial IoT 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | industrial IoT, asset model, time series |
| 대표 키워드 | IoT SiteWise, iot, industrial |
| 자주 비교되는 서비스 | [[AWS IoT Core]], [[Amazon Timestream]], [[Amazon Kinesis Data Streams]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 설비/자산 모델, 게이트웨이, 시계열 측정값, 포털을 제공한다.
- **왜 쓰는가?**: 공장/설비 운영 데이터를 AWS에서 구조화하고 분석한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 일반 MQTT 메시징 허브는 IoT Core다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Asset model | 장비/계층 모델링 | 산업 데이터 구조 |
| Gateway/data streams | 현장 데이터 수집 | OT 통합 |
| Monitor/portal | 운영 대시보드 | 설비 가시성 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-iot-selection-map.png]]

이 그림은 17. IoT 영역에서 `AWS IoT SiteWise`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IoT Core]] | IoT 연결/메시징 | 범용 디바이스 허브 | 산업 자산 모델링 전용 아님 |
| [[Amazon Timestream]] | 시계열 DB | 시계열 저장/쿼리 | 산업 설비 모델/포털은 SiteWise |
| [[Amazon Kinesis Data Streams]] | 스트림 처리 | 실시간 수집 | 산업 자산 관리 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS IoT SiteWise는 `산업 IoT 데이터 모델링` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 일반 MQTT 메시징 허브는 IoT Core다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS IoT SiteWise`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| industrial IoT, asset model, time series | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS IoT SiteWise]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `산업 IoT 데이터 모델링`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 산업 설비/자산 모델링은 IoT SiteWise다.
- 범용 디바이스 메시징은 IoT Core로 구분한다.

## 참고 링크

- [AWS IoT SiteWise 공식 문서](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/what-is-sitewise.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
