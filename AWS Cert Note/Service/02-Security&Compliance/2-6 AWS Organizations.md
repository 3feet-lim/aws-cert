---
type: aws-service
service_name: "AWS Organizations"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Organizations", "AWS Organizations", "SCP"]
tags: [aws, sap-c02, security, governance, multi-account]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Organizations

> [!summary] 한 줄 요약
> 여러 AWS 계정을 OU로 묶고 통합 결제와 SCP 기반 가드레일을 제공하는 멀티 계정 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | multi-account, OU, SCP, consolidated billing, delegated administrator |
| 핵심 의사결정 | 계정이 많고 조직 단위 통제/결제/서비스 통합이 필요하면 Organizations를 선택한다. |
| 대표 키워드 | organization, OU, SCP, consolidated billing, delegated admin, account vending |
| 자주 비교되는 서비스 | [[AWS Control Tower]], [[AWS IAM]], [[AWS RAM]], [[AWS IAM Identity Center]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Organizations의 시험 역할은 multi-account, OU, SCP, consolidated billing, delegated administrator 요구를 해결하는 것이다.
- **왜 쓰는가?**: 여러 AWS 계정을 OU로 묶고 통합 결제와 SCP 기반 가드레일을 제공하는 멀티 계정 관리 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| OU | 계정 그룹화 | 환경/팀/보안 경계 설계 |
| SCP | 계정 권한 최대치 제한 | 명시적 Deny 가드레일 |
| Consolidated billing | 조직 통합 결제 | 비용/할인 집계 |
| Delegated administrator | 서비스 관리 계정 위임 | Security Hub/GuardDuty 등 중앙 운영 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Organizations]] | 계정 구조와 SCP | 멀티 계정 기본 거버넌스 | 세부 리소스 권한은 IAM |
| [[AWS Control Tower]] | 표준 랜딩존 자동화 | 새 조직/계정 베이스라인 빠른 구축 | Organizations 없이 단독 대체 아님 |
| [[AWS RAM]] | 리소스 공유 | 서브넷/TGW 등 공유 | 계정 생성/OU 통제는 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 모든 계정 특정 리전 금지

- **요구사항**: 조직 전체에서 허용 리전 제한
- **정답 단서**: SCP, OU
- **선택할 구성**: Organizations SCP
- **오답 함정**: 각 계정 IAM 정책 수동 설정

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- SCP는 권한을 부여하지 않고 최대 권한을 제한한다.
- Management account는 최소 사용하고 delegated admin을 활용한다.

## 7. 암기 문장

- 멀티 계정 구조와 SCP는 Organizations다.
- SCP는 Allow가 아니라 guardrail로 기억한다.

## 참고 링크

- [What is AWS Organizations?](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)
- [SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
