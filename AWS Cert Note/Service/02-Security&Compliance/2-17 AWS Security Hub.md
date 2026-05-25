---
type: aws-service
service_name: "AWS Security Hub"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Security Hub"]
tags: [aws, sap-c02, security, posture, findings]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Security Hub

> [!summary] 한 줄 요약
> 여러 AWS 보안 서비스와 파트너 findings를 중앙 집계하고 보안 표준 준수 상태를 평가하는 보안 상태 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | central security findings, CSPM, security standards, aggregation |
| 핵심 의사결정 | 조직 전체 보안 findings와 compliance 표준을 한 곳에서 우선순위화해야 하면 Security Hub를 선택한다. |
| 대표 키워드 | security findings, standards, CIS, FSBP, aggregation, delegated admin |
| 자주 비교되는 서비스 | [[Amazon GuardDuty]], [[Amazon Inspector]], [[Amazon Macie]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Security Hub의 시험 역할은 central security findings, CSPM, security standards, aggregation 요구를 해결하는 것이다.
- **왜 쓰는가?**: 여러 AWS 보안 서비스와 파트너 findings를 중앙 집계하고 보안 표준 준수 상태를 평가하는 보안 상태 관리 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Finding aggregation | GuardDuty/Inspector/Macie 등 통합 | 중앙 대시보드 |
| Security standards | FSBP/CIS 등 자동 점검 | compliance posture |
| Multi-account admin | 조직 단위 중앙 관리 | 보안 계정 운영 |
| Automation integration | EventBridge/ASFF | 자동 대응 워크플로우 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Security Hub]] | finding 집계/표준 평가 | 여러 보안 신호 중앙화 | 탐지 엔진 하나가 아님 |
| [[Amazon GuardDuty]] | 위협 탐지 | 악성 활동 finding 생성 | 여러 소스 통합은 Security Hub |
| [[AWS Config]] | 설정 변경/규칙 평가 | 리소스 compliance 원천 | 보안 finding 통합 대시보드는 Security Hub |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-detection-response-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 조직 보안 대시보드

- **요구사항**: 여러 계정 GuardDuty/Inspector findings 통합
- **정답 단서**: central findings, standards
- **선택할 구성**: Security Hub delegated admin
- **오답 함정**: 각 서비스 콘솔만 개별 확인

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Security Hub는 findings를 모으고 표준을 평가하지만 네트워크 트래픽을 직접 차단하지 않는다.
- Config와 통합되지만 Security Hub의 초점은 보안 findings 우선순위화다.

## 7. 암기 문장

- 보안 findings 중앙 집계는 Security Hub다.
- 탐지 소스는 GuardDuty/Inspector/Macie로 나뉜다.

## 참고 링크

- [What is AWS Security Hub?](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
