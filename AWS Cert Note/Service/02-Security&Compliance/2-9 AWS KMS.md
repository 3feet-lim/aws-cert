---
type: aws-service
service_name: "AWS KMS"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["KMS", "Key Management Service", "KMS key"]
tags: [aws, sap-c02, security, encryption, kms]
created: 2026-05-26
updated: 2026-05-26
---

# AWS KMS

> [!summary] 한 줄 요약
> AWS 서비스와 애플리케이션에서 사용하는 암호화 키를 생성·관리·감사하는 관리형 키 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | encryption at rest, KMS key, envelope encryption, key policy, grants, multi-Region key |
| 핵심 의사결정 | AWS 서비스 데이터 암호화와 키 접근 제어/감사가 필요하면 KMS를 기본 선택한다. |
| 대표 키워드 | KMS key, CMK, key policy, envelope encryption, CloudTrail, rotation, multi-Region key |
| 자주 비교되는 서비스 | [[AWS CloudHSM]], [[AWS Secrets Manager]], [[AWS Certificate Manager (ACM)]], [[Amazon S3]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS KMS의 시험 역할은 encryption at rest, KMS key, envelope encryption, key policy, grants, multi-Region key 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS 서비스와 애플리케이션에서 사용하는 암호화 키를 생성·관리·감사하는 관리형 키 관리 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| KMS keys | 대칭/비대칭/HMAC 키 관리 | 대부분 AWS 서비스 암호화 기본 |
| Key policy | 키 사용 권한의 기본 제어 | IAM만으로 안 되는 KMS 권한 함정 |
| Envelope encryption | 데이터 키로 대용량 데이터 암호화 | S3/EBS/RDS 등 내부 패턴 |
| Multi-Region keys | 동일 key material을 여러 리전에 복제 | DR/글로벌 앱 암호화 단서 |
| CloudTrail integration | 키 사용 감사 | 규정 준수와 추적 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS KMS]] | 관리형 키 서비스 | AWS 서비스 암호화/감사/권한 제어 | 전용 HSM 단독 제어 요구에는 CloudHSM |
| [[AWS CloudHSM]] | 고객 전용 HSM 클러스터 | FIPS/키 직접 제어/특수 암호화 API | 일반 AWS 서비스 암호화에는 운영 부담 큼 |
| [[AWS Secrets Manager]] | 비밀값 저장/회전 | DB 비밀번호/API key | 암호화 키 관리 서비스가 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-encryption-secrets-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: S3 객체 암호화와 감사

- **요구사항**: 민감 데이터 저장 시 키 접근 제어 필요
- **정답 단서**: SSE-KMS, key policy, CloudTrail
- **선택할 구성**: S3 SSE-KMS + KMS key
- **오답 함정**: 애플리케이션에 키 하드코딩

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- KMS key policy가 권한의 출발점이다. IAM Allow만으로 항상 충분하지 않다.
- KMS는 키 관리, Secrets Manager는 비밀값 lifecycle 관리다.

## 7. 암기 문장

- AWS 서비스 암호화 키는 KMS다.
- 전용 HSM/키 직접 제어 요구가 강하면 CloudHSM과 비교한다.

## 참고 링크

- [What is AWS KMS?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
