---
title: AWS CodePipeline
category: 11. Developer Tools
service: AWS CodePipeline
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - cicd
  - codepipeline
---

# AWS CodePipeline

> [!summary]
> **AWS CodePipeline**은 소스 변경부터 빌드, 테스트, 승인, 배포까지의 **CI/CD 흐름을 Stage와 Action으로 오케스트레이션**하는 완전관리형 서비스다. SAP-C02에서는 “파이프라인 흐름 조정” 역할과 CodeBuild/CodeDeploy/CodeArtifact와의 역할 분리가 핵심이다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| CI/CD 오케스트레이션 | 여러 단계의 source/build/test/deploy를 자동 연결해야 하면 CodePipeline |
| 승인 게이트 | 운영 배포 전 수동 승인 또는 별도 검증 단계가 필요하면 Manual approval action |
| 아티팩트 전달 | Stage 간 출력 아티팩트는 보통 S3 artifact store를 통해 전달 |
| 권한 모델 | Pipeline service role과 각 action provider 권한을 분리해서 최소 권한 설계 |
| 배포 서비스 선택 | CodePipeline은 배포 “흐름 조정”, 실제 배포 실행은 CodeDeploy/ECS/CloudFormation 등 |

## 1. 핵심 개념

- **Pipeline**: 전체 배포 자동화 흐름.
- **Stage**: Source, Build, Test, Deploy처럼 논리적으로 구분된 단계.
- **Action**: 각 Stage 안에서 실행되는 단위 작업. 예: GitHub 소스 수집, CodeBuild 실행, CodeDeploy 배포.
- **Artifact store**: Stage 간 입력/출력 파일을 저장하는 S3 버킷. 보안 요구사항이 있으면 KMS 암호화를 함께 고려한다.
- **Execution**: 소스 변경 또는 수동 실행으로 시작되는 파이프라인 1회 수행.

## 2. 주요 기능과 시험 포인트

### Stage / Action 기반 흐름 조정

CodePipeline은 여러 AWS 서비스와 외부 도구를 연결해 릴리스 흐름을 구성한다. 시험에서는 “빌드” 자체가 아니라 **빌드와 배포를 순서대로 연결하고 실패 시 중단/재시도/승인 흐름을 구성**하는 서비스로 구분한다.

### Manual approval

프로덕션 배포 전 Change Management, CAB 승인, 보안 승인 같은 사람이 개입하는 지점을 만들 수 있다. 승인 단계는 배포 자동화와 거버넌스를 함께 요구하는 시나리오에서 자주 등장한다.

### Event-driven pipeline

소스 변경 이벤트가 발생하면 파이프라인을 자동 시작할 수 있다. GitHub/Bitbucket/CodeCommit, S3 소스 아티팩트 등 다양한 소스 공급자를 사용할 수 있다.

### 보안 설계

- Pipeline service role에 필요한 action 권한만 부여한다.
- S3 artifact bucket은 암호화와 버킷 정책을 적용한다.
- Cross-account 배포는 artifact bucket, KMS key, 역할 신뢰 정책을 함께 설계한다.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| CI/CD 전체 단계 조정 | CodePipeline | Stage/Action으로 흐름을 연결 |
| 빌드/테스트 명령 실행 | CodeBuild | buildspec 기반 빌드 환경 실행 |
| EC2/Lambda/ECS 배포 전략 실행 | CodeDeploy | AppSpec, hooks, traffic shifting, rollback |
| 패키지 저장소 운영 | CodeArtifact | npm/Maven/pip/NuGet 패키지 저장 |
| 컨테이너 이미지 저장 | Amazon ECR | CodeArtifact가 아니라 ECR |
| 인프라 프로비저닝 배포 | CloudFormation / CDK | IaC 스택 생성/변경 실행 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-developer-tools-cicd-flow.png]]

1. 개발자가 소스 저장소에 변경을 push한다.
2. CodePipeline이 Source Stage에서 소스 아티팩트를 가져온다.
3. CodeBuild가 buildspec.yml에 따라 빌드/테스트를 실행한다.
4. 빌드 산출물 또는 패키지를 S3/CodeArtifact/ECR에 저장한다.
5. Manual approval이 있으면 승인 후 Deploy Stage로 진행한다.
6. CodeDeploy, ECS, CloudFormation 등이 실제 배포를 수행한다.
7. CloudWatch, X-Ray, CodeGuru/Amazon Q Developer 피드백으로 개선 루프를 만든다.

## 5. SAP-C02 시나리오 패턴

- “여러 계정/리전에 안전하게 배포하고 승인 단계를 넣어야 한다” → CodePipeline + cross-account role + KMS/S3 artifact 정책.
- “소스 변경 시 자동으로 빌드 후 ECS에 배포해야 한다” → CodePipeline + CodeBuild + ECS deploy action 또는 CodeDeploy blue/green.
- “운영 배포 전 사람이 승인해야 한다” → Manual approval action.
- “빌드만 수행하는 완전관리형 서비스” → CodeBuild이지 CodePipeline이 아니다.

## 6. 헷갈리는 포인트

- CodePipeline은 **오케스트레이터**다. 빌드 명령을 직접 실행하는 핵심 서비스는 CodeBuild다.
- CodePipeline은 실제 EC2/Lambda/ECS 배포 전략을 직접 구현하는 서비스가 아니라 CodeDeploy 등 배포 공급자를 호출한다.
- Artifact store는 애플리케이션 패키지 저장소가 아니다. npm/Maven 같은 패키지 관리는 CodeArtifact다.

## 7. 암기 문장

> **CodePipeline = CI/CD 흐름 조정자, CodeBuild = 빌더, CodeDeploy = 배포 실행자, CodeArtifact = 패키지 저장소.**

## 8. 참고 링크

- [AWS CodePipeline User Guide](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
- [AWS CodePipeline concepts](https://docs.aws.amazon.com/codepipeline/latest/userguide/concepts.html)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
