---
type: aws-service
service_name: "AWS Artifact"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Artifact"]
tags: [aws, sap-c02, security, compliance, reports]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Artifact

> [!summary] 한 줄 요약
> AWS의 보안·규정 준수 보고서와 일부 계약 문서에 온디맨드로 접근하는 포털 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | compliance reports, SOC, ISO, PCI, agreements, auditor evidence |
| 핵심 의사결정 | 감사인에게 AWS 인프라의 compliance 보고서나 계약 문서를 제공해야 하면 Artifact를 사용한다. |
| 대표 키워드 | SOC report, ISO certification, PCI, compliance report, agreement, NDA |
| 자주 비교되는 서비스 | [[AWS Audit Manager]], [[AWS Config]], [[AWS Security Hub]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS Artifact의 시험 역할은 compliance reports, SOC, ISO, PCI, agreements, auditor evidence 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS의 보안·규정 준수 보고서와 일부 계약 문서에 온디맨드로 접근하는 포털 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Reports | SOC/ISO/PCI 등 보고서 다운로드 | AWS 자체 통제 증거 제공 |
| Agreements | BAA 등 계약 검토/수락 | 규정 요구 계약 관리 |
| On-demand access | 콘솔에서 즉시 접근 | 감사 대응 자료 확보 |
| Organization agreements | 조직 계정 계약 관리 | 멀티 계정 compliance 운영 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Artifact]] | AWS compliance 보고서/계약 | AWS가 준수하는 통제 증명 필요 | 내 워크로드 증거 수집 아님 |
| [[AWS Audit Manager]] | 고객 환경 감사 증거 수집 | 내 계정 리소스 평가 | AWS 보고서 포털과 다름 |
| [[AWS Config]] | 리소스 설정 기록/규칙 | 내 환경 compliance 상태 | AWS 인증서 다운로드 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 감사인이 SOC 보고서 요청

- **요구사항**: AWS 데이터센터/서비스 통제 보고서 필요
- **정답 단서**: SOC, ISO, compliance report
- **선택할 구성**: AWS Artifact
- **오답 함정**: CloudTrail 로그만 제출

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Artifact는 보안 스캐너나 탐지 서비스가 아니다.
- 내 계정의 실제 리소스 compliance 증거는 Audit Manager/Config와 함께 본다.

## 7. 암기 문장

- AWS 준수 보고서 다운로드는 Artifact다.
- 내 환경 감사 증거는 Audit Manager다.

## 참고 링크

- [What is AWS Artifact?](https://docs.aws.amazon.com/artifact/latest/ug/what-is-aws-artifact.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
