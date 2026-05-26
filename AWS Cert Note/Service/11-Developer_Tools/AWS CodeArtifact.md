---
title: AWS CodeArtifact
category: 11. Developer Tools
service: AWS CodeArtifact
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - package-repository
  - codeartifact
---

# AWS CodeArtifact

> [!summary]
> **AWS CodeArtifact**는 npm, Maven, pip, NuGet 같은 소프트웨어 패키지를 저장·공유·프록시하는 **완전관리형 패키지 저장소**다. SAP-C02에서는 “의존성 패키지 저장소”와 “컨테이너 이미지 저장소(ECR)”를 구분하는 것이 핵심이다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| 패키지 저장소 | npm/Maven/pip/NuGet 패키지 관리가 필요하면 CodeArtifact |
| Public upstream 프록시 | 외부 공개 저장소 의존성을 캐싱/통제하려면 upstream repository |
| 권한 제어 | IAM, domain policy, repository policy로 접근 제어 |
| CI/CD 연동 | CodeBuild가 CodeArtifact에서 dependency를 install/publish |
| ECR과 구분 | 컨테이너 이미지는 CodeArtifact가 아니라 Amazon ECR |

## 1. 핵심 개념

- **Domain**: 여러 repository를 묶는 최상위 경계. 계정 또는 조직 단위 패키지 공유 모델을 설계할 때 중요하다.
- **Repository**: 패키지 버전을 저장하고 upstream을 연결하는 단위.
- **Package version**: 특정 패키지의 특정 버전.
- **Upstream repository**: 요청한 패키지가 로컬에 없을 때 다른 CodeArtifact repo 또는 공개 저장소에서 가져오도록 연결한다.
- **Authorization token**: 패키지 매니저가 CodeArtifact에 접근할 때 사용하는 임시 인증 토큰.

## 2. 주요 기능과 시험 포인트

### 패키지 중앙화

조직 내 팀이 동일한 라이브러리를 재사용하고, 승인된 패키지만 사용하도록 통제할 수 있다. 의존성 공급망 보안과 빌드 재현성을 높이는 설계에 적합하다.

### Upstream / External connection

npmjs, Maven Central, PyPI, NuGet Gallery 같은 공개 저장소를 upstream으로 연결하면 외부 패키지를 캐싱하고 통제할 수 있다. 인터넷에서 매번 직접 내려받는 대신 중앙 정책과 감사 지점을 만들 수 있다.

### 권한과 정책

- IAM identity policy로 사용자/역할 권한을 제어한다.
- Domain/repository resource policy로 cross-account 공유를 제어한다.
- CI/CD에서는 CodeBuild service role에 `codeartifact:GetAuthorizationToken`, `ReadFromRepository`, `PublishPackageVersion` 같은 필요한 권한을 부여한다.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| npm/Maven/pip/NuGet 저장 | CodeArtifact | 언어별 패키지 저장소 |
| Docker/OCI 이미지 저장 | Amazon ECR | 컨테이너 레지스트리 |
| 빌드 실행 | CodeBuild | 패키지를 사용해 빌드 수행 |
| 릴리스 흐름 자동화 | CodePipeline | 패키지 publish/build/deploy 흐름 조정 |
| 객체 파일 저장 | Amazon S3 | 일반 파일/아티팩트 저장 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-developer-tools-supporting-services.png]]

1. 개발자 또는 CodeBuild가 CodeArtifact authorization token을 받는다.
2. 패키지 매니저가 CodeArtifact repository를 registry로 사용한다.
3. 내부 패키지를 publish하거나 외부 upstream 패키지를 install한다.
4. Repository policy와 IAM으로 팀/계정별 접근을 제한한다.
5. 빌드 결과는 CodePipeline 다음 단계로 전달되거나 애플리케이션에 포함된다.

## 5. SAP-C02 시나리오 패턴

- “여러 팀이 승인된 npm 패키지만 사용해야 한다” → CodeArtifact + upstream + repository policy.
- “빌드가 외부 인터넷 공개 저장소 장애에 영향을 덜 받아야 한다” → CodeArtifact 캐싱/프록시.
- “컨테이너 이미지를 저장해야 한다” → ECR. CodeArtifact가 아니다.
- “cross-account로 패키지를 공유해야 한다” → CodeArtifact domain/repository policy + IAM.

## 6. 헷갈리는 포인트

- CodeArtifact는 소스 저장소가 아니다. Git 저장소는 GitHub/Bitbucket/CodeCommit 계열이다.
- CodeArtifact는 컨테이너 이미지 레지스트리가 아니다. Docker image는 ECR이다.
- CodeArtifact 자체가 빌드를 실행하지 않는다. 빌드는 CodeBuild가 수행한다.

## 7. 암기 문장

> **CodeArtifact는 언어별 패키지 저장소, ECR은 컨테이너 이미지 저장소다.**

## 8. 참고 링크

- [AWS CodeArtifact User Guide](https://docs.aws.amazon.com/codeartifact/latest/ug/welcome.html)
- [CodeArtifact concepts](https://docs.aws.amazon.com/codeartifact/latest/ug/codeartifact-concepts.html)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
