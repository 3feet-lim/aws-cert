---
type: aws-service
service_name: "AWS App Runner"
category: "03-Computing/Managed"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
status: draft
priority: medium
aliases:
  - App Runner
tags:
  - aws
  - sap-c02
  - compute
  - container
  - managed
created: 2026-05-20
updated: 2026-05-20
---

# AWS App Runner

> [!summary] 한 줄 요약
> AWS App Runner는 소스 코드나 컨테이너 이미지에서 확장 가능한 HTTPS 웹 애플리케이션/API를 인프라 경험 없이 바로 배포하는 완전관리형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 컨테이너/웹 API 빠른 배포, 운영 부담 최소화, 자동 빌드/배포 |
| 핵심 의사결정 | 복잡한 ECS/EKS 제어 없이 웹 서비스만 빠르게 운영할 것인가 |
| 대표 키워드 | source code to web app, container image, fully managed web service, automatic deployment, HTTPS endpoint |
| 자주 비교되는 서비스 | [[AWS Elastic Beanstalk]], [[AWS Fargate]], [[Amazon ECS]], [[AWS Lambda]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: GitHub/source repository 또는 ECR 컨테이너 이미지에서 웹 애플리케이션과 API 서비스를 빌드·배포·확장하는 관리형 서비스.
- **왜 쓰는가?**: 컨테이너/인프라/오케스트레이션 세부 지식 없이 웹 서비스 배포와 운영을 단순화하기 위해 사용한다.
- **관리형/비관리형 여부**: 빌드/배포/로드밸런싱/스케일링/HTTPS endpoint를 관리형으로 제공하지만, 앱 코드·이미지·환경 변수·보안 설정은 사용자가 관리한다.
- **리전/글로벌 서비스 여부**: 리전 서비스.
- **핵심 제약/한계**: 일반-purpose 컨테이너 오케스트레이션이 아니라 웹 요청을 처리하는 서비스에 초점이 있다. 복잡한 service mesh/daemon/세밀한 네트워크 제어는 ECS/EKS가 더 적합할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Source deployment | 코드 저장소에서 빌드/배포 | 개발자 중심 빠른 웹앱 배포 요구에 맞다. |
| Image deployment | ECR 이미지에서 서비스 실행 | 컨테이너 이미지는 있지만 ECS를 직접 운영하고 싶지 않을 때. |
| Auto deployments | repo/image 변경 시 자동 배포 | CI/CD 단순화 단서가 된다. |
| Managed HTTPS endpoint | 외부 접속 가능한 웹 endpoint | ALB/API Gateway 직접 구성 없이 공개 웹서비스 제공. |
| Auto scaling | 요청 부하에 따른 확장 | 세부 scaling 제어보다 간단한 운영이 핵심이다. |
| VPC connector | private VPC 리소스 접근 | RDS 등 private backend 접근 시 네트워크 설계를 확인한다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS App Runner]] vs [[AWS Elastic Beanstalk]] | App Runner는 더 추상화된 웹서비스, Beanstalk는 EC2 기반 환경 제어 | 소스/컨테이너에서 웹 API를 빠르게 배포하면 App Runner | EC2/ALB/ASG 세밀 제어가 필요하면 Beanstalk/EC2. |
| [[AWS App Runner]] vs [[AWS Fargate]] | Fargate는 ECS/EKS 태스크 런타임, App Runner는 웹서비스 플랫폼 | 단순 HTTPS 웹서비스면 App Runner | 복잡한 마이크로서비스 오케스트레이션/서비스 간 제어는 ECS/Fargate. |
| [[AWS App Runner]] vs [[AWS Lambda]] | App Runner는 지속 웹 프로세스, Lambda는 이벤트 함수 | 컨테이너 웹 서버나 지속 API 프로세스면 App Runner | 짧은 이벤트 기반 처리에는 Lambda가 더 비용 효율적일 수 있다. |
| [[AWS App Runner]] vs [[Amazon ECS]] | ECS는 클러스터/서비스/태스크 제어 | 컨테이너 운영 제어보다 빠른 배포가 목표면 App Runner | 여러 내부 서비스/배치/네트워크 제어에는 ECS가 낫다. |

## 4. 언제 사용하는가

- 웹 애플리케이션/API를 소스나 컨테이너 이미지에서 빠르게 공개 HTTPS 서비스로 배포해야 할 때.
- 운영팀이 ECS/EKS/ALB/Auto Scaling 세부 구성을 직접 관리하고 싶지 않을 때.
- 소규모~중간 규모 웹서비스에서 배포 단순성과 자동화를 우선할 때.

## 5. 언제 사용하지 않는가

- 비웹 배치 작업, 복잡한 컨테이너 오케스트레이션, daemon/sidecar 제어, 세밀한 VPC/로드밸런싱 설계가 핵심일 때.
- 이벤트 기반 짧은 처리에는 Lambda가 더 자연스럽다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> App Runner는 “컨테이너를 쉽게 웹서비스로 배포”하는 서비스이지 ECS/EKS 전체 대체재가 아니다.

- 웹 요청 처리 서비스에 초점이 있으므로 일반 배치/워크플로 오케스트레이션 서비스로 보지 않는다.
- VPC connector는 private 리소스 접근용이며, 전체 네트워크 설계가 사라지는 것은 아니다.
- 컨테이너 이미지만 있으면 무조건 Fargate가 아니라, 웹서비스 단순 배포면 App Runner가 더 맞을 수 있다.

## 7. 암기 문장

- “소스/이미지에서 바로 HTTPS 웹 앱”이면 App Runner다.
- 더 많은 컨테이너 제어는 Fargate/ECS, EC2 기반 플랫폼 제어는 Beanstalk, 이벤트 함수는 Lambda와 비교한다.

## 8. 참고 링크

- [What is AWS App Runner?](https://docs.aws.amazon.com/apprunner/latest/dg/what-is-apprunner.html)
- [AWS App Runner - deployment options](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/aws-apprunner.html)
- [App Runner VPC access](https://docs.aws.amazon.com/apprunner/latest/dg/network-vpc.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
