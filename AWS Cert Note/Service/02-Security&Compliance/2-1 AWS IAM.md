---
type: aws-service
service_name: "AWS IAM"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["IAM", "Identity and Access Management"]
tags: [aws, sap-c02, security, iam, identity]
created: 2026-05-26
updated: 2026-05-26
---

# AWS IAM

> [!summary] 한 줄 요약
> AWS 리소스에 누가 어떤 작업을 할 수 있는지 인증·인가 정책으로 통제하는 기본 보안 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 사용자/Role/정책 기반 접근 제어, least privilege, cross-account access, federation, policy evaluation |
| 핵심 의사결정 | AWS API 권한을 세밀하게 제어해야 하면 IAM을 기본으로 사용하고, 장기 자격 증명보다 Role/STS를 우선한다. |
| 대표 키워드 | principal, policy, role, permission, least privilege, resource policy, permission boundary, SCP |
| 자주 비교되는 서비스 | [[AWS STS]], [[AWS IAM Identity Center]], [[AWS Organizations]], [[Amazon Cognito]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 계정 내 identity와 resource 접근 권한을 제어하는 글로벌 서비스.
- **왜 쓰는가?**: 사람·애플리케이션·AWS 서비스가 필요한 최소 권한으로 AWS API를 호출하게 한다.
- **관리형 여부**: IAM 자체는 관리형이지만 정책 설계, 권한 검토, key rotation은 사용자 책임이다.
- **범위/적용 위치**: 글로벌 서비스이며 리전별 리소스 권한을 정책으로 통제한다.
- **핵심 제약/한계**: 정책 평가에는 identity policy, resource policy, SCP, permission boundary, session policy가 함께 작용할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| IAM Role | 장기 비밀번호/Access key 없이 임시 권한 부여 | EC2/Lambda/ECS와 cross-account 접근의 기본 정답 |
| Policy evaluation | 명시적 Deny가 Allow보다 우선 | SCP/Boundary가 권한 최대치를 제한한다는 단서 |
| Resource-based policy | S3/KMS/SQS 등 리소스 측 정책 | 교차 계정 접근에서 identity policy와 함께 확인 |
| Permission boundary | 사용자/Role이 가질 수 있는 최대 권한 | 위임 관리자에게 권한 생성 권한을 줄 때 안전장치 |
| Access Analyzer | 외부 공유/권한 경로 분석 | least privilege와 public/cross-account 노출 점검 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IAM]] | AWS API 권한 제어 | 모든 AWS 리소스 접근 제어의 기본 | 앱 최종 사용자 로그인 서비스로 오해 금지 |
| [[AWS IAM Identity Center]] | 인력 SSO와 중앙 계정 접근 | 직원/조직 계정 포털이 필요할 때 | IAM 사용자를 대량 생성하는 방향은 오답 가능 |
| [[Amazon Cognito]] | 앱 사용자 인증/권한 위임 | 모바일/웹 앱 고객 로그인 | AWS 관리자 SSO와 혼동 금지 |
| [[AWS Organizations]] | 계정 구조와 SCP | 멀티 계정 가드레일 | 세부 리소스 권한은 IAM 정책 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-identity-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: Cross-account 운영 Role

- **요구사항**: 중앙 보안 계정에서 워크로드 계정 읽기 권한 필요
- **정답 단서**: AssumeRole, external ID, trust policy
- **선택할 구성**: IAM Role + STS
- **오답 함정**: Access key 공유는 오답

### 패턴 2: EC2가 S3 접근

- **요구사항**: 인스턴스가 객체 읽기 필요
- **정답 단서**: no hard-coded credentials
- **선택할 구성**: Instance profile Role
- **오답 함정**: 인스턴스 내부에 access key 저장 금지

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Root user는 일상 운영에 쓰지 않고 MFA와 break-glass로 보호한다.
- 권한이 안 되는 문제는 Allow만 보지 말고 명시적 Deny, SCP, boundary, session policy를 함께 본다.
- IAM User 장기 키는 자동화의 쉬운 해법처럼 보여도 Role/STS가 더 안전한 경우가 많다.

## 7. 암기 문장

- AWS API 권한의 기본 언어는 IAM policy다.
- 운영 권한은 장기 키보다 Role+STS로 준다.

## 참고 링크

- [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [Policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
