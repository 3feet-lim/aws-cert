---
type: aws-service
service_name: "AWS Certificate Manager (ACM)"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["ACM", "Certificate Manager"]
tags: [aws, sap-c02, security, tls, certificates]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Certificate Manager (ACM)

> [!summary] 한 줄 요약
> AWS 통합 서비스에서 사용할 TLS/SSL 인증서를 발급·가져오기·갱신 관리하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | TLS certificate, ALB, CloudFront, API Gateway, public/private certificate |
| 핵심 의사결정 | ALB/CloudFront/API Gateway 등에 TLS 인증서를 쉽게 배포하고 자동 갱신하려면 ACM을 선택한다. |
| 대표 키워드 | certificate, TLS, SSL, public certificate, private CA, DNS validation, automatic renewal |
| 자주 비교되는 서비스 | [[AWS KMS]], [[AWS Secrets Manager]], [[AWS WAF]], [[Elastic Load Balancing]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Certificate Manager (ACM)의 시험 역할은 TLS certificate, ALB, CloudFront, API Gateway, public/private certificate 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS 통합 서비스에서 사용할 TLS/SSL 인증서를 발급·가져오기·갱신 관리하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Public certificates | 공개 신뢰 인증서 발급 | 인터넷 HTTPS 엔드포인트 |
| Automatic renewal | ACM 발급 인증서 자동 갱신 | 운영 부담 감소 |
| AWS integrations | ALB/CloudFront/API Gateway 등 연결 | 인증서 private key 직접 접근 불가 |
| Private CA integration | 사설 인증서 발급 | 내부 PKI 요구 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Certificate Manager (ACM)]] | TLS 인증서 관리 | HTTPS 엔드포인트 인증서 | 비밀값/암호화 키 관리와 혼동 금지 |
| [[AWS Secrets Manager]] | DB/API secret 저장 | 비밀값 회전 | TLS 인증서 배포 서비스 아님 |
| [[AWS KMS]] | 암호화 키 관리 | 데이터 암호화 | 인증서 발급 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-encryption-secrets-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: ALB HTTPS 적용

- **요구사항**: 퍼블릭 웹 앱에 TLS 필요
- **정답 단서**: certificate, ALB, auto renewal
- **선택할 구성**: ACM public certificate + ALB listener
- **오답 함정**: 인증서를 EC2에 수동 배포

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- CloudFront용 ACM 인증서는 us-east-1 리전 요구가 자주 나온다.
- ACM 발급 public certificate의 private key는 내보낼 수 없다.

## 7. 암기 문장

- HTTPS 인증서 관리는 ACM이다.
- 비밀값은 Secrets Manager, 암호화 키는 KMS와 구분한다.

## 참고 링크

- [What is ACM?](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
