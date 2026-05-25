---
type: aws-service
service_name: "Amazon Detective"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Detective"]
tags: [aws, sap-c02, security, investigation]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Detective

> [!summary] 한 줄 요약
> 보안 finding 주변의 계정·리소스·네트워크 활동 관계를 그래프로 분석해 조사 시간을 줄이는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | security investigation, behavior graph, root cause, GuardDuty findings |
| 핵심 의사결정 | GuardDuty/Security Hub finding의 원인과 관련 활동을 빠르게 조사해야 하면 Detective를 사용한다. |
| 대표 키워드 | investigation, behavior graph, finding triage, root cause, related resources |
| 자주 비교되는 서비스 | [[Amazon GuardDuty]], [[AWS Security Hub]], [[AWS CloudTrail]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Amazon Detective의 시험 역할은 security investigation, behavior graph, root cause, GuardDuty findings 요구를 해결하는 것이다.
- **왜 쓰는가?**: 보안 finding 주변의 계정·리소스·네트워크 활동 관계를 그래프로 분석해 조사 시간을 줄이는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Behavior graph | 로그 기반 관계 그래프 생성 | 이벤트 상관관계 조사 |
| Finding investigation | GuardDuty finding 심층 분석 | 침해 범위 파악 |
| Entity profiles | 계정/사용자/IP/리소스 활동 보기 | 원인 분석 단서 |
| Multi-account | 조직 보안 조사 지원 | 중앙 보안 운영 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Detective]] | 보안 조사/상관 분석 | finding 원인 분석 | 탐지 자체는 GuardDuty |
| [[Amazon GuardDuty]] | 위협 finding 생성 | 악성 활동 탐지 | 그래프 기반 심층 조사 목적 아님 |
| [[AWS Security Hub]] | finding 집계와 표준 점검 | 보안 상태 중앙화 | 조사 그래프는 Detective |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-detection-response-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: GuardDuty finding 분석

- **요구사항**: 의심 EC2와 관련 API/IP 활동 파악
- **정답 단서**: investigate, behavior graph
- **선택할 구성**: Amazon Detective
- **오답 함정**: CloudTrail 로그를 모두 수동 grep

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Detective는 보안 데이터를 분석하지만 예방/차단 서비스가 아니다.
- 탐지-조사-집계 역할을 GuardDuty/Detective/Security Hub로 구분한다.

## 7. 암기 문장

- Finding 조사는 Detective다.
- 탐지는 GuardDuty, 중앙 대시보드는 Security Hub다.

## 참고 링크

- [What is Amazon Detective?](https://docs.aws.amazon.com/detective/latest/userguide/what-is-detective.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
