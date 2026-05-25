---
type: aws-service
service_name: "AWS STS"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["STS", "Security Token Service"]
tags: [aws, sap-c02, security, iam, sts]
created: 2026-05-26
updated: 2026-05-26
---

# AWS STS

> [!summary] 한 줄 요약
> Role assumption과 federation을 통해 제한 시간 임시 보안 자격 증명을 발급하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 임시 자격 증명, AssumeRole, cross-account access, federation |
| 핵심 의사결정 | 장기 access key 없이 AWS 권한을 위임하거나 교차 계정 접근해야 하면 STS 기반 임시 자격 증명을 사용한다. |
| 대표 키워드 | temporary credentials, AssumeRole, trust policy, session token, federation, external ID |
| 자주 비교되는 서비스 | [[AWS IAM]], [[AWS IAM Identity Center]], [[Amazon Cognito]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: IAM Role을 맡아 임시 access key, secret key, session token을 발급한다.
- **왜 쓰는가?**: 교차 계정, SAML/OIDC federation, 서비스 Role에서 핵심적으로 사용된다.
- **관리형 여부**: 관리형 글로벌 서비스이며 리전 엔드포인트 사용도 가능하다.
- **범위/적용 위치**: 권한은 Role 정책, trust policy, session policy, SCP 등에 의해 제한된다.
- **핵심 제약/한계**: 임시 자격 증명에는 만료 시간이 있어 장기 키 노출 위험을 줄인다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| AssumeRole | 다른 Role 권한으로 세션 발급 | cross-account와 workload identity 기본 패턴 |
| External ID | 제3자 SaaS 접근 confused deputy 방지 | 외부 벤더 계정 접근 문제 단서 |
| Federation | SAML/OIDC 사용자에게 임시 권한 | 기업 IdP와 AWS 연동 |
| Session policy/tags | 세션별 권한 축소와 속성 전달 | ABAC와 임시 권한 제한 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS STS]] | 임시 자격 증명 발급 | 권한 위임/교차 계정/연동 | 정책 저장소 자체가 아님 |
| [[AWS IAM]] | Role/Policy 정의 | 누가 무엇을 할 수 있는지 선언 | 임시 토큰 발급은 STS |
| [[Amazon Cognito]] | 앱 사용자 인증과 AWS 권한 위임 | 모바일/웹 앱 사용자 | 관리자 cross-account Role과 혼동 금지 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-identity-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: SaaS가 고객 계정 읽기

- **요구사항**: 외부 업체가 고객 AWS 계정 모니터링
- **정답 단서**: external ID, cross-account role
- **선택할 구성**: STS AssumeRole
- **오답 함정**: 업체에게 access key 발급

### 패턴 2: CI/CD 배포 권한

- **요구사항**: 빌드 시스템이 배포 Role을 잠깐 사용
- **정답 단서**: temporary credentials, OIDC
- **선택할 구성**: STS federation/AssumeRole
- **오답 함정**: 장기 키를 CI secret에 저장

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Trust policy는 누가 Role을 맡을 수 있는지, permission policy는 맡은 뒤 무엇을 할 수 있는지다.
- STS로 발급받은 권한도 SCP와 permission boundary를 넘어설 수 없다.

## 7. 암기 문장

- 임시 자격 증명과 Role assumption은 STS다.
- 제3자 교차 계정 접근에는 external ID를 떠올린다.

## 참고 링크

- [Temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html)
- [AWS STS API Reference](https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
