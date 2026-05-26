---
type: aws-service
service_name: "AWS CLI"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["AWS Command Line Interface", "CLI"]
tags: [aws, sap-c02, cli, automation]
created: 2026-05-26
updated: 2026-05-26
---

# AWS CLI

> [!summary] 한 줄 요약
> 터미널에서 AWS API를 호출해 리소스를 조회·관리·자동화하는 명령줄 도구다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 운영 자동화, 스크립팅, 임시 자격 증명, CloudTrail 감사 |
| 핵심 의사결정 | 반복 작업과 자동화를 터미널/CI에서 수행해야 하면 AWS CLI |
| 대표 키워드 | profiles, credentials, IAM role, STS, CloudShell, scripting |
| 자주 비교되는 서비스 | [[AWS Management Console]], [[AWS CloudTrail]], [[AWS Systems Manager]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS 서비스 API를 명령줄에서 호출하는 공식 도구.
- **왜 쓰는가?**: 반복 가능한 운영, 배포 스크립트, 진단, CI/CD 자동화에 사용한다.
- **핵심 제약**: 장기 access key보다 IAM Role, IAM Identity Center, STS 임시 자격 증명을 우선한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Profiles | 계정/역할별 설정 | 멀티계정 운영 |
| STS AssumeRole | 임시 자격 증명 | 장기 키 최소화 |
| Output/query | JSON 필터링 | 자동화와 리포팅 |
| CloudShell | 브라우저 기반 CLI | 로컬 설치/키 없이 실행 |
| CloudTrail 감사 | CLI 호출도 기록 | 운영 추적 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-access-license-governance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 반복 명령/자동화 | AWS CLI | 콘솔 클릭은 재현성이 낮음 |
| 대규모 서버 명령 실행 | Systems Manager Run Command | CLI는 제어 도구, 노드 실행 엔진은 SSM |
| 인프라 선언형 배포 | CloudFormation/CDK | CLI 스크립트만으로 drift 관리 어려움 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Console과 CLI는 같은 AWS API를 호출한다. 차이는 UI/자동화 방식이지 감사 원천이 다르지 않다.

- CI/CD에는 long-lived access key 대신 OIDC/role assumption을 고려한다.
- CLI 작업도 CloudTrail에 기록된다.
- 사람이 직접 반복 실행하는 CLI는 IaC보다 변경 통제가 약할 수 있다.

## 6. 암기 문장

- 자동화된 AWS API 호출은 CLI/SDK, 감사는 CloudTrail이다.
- 장기 키보다 Role/STS/SSO 기반 임시 자격 증명을 우선한다.

## 참고 링크

- [What is the AWS CLI?](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [AWS CLI configuration basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
