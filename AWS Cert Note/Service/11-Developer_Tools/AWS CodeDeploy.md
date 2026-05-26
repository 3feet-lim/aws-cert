---
title: AWS CodeDeploy
category: 11. Developer Tools
service: AWS CodeDeploy
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - deployment
  - codedeploy
---

# AWS CodeDeploy

> [!summary]
> **AWS CodeDeploy**는 EC2/온프레미스, Lambda, ECS 애플리케이션 배포를 자동화하고 배포 상태, 트래픽 전환, rollback을 관리하는 서비스다. SAP-C02에서는 CodeBuild와 혼동하지 않고 **배포 대상별 전략과 AppSpec/hooks**를 구분하는 것이 중요하다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| EC2/On-prem 배포 | CodeDeploy agent, deployment group, AppSpec hooks |
| Lambda 배포 | Alias 기반 canary/linear/all-at-once traffic shifting |
| ECS 배포 | Blue/green task set, ALB listener/target group, rollback |
| 자동 rollback | CloudWatch alarms 또는 배포 실패 기준으로 중단/rollback |
| 빌드와 구분 | CodeDeploy는 빌드 서비스가 아니라 배포 자동화 서비스 |

## 1. 핵심 개념

- **Application**: 배포 대상 애플리케이션의 논리 단위.
- **Deployment group**: 배포할 EC2 인스턴스, Auto Scaling Group, Lambda alias, ECS service 등을 묶은 대상 그룹.
- **Revision**: 배포할 애플리케이션 버전. S3, GitHub, Bitbucket 등에서 가져올 수 있다.
- **AppSpec file**: 배포 대상, 파일 복사, lifecycle hooks를 정의한다.
- **Deployment configuration**: all-at-once, rolling, canary, linear, blue/green 등 배포 방식.

## 2. 주요 기능과 시험 포인트

### EC2 / On-premises

EC2와 온프레미스 서버에는 CodeDeploy agent가 필요하다. AppSpec hooks를 통해 `BeforeInstall`, `AfterInstall`, `ApplicationStart`, `ValidateService` 같은 lifecycle 단계에서 스크립트를 실행할 수 있다.

### Lambda

Lambda 배포에서는 alias를 사용해 새 버전으로 트래픽을 점진 이동한다. Canary 또는 linear 배포 중 CloudWatch alarm이 발생하면 배포를 중단하거나 rollback할 수 있다.

### Amazon ECS

ECS blue/green 배포에서는 기존 blue task set과 신규 green task set을 만들고 ALB listener/target group을 사용해 트래픽을 전환한다. 운영 트래픽 전환 전 테스트 listener로 검증하는 패턴도 중요하다.

### 자동 rollback

배포 실패, alarm 발생, health check 실패 시 자동 rollback을 구성할 수 있다. 고가용성 시나리오에서 “문제 발생 시 빠르게 이전 안정 버전으로 되돌리기” 요구에 적합하다.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| 빌드/테스트 실행 | CodeBuild | buildspec 기반 빌드 |
| 배포 전략과 rollback | CodeDeploy | AppSpec/hooks, traffic shifting |
| 전체 CI/CD 흐름 | CodePipeline | CodeBuild/CodeDeploy를 연결 |
| ECS 기본 rolling update | ECS service deployment | 단순 rolling이면 ECS 자체 기능 가능 |
| ECS blue/green 고급 제어 | CodeDeploy + ECS | ALB target group 기반 트래픽 전환 |
| Lambda canary 배포 | CodeDeploy + Lambda alias | 점진 트래픽 이동과 alarm rollback |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-codedeploy-deployment-strategy.png]]

1. CodePipeline 또는 사용자가 CodeDeploy deployment를 시작한다.
2. CodeDeploy가 revision과 AppSpec을 읽는다.
3. 배포 대상별로 agent, Lambda alias, ECS task set을 사용한다.
4. Lifecycle hook 또는 traffic shifting으로 검증 지점을 둔다.
5. CloudWatch alarm/health check 실패 시 배포를 중단하거나 rollback한다.

## 5. SAP-C02 시나리오 패턴

- “EC2 Auto Scaling Group에 무중단 또는 rolling 배포를 해야 한다” → CodeDeploy deployment group + ASG + ELB.
- “Lambda 새 버전을 10% 트래픽부터 점진 배포하고 실패 시 rollback” → CodeDeploy canary/linear + CloudWatch alarm.
- “ECS에서 blue/green 배포와 트래픽 전환” → CodeDeploy ECS deployment + ALB target groups.
- “빌드 스크립트를 정의해야 한다” → CodeBuild buildspec이지 CodeDeploy AppSpec이 아니다.

## 6. 헷갈리는 포인트

- CodeDeploy는 빌드하지 않는다. 빌드 산출물을 **어떻게 배포할지** 관리한다.
- EC2/온프레미스 배포에는 agent와 인스턴스 권한이 중요하다.
- Lambda/ECS는 트래픽 전환이 핵심이고, EC2는 인스턴스 lifecycle hook과 agent 동작이 핵심이다.

## 7. 암기 문장

> **CodeDeploy = AppSpec/hooks + 대상별 배포 전략 + CloudWatch alarm rollback.**

## 8. 참고 링크

- [AWS CodeDeploy User Guide](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html)
- [CodeDeploy AppSpec files](https://docs.aws.amazon.com/codedeploy/latest/userguide/application-specification-files.html)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
