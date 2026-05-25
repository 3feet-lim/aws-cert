---
type: aws-service
service_name: "AWS Audit Manager"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Audit Manager"]
tags: [aws, sap-c02, security, compliance, audit]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Audit Manager

> [!summary] 한 줄 요약
> AWS 사용 증거를 프레임워크 기준으로 자동 수집해 감사 준비와 규정 준수 평가를 돕는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | audit evidence, compliance framework, assessment, control evidence |
| 핵심 의사결정 | 감사 증적 수집과 compliance assessment 자동화가 필요하면 Audit Manager를 선택한다. |
| 대표 키워드 | audit evidence, assessment, control, compliance framework, SOC, PCI, HIPAA |
| 자주 비교되는 서비스 | [[AWS Artifact]], [[AWS Config]], [[AWS Security Hub]], [[AWS CloudTrail]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS Audit Manager의 시험 역할은 audit evidence, compliance framework, assessment, control evidence 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS 사용 증거를 프레임워크 기준으로 자동 수집해 감사 준비와 규정 준수 평가를 돕는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Assessments | 감사 프레임워크별 평가 생성 | 규정 준수 프로젝트 관리 |
| Evidence collection | AWS 서비스 데이터 자동 수집 | 감사 준비 시간 단축 |
| Control mapping | 요구사항과 증거 연결 | 감사 추적성 |
| Delegated admin | 조직 계정 증거 중앙 관리 | 멀티 계정 compliance |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Audit Manager]] | 고객 환경의 감사 증거 수집 | 감사 준비/평가 자동화 | AWS 자체 compliance 보고서 다운로드는 Artifact |
| [[AWS Artifact]] | AWS 보고서/계약 접근 | SOC/ISO 보고서 확인 | 내 리소스 증거 수집 아님 |
| [[AWS Config]] | 리소스 설정 기록/규칙 | 증거 소스 중 하나 | 감사 워크플로우 전체는 Audit Manager |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: PCI 감사 준비

- **요구사항**: 여러 계정 컨트롤 증거 자동 수집
- **정답 단서**: audit evidence, framework
- **선택할 구성**: Audit Manager
- **오답 함정**: Artifact만 다운로드

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Audit Manager는 고객 워크로드 증거 수집, Artifact는 AWS의 준수 문서 제공이다.
- 감사 통과를 보장하지 않고 증거 수집/정리를 돕는다.

## 7. 암기 문장

- 감사 증거 자동 수집은 Audit Manager다.
- AWS compliance 보고서 다운로드는 Artifact다.

## 참고 링크

- [What is AWS Audit Manager?](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
