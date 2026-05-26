---
type: aws-service
service_name: "AWS Proton"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Proton", "AWS Proton templates"]
tags: [aws, sap-c02, platform-engineering, deployment]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Proton

> [!summary] 한 줄 요약
> 플랫폼 팀이 환경/서비스 템플릿을 정의하고 개발자가 표준화된 방식으로 컨테이너·서버리스 애플리케이션을 배포하게 하는 서비스다.

> [!warning] 수명주기 주의
> AWS는 AWS Proton 지원 종료를 2026-10-07로 공지했다. 신규 설계 문제에서는 CloudFormation, Service Catalog, CodePipeline, CDK 등 대안을 함께 검토한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 플랫폼 팀 표준 템플릿, 서비스 배포 자동화, 환경/서비스 분리, 수명주기 리스크 |
| 핵심 의사결정 | 기존 Proton 환경을 이해하거나 템플릿 기반 앱 배포 개념을 구분할 때 출제될 수 있음 |
| 대표 키워드 | environment template, service template, pipeline, platform team, EOL |
| 자주 비교되는 서비스 | [[AWS CloudFormation]], [[AWS Service Catalog]], [[AWS CodePipeline]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 플랫폼 팀이 인프라/배포 템플릿을 만들고 개발팀이 이를 사용해 서비스를 배포하는 관리형 워크플로우.
- **왜 쓰는가?**: 네트워크/보안/CI-CD 표준을 반복 적용하고 개발자의 배포 경험을 단순화한다.
- **핵심 제약**: 2026-10-07 지원 종료 예정이므로 신규 장기 아키텍처의 기본 선택지로는 주의한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Environment template | 계정/네트워크/클러스터 같은 환경 표준 | 플랫폼팀 guardrail |
| Service template | 앱 리소스와 배포 파이프라인 표준 | 개발팀 self-service |
| Pipeline integration | CI/CD와 연결 | 표준 배포 자동화 |
| Template version | 템플릿 버전 관리 | 중앙 업데이트와 호환성 |
| EOL | 지원 종료 일정 존재 | 신규 선택 시 대안 고려 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-governed-iac-deployment-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 기존 Proton 환경 운영 이해 | Proton | 신규 장기 선택은 EOL 확인 |
| 승인된 제품 self-service | Service Catalog | Proton은 앱/환경 템플릿 중심 |
| 범용 IaC | CloudFormation/CDK | Proton은 더 높은 수준의 플랫폼 워크플로우 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Proton은 시험에서 기존 개념으로 나올 수 있지만, 현재 기준 신규 설계는 지원 종료 일정을 고려해야 한다.

- Service Catalog는 승인된 제품 카탈로그, Proton은 환경/서비스 템플릿 기반 앱 배포에 가깝다.
- IaC 엔진 자체는 CloudFormation/Terraform/CDK와 비교한다.
- 장기 운영성 요구가 강하면 현재 지원 상태를 반드시 확인한다.

## 6. 암기 문장

- Proton은 플랫폼 팀 템플릿으로 앱 배포를 표준화하는 서비스였고, 2026-10-07 지원 종료 예정이다.
- 신규 self-service governance는 Service Catalog와 CloudFormation/CDK 조합을 먼저 본다.

## 참고 링크

- [What is AWS Proton?](https://docs.aws.amazon.com/proton/latest/userguide/Welcome.html)
- [AWS Proton availability change](https://docs.aws.amazon.com/proton/latest/userguide/proton-end-of-support.html)
