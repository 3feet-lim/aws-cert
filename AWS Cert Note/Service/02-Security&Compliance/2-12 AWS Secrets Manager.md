---
type: aws-service
service_name: "AWS Secrets Manager"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Secrets Manager"]
tags: [aws, sap-c02, security, secrets, rotation]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Secrets Manager

> [!summary] 한 줄 요약
> 데이터베이스 비밀번호, API 키 같은 비밀값을 안전하게 저장하고 자동 교체(rotation)하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | secret storage, automatic rotation, RDS credentials, API keys |
| 핵심 의사결정 | 비밀값 저장과 주기적 rotation이 필요하면 Secrets Manager를 선택한다. |
| 대표 키워드 | secret, rotation, database credentials, API key, Lambda rotation, KMS encryption |
| 자주 비교되는 서비스 | [[AWS KMS]], [[AWS Systems Manager Parameter Store]], [[AWS Certificate Manager (ACM)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Secrets Manager의 시험 역할은 secret storage, automatic rotation, RDS credentials, API keys 요구를 해결하는 것이다.
- **왜 쓰는가?**: 데이터베이스 비밀번호, API 키 같은 비밀값을 안전하게 저장하고 자동 교체(rotation)하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Secret storage | 비밀값 암호화 저장 | 코드/환경변수 하드코딩 제거 |
| Automatic rotation | Lambda 기반 교체 | RDS/Aurora 자격 증명 관리 단서 |
| Fine-grained access | IAM/KMS로 접근 통제 | 최소 권한과 감사 |
| Version staging labels | AWSCURRENT/AWSPREVIOUS | 무중단 rotation 이해 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Secrets Manager]] | 비밀값 저장/회전 | DB password/API key lifecycle | 암호화 키 자체 관리가 아님 |
| [[AWS Systems Manager Parameter Store]] | 설정값/간단 secret 저장 | 비용/단순 설정 중심 | 자동 rotation은 Secrets Manager가 강점 |
| [[AWS KMS]] | 암호화 키 관리 | secret 암호화에 사용 | 비밀번호 교체 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-encryption-secrets-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: RDS 비밀번호 자동 교체

- **요구사항**: 앱 코드에 DB 암호 저장 금지
- **정답 단서**: rotation, database credentials
- **선택할 구성**: Secrets Manager rotation
- **오답 함정**: 소스 코드에 암호 저장

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Secrets Manager는 KMS를 사용해 secret을 암호화하지만 KMS를 대체하지 않는다.
- Parameter Store와 비교할 때 rotation/secret lifecycle 요구가 핵심 단서다.

## 7. 암기 문장

- 비밀번호/API key 저장과 rotation은 Secrets Manager다.
- 키 관리는 KMS와 분리해 기억한다.

## 참고 링크

- [What is AWS Secrets Manager?](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
