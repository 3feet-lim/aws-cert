---
type: aws-service
service_name: "AWS Systems Manager"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["SSM", "Systems Manager", "Session Manager", "Parameter Store"]
tags: [aws, sap-c02, operations, automation]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Systems Manager

> [!summary] 한 줄 요약
> EC2, 온프레미스, 엣지 노드를 중앙에서 운영·자동화·패치·접속·인벤토리 관리하는 운영 허브다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 운영 자동화, 패치 관리, SSH 없는 접속, 하이브리드 노드 관리, runbook |
| 핵심 의사결정 | 여러 서버에 명령 실행, 패치, 세션 접속, 운영 자동화를 중앙에서 수행해야 하면 Systems Manager |
| 대표 키워드 | SSM Agent, managed node, Session Manager, Run Command, Patch Manager, Automation, Parameter Store |
| 자주 비교되는 서비스 | [[Amazon CloudWatch Logs]], [[AWS CloudTrail]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 관리 대상 노드와 AWS 리소스를 운영하는 도구 모음.
- **왜 쓰는가?**: bastion 없이 Session Manager로 접속하고, Run Command/Patch Manager/Automation으로 운영 작업을 표준화한다.
- **핵심 제약**: SSM Agent, IAM 권한, HTTPS 네트워크 경로 또는 VPC endpoint가 필요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Session Manager | 브라우저/CLI 기반 보안 세션 | inbound SSH/RDP 제거 |
| Run Command | 다수 노드 명령 실행 | 운영 작업 일괄 처리 |
| Patch Manager | 패치 기준과 유지보수 창 | 컴플라이언스/보안 패치 |
| Automation | runbook 자동화 | 반복 작업/복구 자동화 |
| Parameter Store | 구성값/암호 저장 | Secrets Manager와 비교 |
| Inventory/OpsCenter | 자산 정보와 운영 이슈 관리 | 운영 가시성 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-systems-manager-operations-hub.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| bastion 없이 EC2 접속 | Session Manager | SSH 22 inbound를 열 필요 없음 |
| 서버 패치/명령 자동화 | Systems Manager | CloudFormation은 인프라 프로비저닝 |
| 비밀 자동 rotation | Secrets Manager | Parameter Store SecureString과 구분 |
| 구성 규정 위반 탐지 | AWS Config | SSM은 조치 자동화와 운영 관리 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Systems Manager는 에이전트와 권한/네트워크 경로가 준비되어야 동작한다.

- Private subnet 노드는 NAT 또는 SSM VPC endpoints를 고려한다.
- Session Manager 로그는 CloudWatch Logs/S3로 남겨 감사 가능하게 한다.
- Hybrid activation으로 온프레미스 서버도 managed node로 등록할 수 있다.

## 6. 암기 문장

- 서버 운영 자동화와 bastion 대체는 Systems Manager다.
- 탐지는 Config/CloudWatch, 조치는 SSM Automation/Run Command로 연결한다.

## 참고 링크

- [What is AWS Systems Manager?](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)
- [Setting up AWS Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up-console.html)
