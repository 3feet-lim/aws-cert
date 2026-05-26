---
type: aws-service
service_name: "AWS Management Console"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Console", "AWS Console"]
tags: [aws, sap-c02, console, operations]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Management Console

> [!summary] 한 줄 요약
> 웹 브라우저에서 AWS 서비스를 시각적으로 관리하는 기본 운영 인터페이스이며, 내부적으로 AWS API를 호출한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 운영자 접근 경로, IAM/MFA/SSO, CloudTrail 감사, break-glass |
| 핵심 의사결정 | 사람이 브라우저로 AWS 리소스를 관리해야 하면 Console, 자동화/반복 작업은 CLI/SDK/IaC |
| 대표 키워드 | web console, MFA, IAM Identity Center, CloudTrail, CloudShell |
| 자주 비교되는 서비스 | [[AWS CLI]], [[AWS CloudTrail]], [[AWS IAM Identity Center]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS 서비스 설정과 상태를 웹 UI로 관리하는 콘솔.
- **왜 쓰는가?**: 초기 탐색, 수동 운영, troubleshooting, 권한 검증에 유용하다.
- **핵심 제약**: 반복 가능성과 변경 통제는 CloudFormation/CLI/CI-CD가 더 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Web UI | 서비스별 설정과 대시보드 | 수동 운영/탐색 |
| IAM/MFA/SSO | 사용자 인증과 권한 | 사람 접근 보안 |
| CloudShell | 브라우저 기반 shell | 로컬 credential 없이 CLI 실행 |
| CloudTrail 기록 | Console 작업도 API 이벤트로 기록 | 감사/추적 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-access-license-governance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 수동 관리/탐색 | Management Console | 반복 배포를 콘솔 클릭으로 운영하면 drift 증가 |
| 자동화 스크립트 | AWS CLI/SDK | 콘솔은 자동화 인터페이스가 아님 |
| 감사 추적 | CloudTrail | 콘솔 자체가 감사 저장소는 아님 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Console과 CLI/SDK는 모두 AWS API를 호출하므로 CloudTrail 감사 대상이다.

- 루트 사용자 콘솔 사용은 최소화하고 MFA를 적용한다.
- 운영자는 IAM Identity Center/Role 기반 접근을 우선한다.
- 수동 변경은 IaC drift를 만들 수 있다.

## 6. 암기 문장

- Console은 사람용 AWS API 인터페이스, CLI/SDK는 자동화용 API 인터페이스다.
- 누가 콘솔에서 변경했는지는 CloudTrail로 추적한다.

## 참고 링크

- [AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)
- [What Is AWS CloudTrail?](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
