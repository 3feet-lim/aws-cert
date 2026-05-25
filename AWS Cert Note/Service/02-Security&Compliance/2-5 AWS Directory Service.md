---
type: aws-service
service_name: "AWS Directory Service"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Directory Service", "AWS Managed Microsoft AD", "AD Connector"]
tags: [aws, sap-c02, security, directory, microsoft-ad]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Directory Service

> [!summary] 한 줄 요약
> Microsoft AD 호환 디렉터리 또는 온프레미스 AD 연결을 관리형으로 제공해 Windows 워크로드와 기업 인증을 통합하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | Microsoft AD, domain join, AD Connector, trust, Kerberos/LDAP |
| 핵심 의사결정 | Windows/AD 의존 워크로드를 AWS로 이전하거나 AWS 서비스가 AD 인증을 써야 하면 Directory Service를 고려한다. |
| 대표 키워드 | Microsoft AD, domain join, trust relationship, AD Connector, WorkSpaces, FSx for Windows |
| 자주 비교되는 서비스 | [[AWS IAM Identity Center]], [[Amazon Cognito]], [[AWS Organizations]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS Directory Service의 시험 역할은 Microsoft AD, domain join, AD Connector, trust, Kerberos/LDAP 요구를 해결하는 것이다.
- **왜 쓰는가?**: Microsoft AD 호환 디렉터리 또는 온프레미스 AD 연결을 관리형으로 제공해 Windows 워크로드와 기업 인증을 통합하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| AWS Managed Microsoft AD | AWS 관리형 실제 Microsoft AD | 도메인 조인/Group Policy/trust 요구 |
| AD Connector | 온프레미스 AD로 프록시 | 디렉터리를 AWS에 새로 만들지 않을 때 |
| Simple AD | 소규모 Samba 기반 디렉터리 | 기능 제한과 비용 단서 |
| Trust relationship | 온프레미스 AD와 신뢰 구성 | 하이브리드 identity |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Directory Service]] | AD 호환 디렉터리/연결 | Windows 도메인 조인과 AD 인증 | AWS API 권한 서비스로 오해 금지 |
| [[AWS IAM Identity Center]] | AWS 계정/앱 SSO | 인력 접근 포털 | AD 기능 자체 제공 아님 |
| [[Amazon Cognito]] | 앱 고객 로그인 | 웹/모바일 사용자 인증 | Windows 도메인 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-identity-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: Windows 파일 서버 이전

- **요구사항**: FSx for Windows가 AD 도메인 필요
- **정답 단서**: domain join, managed AD
- **선택할 구성**: AWS Managed Microsoft AD
- **오답 함정**: IAM만으로 Windows 도메인 대체

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- AD Connector는 디렉터리 데이터를 저장하지 않고 기존 AD로 요청을 프록시한다.
- IAM 정책과 Microsoft AD 권한 모델은 목적이 다르다.

## 7. 암기 문장

- AD 의존 Windows 워크로드는 Directory Service를 떠올린다.
- AWS 계정 SSO는 Identity Center와 조합한다.

## 참고 링크

- [What is AWS Directory Service?](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/what_is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
