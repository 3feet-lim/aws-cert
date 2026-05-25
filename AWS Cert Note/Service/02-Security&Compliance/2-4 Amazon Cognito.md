---
type: aws-service
service_name: "Amazon Cognito"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Cognito", "Cognito User Pools", "Cognito Identity Pools"]
tags: [aws, sap-c02, security, identity, app-auth]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Cognito

> [!summary] 한 줄 요약
> 웹/모바일 애플리케이션의 최종 사용자 가입·로그인·토큰 발급과 AWS 리소스 접근 위임을 제공하는 ID 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 앱 사용자 인증, User Pool, Identity Pool, social IdP, JWT, federation |
| 핵심 의사결정 | B2C/B2B 앱 로그인과 사용자 토큰이 필요하면 Cognito를 선택한다. |
| 대표 키워드 | user pool, identity pool, app user, JWT, social login, federated identity |
| 자주 비교되는 서비스 | [[AWS IAM Identity Center]], [[AWS IAM]], [[AWS STS]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Amazon Cognito의 시험 역할은 앱 사용자 인증, User Pool, Identity Pool, social IdP, JWT, federation 요구를 해결하는 것이다.
- **왜 쓰는가?**: 웹/모바일 애플리케이션의 최종 사용자 가입·로그인·토큰 발급과 AWS 리소스 접근 위임을 제공하는 ID 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| User Pools | 사용자 디렉터리와 로그인/JWT 발급 | 앱 사용자 인증의 정답 단서 |
| Identity Pools | 인증된/비인증 사용자에게 AWS 임시 권한 | S3 업로드 등 제한된 AWS 접근 |
| Hosted UI/Federation | 소셜/기업 IdP 연동 | 빠른 앱 인증 구현 |
| MFA/Adaptive security | 사용자 로그인 보호 | 앱 보안 강화 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Cognito]] | 앱 최종 사용자 인증 | 모바일/웹 서비스 회원 로그인 | 직원 AWS 계정 SSO로 오해 금지 |
| [[AWS IAM Identity Center]] | 인력 SSO | 직원/운영자의 AWS 계정 접근 | 고객 앱 로그인에는 부적합 |
| [[AWS IAM]] | AWS API 권한 | 서비스/관리자 권한 제어 | 사용자 가입/로그인 UI 제공 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-identity-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 모바일 앱 사진 업로드

- **요구사항**: 로그인한 사용자만 S3에 제한 업로드
- **정답 단서**: app user, temporary AWS credentials
- **선택할 구성**: Cognito User Pool + Identity Pool
- **오답 함정**: IAM User를 앱에 내장

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- User Pool은 인증/JWT, Identity Pool은 AWS 임시 권한에 가깝다.
- Cognito는 앱 사용자용이고 IAM Identity Center는 workforce용이다.

## 7. 암기 문장

- 앱 사용자 로그인은 Cognito다.
- AWS 권한 위임이 필요하면 Identity Pool/STS 흐름을 본다.

## 참고 링크

- [What is Amazon Cognito?](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
