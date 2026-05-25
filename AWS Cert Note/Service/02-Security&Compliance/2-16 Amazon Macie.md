---
type: aws-service
service_name: "Amazon Macie"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Macie"]
tags: [aws, sap-c02, security, data-protection, pii]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Macie

> [!summary] 한 줄 요약
> S3 객체를 분석해 PII 같은 민감 데이터를 발견·분류하고 노출 위험을 알리는 데이터 보안 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | S3 sensitive data discovery, PII, data classification, bucket exposure |
| 핵심 의사결정 | S3에 저장된 민감 데이터 발견/분류와 공개 위험 점검이 필요하면 Macie를 선택한다. |
| 대표 키워드 | sensitive data, PII, S3 bucket, classification, data discovery |
| 자주 비교되는 서비스 | [[Amazon S3]], [[AWS Security Hub]], [[Amazon GuardDuty]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Amazon Macie의 시험 역할은 S3 sensitive data discovery, PII, data classification, bucket exposure 요구를 해결하는 것이다.
- **왜 쓰는가?**: S3 객체를 분석해 PII 같은 민감 데이터를 발견·분류하고 노출 위험을 알리는 데이터 보안 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Sensitive data discovery | PII/자격 증명 등 탐지 | 데이터 분류 요구 |
| S3 security posture | 버킷 공개/암호화 상태 평가 | 데이터 노출 위험 |
| Findings | 민감 데이터/정책 위반 알림 | Security Hub 연동 |
| Custom data identifiers | 조직별 패턴 탐지 | 규정 데이터 식별 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Macie]] | S3 민감 데이터 탐지 | PII/classification 요구 | 일반 악성 활동 탐지 아님 |
| [[Amazon GuardDuty]] | 위협 탐지 | 계정/워크로드 침해 정황 | S3 데이터 분류와 다름 |
| [[AWS Config]] | 리소스 설정 규정 평가 | 버킷 설정 compliance | 객체 내용 PII 탐지는 Macie |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-detection-response-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: S3에 PII 존재 확인

- **요구사항**: 데이터 레이크에 주민번호/카드정보 포함 여부 탐지
- **정답 단서**: sensitive data, PII, S3
- **선택할 구성**: Amazon Macie
- **오답 함정**: Inspector로 데이터 분류

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Macie의 핵심 범위는 S3 민감 데이터 발견이다.
- 버킷 정책 위반만 보면 Config도 가능하지만 객체 내용 분류는 Macie다.

## 7. 암기 문장

- S3 민감 데이터/PII 탐지는 Macie다.
- 위협 탐지 GuardDuty, 취약점 Inspector와 구분한다.

## 참고 링크

- [What is Amazon Macie?](https://docs.aws.amazon.com/macie/latest/user/what-is-macie.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
