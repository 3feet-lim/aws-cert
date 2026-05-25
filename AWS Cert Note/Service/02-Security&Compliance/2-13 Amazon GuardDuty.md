---
type: aws-service
service_name: "Amazon GuardDuty"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["GuardDuty"]
tags: [aws, sap-c02, security, threat-detection]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon GuardDuty

> [!summary] 한 줄 요약
> CloudTrail, VPC Flow Logs, DNS 로그 등 신호를 분석해 계정/워크로드의 위협 활동을 탐지하는 관리형 threat detection 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | threat detection, malicious activity, findings, threat intelligence |
| 핵심 의사결정 | 계정 침해, 의심스러운 API 호출, 악성 네트워크 활동을 자동 탐지해야 하면 GuardDuty를 선택한다. |
| 대표 키워드 | threat detection, finding, compromised instance, anomalous API, malware protection, DNS exfiltration |
| 자주 비교되는 서비스 | [[AWS Security Hub]], [[Amazon Detective]], [[Amazon Inspector]], [[Amazon Macie]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Amazon GuardDuty의 시험 역할은 threat detection, malicious activity, findings, threat intelligence 요구를 해결하는 것이다.
- **왜 쓰는가?**: CloudTrail, VPC Flow Logs, DNS 로그 등 신호를 분석해 계정/워크로드의 위협 활동을 탐지하는 관리형 threat detection 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Managed threat detection | 로그/이벤트 기반 위협 탐지 | 운영 부담 없이 findings 생성 |
| Threat intelligence/ML | 악성 IP/이상 행위 분석 | 침해 단서 탐지 |
| Multi-account admin | 조직 중앙 관리 | 보안 계정 집계 |
| Runtime/Malware options | 워크로드 보호 확장 | EC2/EKS/S3 등 보호 범위 확인 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon GuardDuty]] | 위협/침해 탐지 | 의심 활동 findings 필요 | 취약점 스캐너가 아님 |
| [[Amazon Inspector]] | 취약점 평가 | CVE/패키지 취약점 | 실시간 공격 탐지와 다름 |
| [[Amazon Detective]] | 조사/그래프 분석 | GuardDuty finding 원인 분석 | 탐지 엔진 자체가 아님 |
| [[AWS Security Hub]] | findings 중앙 집계 | 여러 보안 서비스 통합 | 단일 탐지 소스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-detection-response-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 계정 침해 의심

- **요구사항**: 비정상 API 호출과 악성 IP 통신 탐지
- **정답 단서**: threat intelligence, finding
- **선택할 구성**: GuardDuty
- **오답 함정**: Inspector만 활성화

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- GuardDuty는 로그를 분석하지만 로그 저장/감사 원본은 CloudTrail 등이다.
- 취약점(CVE) 찾기는 Inspector와 구분한다.

## 7. 암기 문장

- 위협 탐지는 GuardDuty다.
- 조사는 Detective, 중앙 집계는 Security Hub다.

## 참고 링크

- [What is Amazon GuardDuty?](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
