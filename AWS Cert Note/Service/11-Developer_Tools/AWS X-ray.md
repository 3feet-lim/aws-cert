---
title: AWS X-Ray
category: 11. Developer Tools
service: AWS X-Ray
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - observability
  - tracing
  - x-ray
---

# AWS X-Ray

> [!summary]
> **AWS X-Ray**는 마이크로서비스와 서버리스 애플리케이션의 요청 흐름을 추적해 지연 시간, 오류 위치, 서비스 간 의존성을 분석하는 **분산 추적(distributed tracing)** 서비스다. 신규 계측 설계에서는 X-Ray SDK/daemon 수명주기와 OpenTelemetry/AWS Distro for OpenTelemetry(ADOT) 방향을 함께 확인해야 한다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| 분산 추적 | 요청이 여러 서비스/API/Lambda/ECS를 통과할 때 end-to-end trace가 필요하면 X-Ray |
| Service map | 서비스 간 호출 관계, 지연 시간, 오류 위치 시각화 |
| Trace 구조 | Trace, segment, subsegment, annotation, metadata 구분 |
| Sampling | 모든 요청이 아니라 규칙 기반 샘플링으로 비용과 오버헤드 제어 |
| CloudWatch와 구분 | 로그/메트릭은 CloudWatch, 요청 경로 추적은 X-Ray |

## 1. 핵심 개념

- **Trace**: 하나의 요청이 시스템 전체를 통과한 end-to-end 기록.
- **Segment**: 개별 서비스 또는 리소스가 처리한 작업 단위.
- **Subsegment**: downstream 호출, SQL query, 외부 API 호출 같은 세부 작업.
- **Service map**: trace 데이터를 기반으로 생성되는 서비스 의존성 그래프.
- **Sampling rule**: 수집할 요청 비율과 조건을 제어한다.
- **Annotation / Metadata**: 검색 가능한 key-value 또는 상세 진단 정보를 trace에 추가한다.

## 2. 주요 기능과 시험 포인트

### 분산 추적

API Gateway, Lambda, ECS, EC2 애플리케이션 등에서 요청 경로를 추적해 “어느 서비스에서 latency가 증가했는지”, “어떤 downstream 호출이 오류를 유발했는지”를 확인한다.

### Root cause 분석

X-Ray는 trace timeline과 service map을 통해 병목 지점, throttle, 오류 응답, cold start 영향 등을 분석하는 데 도움을 준다. 시험에서는 CloudWatch Logs만으로는 요청 경로 전체를 연결하기 어렵다는 점이 포인트다.

### OpenTelemetry / ADOT 고려

AWS는 X-Ray trace 데이터를 계속 활용할 수 있지만, 신규 계측은 OpenTelemetry 표준 및 ADOT 사용을 검토하는 것이 안전하다. 특히 X-Ray SDK와 daemon 관련 지원 종료 일정은 아키텍처 결정 시 공식 문서를 확인해야 한다.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| 요청 경로와 지연 원인 추적 | X-Ray | Trace/service map/segment 분석 |
| 로그 검색/보관 | CloudWatch Logs | 애플리케이션 로그 저장과 검색 |
| 지표와 알람 | CloudWatch Metrics/Alarms | CPU, latency, error count 등 모니터링 |
| 표준 기반 계측 | OpenTelemetry / ADOT | 벤더 중립 계측과 collector 기반 수집 |
| 코드 성능 hotspot | CodeGuru Profiler | 런타임 CPU/latency/cost 분석 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-developer-tools-supporting-services.png]]

1. 사용자의 요청이 ALB, API Gateway, Lambda, ECS, EC2 애플리케이션을 통과한다.
2. 애플리케이션 계측 SDK 또는 OpenTelemetry collector가 trace 데이터를 생성한다.
3. X-Ray가 segment/subsegment를 수집한다.
4. Service map과 trace timeline에서 latency, error, downstream dependency를 분석한다.
5. CloudWatch Logs/Metrics와 함께 원인 분석과 alarm 기반 대응을 설계한다.

## 5. SAP-C02 시나리오 패턴

- “마이크로서비스 호출 체인에서 병목 서비스를 찾아야 한다” → X-Ray.
- “Lambda/API Gateway 기반 서버리스 앱에서 요청별 latency를 분석해야 한다” → X-Ray + CloudWatch.
- “로그를 장기간 검색하고 metric alarm을 만들어야 한다” → CloudWatch가 중심, X-Ray는 trace 중심.
- “신규 계측 표준화와 장기 호환성이 중요하다” → OpenTelemetry/ADOT 고려 후 X-Ray로 내보내기.

## 6. 헷갈리는 포인트

- X-Ray는 로그 저장소가 아니다. 로그 검색과 보관은 CloudWatch Logs를 사용한다.
- X-Ray는 모든 요청을 무조건 수집하는 도구가 아니라 sampling rule을 통해 제어한다.
- X-Ray SDK/daemon의 lifecycle은 별도 확인이 필요하며, 새 설계에서는 OpenTelemetry/ADOT가 더 적합할 수 있다.

## 7. 암기 문장

> **CloudWatch는 로그/메트릭, X-Ray는 요청 흐름과 병목 지점 추적.**

## 8. 참고 링크

- [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)
- [X-Ray SDKs and daemon support timeline](https://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-daemon-timeline.html)
- [AWS Distro for OpenTelemetry](https://aws-otel.github.io/)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
