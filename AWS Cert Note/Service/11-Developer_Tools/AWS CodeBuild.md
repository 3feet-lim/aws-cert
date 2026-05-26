---
title: AWS CodeBuild
category: 11. Developer Tools
service: AWS CodeBuild
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - cicd
  - codebuild
---

# AWS CodeBuild

> [!summary]
> **AWS CodeBuild**는 소스 코드를 컴파일하고 테스트를 실행하며 배포 가능한 아티팩트를 생성하는 **완전관리형 빌드 서비스**다. SAP-C02에서는 buildspec.yml, IAM/VPC/KMS, 캐시, Docker 빌드, CodePipeline 연동을 구분하는 문제가 자주 나온다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| 완전관리형 빌드 | 빌드 서버를 직접 운영하지 않고 빌드/테스트를 실행하려면 CodeBuild |
| buildspec.yml | install/pre_build/build/post_build 단계와 artifacts/reports/cache 정의 |
| Docker 이미지 빌드 | privileged mode, ECR 권한, Docker layer cache 고려 |
| 사설 리소스 접근 | VPC 설정으로 private subnet 내부 리소스 접근 |
| 보안 | Service role, Secrets Manager/SSM Parameter Store, KMS, CloudWatch Logs |

## 1. 핵심 개념

- **Build project**: 소스, 환경, 권한, buildspec, 로그, 아티팩트 설정을 묶는 단위.
- **Build environment**: AWS managed image 또는 custom Docker image를 사용하는 실행 환경.
- **buildspec.yml**: 빌드 명령, 아티팩트, 캐시, 리포트를 선언하는 YAML 파일.
- **Artifact**: 빌드 결과물. CodePipeline 연동 시 다음 Stage의 입력이 된다.
- **Reports**: 테스트 리포트와 코드 커버리지 결과를 수집할 수 있다.

## 2. 주요 기능과 시험 포인트

### buildspec 단계

- `install`: 런타임/의존성 준비
- `pre_build`: 로그인, 환경 변수 검증, 테스트 준비
- `build`: 컴파일, 단위 테스트, Docker build
- `post_build`: 이미지 push, 결과 정리, 메타데이터 생성

시험에서는 CodeDeploy의 AppSpec과 혼동시키는 보기가 자주 나온다. **빌드는 buildspec, 배포 hooks는 AppSpec**으로 기억한다.

### VPC 연결

CodeBuild 프로젝트를 VPC에 연결하면 private subnet의 RDS, ElastiCache, 내부 API 등에 접근할 수 있다. 단, 인터넷 패키지 다운로드가 필요하면 NAT Gateway 또는 VPC endpoint 설계가 필요하다.

### 보안과 비밀 관리

- 환경 변수에 평문 비밀을 직접 넣지 않는다.
- Secrets Manager 또는 SSM Parameter Store와 IAM 권한을 사용한다.
- 빌드 로그에 secret이 출력되지 않도록 명령과 마스킹을 주의한다.

### 캐시와 성능

소스 의존성 다운로드가 오래 걸리면 S3 cache 또는 local cache를 고려한다. 반복 빌드 시간을 줄이는 시나리오에서 비용/속도 최적화 포인트가 된다.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| 빌드/테스트 실행 | CodeBuild | 완전관리형 빌드 환경 |
| CI/CD 단계 연결 | CodePipeline | Source/Build/Deploy 흐름 조정 |
| EC2/Lambda/ECS 배포 | CodeDeploy | 배포 전략과 rollback |
| 패키지 의존성 저장 | CodeArtifact | npm/Maven/pip/NuGet 저장소 |
| 컨테이너 이미지 저장/배포 | ECR + ECS/EKS | 이미지는 CodeArtifact가 아니라 ECR |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-developer-tools-cicd-flow.png]]

1. CodePipeline 또는 개발자가 CodeBuild 프로젝트를 시작한다.
2. CodeBuild가 소스와 buildspec.yml을 읽는다.
3. Service role 권한으로 S3, ECR, Secrets Manager, CloudWatch Logs 등에 접근한다.
4. 빌드/테스트를 실행하고 아티팩트 또는 Docker 이미지를 생성한다.
5. 결과를 S3/ECR/CodeArtifact 또는 다음 Pipeline Stage로 전달한다.

## 5. SAP-C02 시나리오 패턴

- “Jenkins 빌드 서버 운영 부담을 줄이고 자동 확장되는 빌드가 필요하다” → CodeBuild.
- “빌드 중 private RDS에 접근해야 한다” → CodeBuild VPC 설정 + subnet/security group + NAT/VPC endpoint.
- “Docker 이미지를 빌드해 ECR에 push해야 한다” → CodeBuild privileged mode + ECR 권한.
- “패키지 다운로드 속도를 개선해야 한다” → CodeBuild cache 또는 CodeArtifact upstream/cache.

## 6. 헷갈리는 포인트

- CodeBuild는 배포 전략 서비스가 아니다. Blue/green, canary traffic shifting은 CodeDeploy/ECS/Lambda 배포 구성에서 판단한다.
- buildspec은 빌드 명령 정의이고 AppSpec은 CodeDeploy 배포 lifecycle hook 정의다.
- CodeBuild가 VPC 안에서 실행되면 인터넷 접근은 자동 보장되지 않는다.

## 7. 암기 문장

> **CodeBuild는 buildspec.yml로 빌드/테스트를 실행하는 완전관리형 빌더다.**

## 8. 참고 링크

- [AWS CodeBuild User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html)
- [Build specification reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
