---
type: aws-service
service_name: "AWS CloudFormation"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["CloudFormation", "CFN", "StackSets"]
tags: [aws, sap-c02, iac, deployment]
created: 2026-05-26
updated: 2026-05-26
---

# AWS CloudFormation

> [!summary] 한 줄 요약
> YAML/JSON 템플릿으로 AWS 리소스를 모델링하고 stack 단위로 일관되게 생성·변경·삭제하는 IaC 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | IaC, 반복 가능한 배포, change set, rollback, drift detection, StackSets |
| 핵심 의사결정 | 인프라를 코드로 정의하고 변경 추적/롤백/멀티계정 배포가 필요하면 CloudFormation |
| 대표 키워드 | template, stack, change set, rollback, drift detection, StackSets |
| 자주 비교되는 서비스 | [[AWS Service Catalog]], [[AWS Proton]], [[AWS CLI]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 템플릿에 원하는 리소스와 속성을 정의하면 CloudFormation이 의존성을 고려해 프로비저닝한다.
- **왜 쓰는가?**: 동일한 인프라를 여러 환경/리전에 반복 생성하고 변경을 버전 관리한다.
- **핵심 제약**: 이미 생성된 리소스 운영 작업은 Systems Manager, 승인된 self-service 배포는 Service Catalog와 비교한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Template | YAML/JSON 리소스 정의 | IaC 원천 |
| Stack | 리소스 집합 관리 단위 | 생성/업데이트/삭제 일관성 |
| Change Set | 적용 전 변경 미리보기 | 운영 변경 리스크 완화 |
| Rollback | 실패 시 이전 상태 복구 | 안정적 배포 |
| Drift detection | 실제 상태와 템플릿 차이 탐지 | 수동 변경 탐지 |
| StackSets | 멀티계정/리전 배포 | Organizations 환경 표준화 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-governed-iac-deployment-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| IaC 엔진 | CloudFormation | 승인 카탈로그 요구는 Service Catalog |
| End user self-service | Service Catalog | CloudFormation 직접 권한 부여는 과권한 위험 |
| 서버 명령/패치 | Systems Manager | CloudFormation은 리소스 프로비저닝 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> CloudFormation은 인프라 생성/변경 엔진이다. “승인된 제품만 사용자에게 배포 허용”은 Service Catalog가 더 직접적이다.

- Change Set으로 변경 전 영향 범위를 확인한다.
- Drift detection은 템플릿과 실제 상태 차이를 찾지만 모든 운영 문제를 해결하지는 않는다.
- StackSets는 멀티계정/멀티리전 표준 배포 단서다.

## 6. 암기 문장

- 코드로 인프라를 반복 생성하면 CloudFormation이다.
- 승인된 self-service 카탈로그는 Service Catalog 위에 CloudFormation/Terraform을 얹는다.

## 참고 링크

- [What is CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [How CloudFormation works](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-overview.html)
