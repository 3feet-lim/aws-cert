---
type: aws-service
service_name: "AWS IAM Identity Center"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["IAM Identity Center", "AWS SSO"]
tags: [aws, sap-c02, security, iam, sso]
created: 2026-05-26
updated: 2026-05-26
---

# AWS IAM Identity Center

> [!summary] 한 줄 요약
> 직원과 관리자가 여러 AWS 계정과 애플리케이션에 중앙 SSO로 접근하게 하는 인력 ID 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 멀티 계정 인력 접근, SSO, permission set, external IdP 연동 |
| 핵심 의사결정 | 조직 사용자에게 여러 AWS 계정 접근을 중앙에서 부여해야 하면 IAM Identity Center를 선택한다. |
| 대표 키워드 | SSO, workforce identity, permission set, AWS Organizations, external identity provider, SAML, SCIM |
| 자주 비교되는 서비스 | [[AWS IAM]], [[AWS Organizations]], [[Amazon Cognito]], [[AWS Directory Service]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Organizations와 통합해 인력 사용자의 계정/역할 접근을 중앙 관리한다.
- **왜 쓰는가?**: Okta/Entra ID 같은 외부 IdP 또는 Identity Center directory와 연동할 수 있다.
- **관리형 여부**: Permission set은 대상 계정에 IAM Role 형태 권한을 프로비저닝한다.
- **범위/적용 위치**: 주로 리전별 Identity Center 인스턴스를 활성화하지만 계정 접근은 조직 전반에 적용된다.
- **핵심 제약/한계**: 고객 앱 사용자 인증용 서비스가 아니라 직원/운영자 SSO 서비스다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Permission set | 직무별 권한 템플릿 | 여러 계정에 같은 권한을 일관 적용 |
| External IdP | SAML/OIDC/SCIM 기반 연동 | 기업 디렉터리 유지와 AWS 접근 통합 |
| Multi-account access | AWS access portal 제공 | 계정별 IAM User 생성 방지 |
| MFA/Session control | 인증 강도와 세션 제어 | 보안 요구와 운영 편의 균형 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS IAM Identity Center]] | 인력 SSO 중앙 관리 | 직원/관리자 멀티 계정 접근 | 앱 고객 로그인용으로 선택하면 오답 |
| [[AWS IAM]] | 정책/Role 권한 엔진 | 서비스/리소스 권한 세부 제어 | 대규모 직원 계정 수동 생성은 비효율 |
| [[Amazon Cognito]] | 앱 최종 사용자 로그인 | B2C/B2B 애플리케이션 인증 | AWS 계정 관리 포털이 아님 |
| [[AWS Directory Service]] | Microsoft AD 연동/운영 | 도메인 조인/LDAP/Kerberos 요구 | SSO 권한 배포 자체는 Identity Center |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-identity-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴x 

### 패턴 1: 기업 SSO로 AWS 접근

- **요구사항**: 여러 팀이 여러 계정에 직무별 접근 필요
- **정답 단서**: permission set, SSO portal, Organizations
- **선택할 구성**: IAM Identity Center + external IdP
- **오답 함정**: 각 계정 IAM User 생성

### 패턴 2: 퇴사자 접근 회수

- **요구사항**: 중앙 IdP에서 비활성화 시 AWS 접근도 제거
- **정답 단서**: SCIM, centralized identity
- **선택할 구성**: Identity Center 연동
- **오답 함정**: 계정별 수동 회수

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- IAM Identity Center는 IAM을 대체하지 않고 IAM Role/Policy를 배포해 사용한다.
- Cognito와 가장 많이 혼동된다. Cognito는 애플리케이션 사용자, Identity Center는 인력 사용자다.

## 7. 암기 문장

- 직원 SSO와 멀티 계정 접근은 IAM Identity Center다.
- Permission set은 계정별 Role 권한을 중앙에서 배포하는 단위다.

## 참고 링크

- [What is IAM Identity Center?](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
