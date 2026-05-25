---
type: aws-service
service_name: "AWS Control Tower"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션"]
status: complete
priority: high
aliases: ["Control Tower", "Landing Zone", "Account Factory"]
tags: [aws, sap-c02, security, governance, landing-zone]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Control Tower

> [!summary] 한 줄 요약
> AWS Organizations 기반 멀티 계정 landing zone을 모범 사례대로 설정하고 guardrail과 계정 생성을 자동화하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | landing zone, guardrails, account factory, baseline, multi-account governance |
| 핵심 의사결정 | 새 멀티 계정 환경을 표준 보안 기준으로 빠르게 구축/운영해야 하면 Control Tower를 선택한다. |
| 대표 키워드 | landing zone, guardrail, account factory, baseline, preventive/detective controls |
| 자주 비교되는 서비스 | [[AWS Organizations]], [[AWS IAM Identity Center]], [[AWS Config]], [[AWS Service Catalog]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Control Tower의 시험 역할은 landing zone, guardrails, account factory, baseline, multi-account governance 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS Organizations 기반 멀티 계정 landing zone을 모범 사례대로 설정하고 guardrail과 계정 생성을 자동화하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Landing zone | 기본 계정/OU/로그/감사 구조 | 초기 멀티 계정 베이스라인 |
| Guardrails/Controls | 예방/탐지 통제 | Config/SCP 기반 거버넌스 |
| Account Factory | 표준 계정 프로비저닝 | 셀프서비스 계정 생성 |
| Dashboard | 계정 compliance 상태 가시화 | 운영 통제 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Control Tower]] | 랜딩존 자동 구성/운영 | 멀티 계정 베이스라인이 필요할 때 | 단순 계정 묶음만이면 Organizations |
| [[AWS Organizations]] | OU/SCP/결제 기본 기능 | 세밀한 계정 구조 통제 | 랜딩존 자동화는 부족 |
| [[AWS Config]] | 리소스 규정 평가 | 탐지형 control 근거 | 계정 생성 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 신규 기업 AWS 도입

- **요구사항**: 보안/로그/감사 계정과 표준 계정 생성 필요
- **정답 단서**: landing zone, guardrails
- **선택할 구성**: AWS Control Tower
- **오답 함정**: 수동 Organizations 구성만 선택

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Control Tower는 Organizations, IAM Identity Center, Config 등을 조합해 제공한다.
- 기존 복잡한 조직에는 적용 범위/드리프트를 확인해야 한다.

## 7. 암기 문장

- 표준 landing zone은 Control Tower다.
- OU/SCP 자체는 Organizations가 기반이다.

## 참고 링크

- [What is AWS Control Tower?](https://docs.aws.amazon.com/controltower/latest/userguide/what-is-control-tower.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
