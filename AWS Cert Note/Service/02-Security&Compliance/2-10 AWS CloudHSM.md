---
type: aws-service
service_name: "AWS CloudHSM"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["CloudHSM"]
tags: [aws, sap-c02, security, encryption, hsm]
created: 2026-05-26
updated: 2026-05-26
---

# AWS CloudHSM

> [!summary] 한 줄 요약
> 고객 전용 하드웨어 보안 모듈 클러스터를 AWS에서 제공해 키를 직접 제어하게 하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | dedicated HSM, FIPS, custom key store, PKCS#11, customer-managed keys |
| 핵심 의사결정 | 규정상 전용 HSM과 키 단독 제어가 필요하면 CloudHSM을 선택한다. |
| 대표 키워드 | HSM, FIPS 140, PKCS#11, JCE, CNG, key ownership, custom key store |
| 자주 비교되는 서비스 | [[AWS KMS]], [[AWS Secrets Manager]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS CloudHSM의 시험 역할은 dedicated HSM, FIPS, custom key store, PKCS#11, customer-managed keys 요구를 해결하는 것이다.
- **왜 쓰는가?**: 고객 전용 하드웨어 보안 모듈 클러스터를 AWS에서 제공해 키를 직접 제어하게 하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Dedicated HSM | 고객 전용 HSM 인스턴스 | 키 단독 제어와 규제 요구 |
| Cluster/Multi-AZ | HSM 클러스터 고가용성 | 운영 설계 필요 |
| Crypto APIs | PKCS#11/JCE/CNG 지원 | 특수 앱 암호화 연동 |
| KMS custom key store | KMS와 CloudHSM 연계 | KMS 편의성과 HSM 제어 결합 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS CloudHSM]] | 전용 HSM 직접 제어 | 강한 규제/특수 암호화 API | 운영 부담과 비용 큼 |
| [[AWS KMS]] | 관리형 키 관리 | 대부분 AWS 서비스 암호화 | 키 material 직접 제어 요구에는 부족할 수 있음 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-encryption-secrets-flow.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 규제상 HSM 요구

- **요구사항**: 키를 공유 인프라가 아닌 전용 HSM에 보관
- **정답 단서**: FIPS, dedicated HSM
- **선택할 구성**: CloudHSM cluster
- **오답 함정**: 일반 KMS만 사용

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- CloudHSM은 완전 서버리스 키 서비스가 아니라 클러스터 운영 고려가 필요하다.
- 일반적인 EBS/S3/RDS 암호화 문제는 KMS가 더 흔한 정답이다.

## 7. 암기 문장

- 전용 HSM이면 CloudHSM이다.
- 일반 관리형 키 암호화는 KMS부터 본다.

## 참고 링크

- [What is AWS CloudHSM?](https://docs.aws.amazon.com/cloudhsm/latest/userguide/introduction.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
