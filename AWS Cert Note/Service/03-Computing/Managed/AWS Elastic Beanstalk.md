---
type: aws-service
service_name: "AWS Elastic Beanstalk"
category: "03-Computing/Managed"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: medium
aliases:
  - Elastic Beanstalk
  - Beanstalk
tags:
  - aws
  - sap-c02
  - compute
  - paas
created: 2026-05-20
updated: 2026-05-20
---

# AWS Elastic Beanstalk

> [!summary] 한 줄 요약
> AWS Elastic Beanstalk는 애플리케이션 코드를 업로드하면 EC2, Auto Scaling, Load Balancer 등 웹 애플리케이션 인프라를 자동 프로비저닝·관리하는 PaaS형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 빠른 웹 앱 배포, 개발자 생산성, 기존 코드 배포, 관리형 플랫폼과 인프라 제어의 균형 |
| 핵심 의사결정 | 서버리스까지 바꾸지 않고 EC2 기반 웹앱 운영 부담을 줄일 것인가 |
| 대표 키워드 | upload code, web environment, worker environment, managed platform, EC2/ALB/ASG provisioned |
| 자주 비교되는 서비스 | [[AWS App Runner]], [[Amazon EC2]], [[AWS Lambda]], [[Amazon ECS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker 등 애플리케이션을 배포하면 필요한 AWS 리소스를 구성하는 애플리케이션 관리 서비스.
- **왜 쓰는가?**: 인프라 세부 구성보다 애플리케이션 배포와 환경 관리에 집중하기 위해 사용한다.
- **관리형/비관리형 여부**: Beanstalk가 EC2/ALB/ASG/health monitoring을 구성하지만, 생성된 리소스는 사용자 계정에 있으며 설정을 조정할 수 있다.
- **리전/글로벌 서비스 여부**: 리전 서비스.
- **핵심 제약/한계**: 완전 서버리스가 아니며, 플랫폼 버전/EC2 리소스/네트워크/보안 업데이트 관리 이해가 필요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Application / Environment | 앱과 실행 환경 분리 | dev/test/prod 환경 관리와 배포 전략에 연결된다. |
| Web server environment | HTTP 요청 처리 환경 | ALB/ASG 기반 웹앱 빠른 배포에 적합하다. |
| Worker environment | SQS 메시지 기반 백그라운드 처리 | 비동기/장기 작업을 웹 요청과 분리하는 문제에 사용된다. |
| Platform | 언어/런타임/웹서버 조합 | 플랫폼 버전 유지와 업데이트가 운영 포인트다. |
| Deployment policies | all-at-once, rolling, immutable, blue/green 등 | 무중단/안전 배포 요구에서 중요하다. |
| Configuration | capacity, load balancer, VPC, env vars | 단순 서비스지만 인프라 설정을 조정할 수 있다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Elastic Beanstalk]] vs [[AWS App Runner]] | Beanstalk는 EC2 기반 환경 제어, App Runner는 더 추상화된 웹/컨테이너 서비스 | EC2/ALB/ASG 설정 제어가 필요하면 Beanstalk | 단순 컨테이너 웹 API는 App Runner가 더 간단할 수 있다. |
| [[AWS Elastic Beanstalk]] vs [[Amazon EC2]] | Beanstalk가 EC2 운영 구성을 자동화 | 빠른 앱 배포와 표준 환경이면 Beanstalk | OS/네트워크/배포 전체를 직접 제어해야 하면 EC2 직접 구성. |
| [[AWS Elastic Beanstalk]] vs [[AWS Lambda]] | Beanstalk는 서버 기반 웹앱, Lambda는 이벤트 함수 | 기존 웹 프레임워크를 그대로 배포하면 Beanstalk | 이벤트 기반 서버리스로 재설계 가능하면 Lambda/API Gateway가 운영 부담이 낮다. |
| [[AWS Elastic Beanstalk]] vs [[Amazon ECS]] | ECS는 컨테이너 오케스트레이션 제어, Beanstalk는 앱 플랫폼 | 컨테이너 클러스터 제어가 핵심이면 ECS | 단순 웹앱 배포만이면 ECS는 과할 수 있다. |

## 4. 설계 시 고려사항

- Beanstalk는 리소스를 숨기는 것이 아니라 생성/관리한다. VPC, 보안 그룹, ALB, ASG, RDS 연결을 이해해야 한다.
- 운영 환경은 Multi-AZ load-balanced 환경으로 구성하고, 단일 인스턴스 환경은 개발/테스트에 가깝다.
- Blue/green 배포는 별도 환경을 만들고 CNAME swap으로 전환하는 패턴이 자주 쓰인다.
- DB를 Beanstalk environment lifecycle에 묶으면 환경 삭제 시 위험할 수 있으므로 프로덕션 DB는 분리하는 것이 일반적이다.

## 5. 비용 / 운영 포인트

- Beanstalk 자체 추가 요금은 없고, EC2/ELB/RDS 등 하부 리소스 비용이 발생한다.
- 플랫폼 업데이트, 보안 패치, 인스턴스 타입/ASG 용량, 로그 수집, health 상태가 운영 포인트다.
- 단순 시작은 쉽지만 규모가 커지면 직접 생성된 리소스와 배포 정책을 이해해야 한다.

## 6. SAP-C02 시나리오 패턴

### 패턴 1: 기존 웹 앱 빠른 배포

- **요구사항**: Java/Python/Node 웹앱을 빠르게 AWS에 배포하고 자동 확장/로드밸런싱 사용.
- **정답 단서**: upload source code, managed web environment, minimal infrastructure management.
- **선택할 구성**: Elastic Beanstalk load-balanced environment.
- **오답 함정**: EC2를 수동 구성하면 요구된 운영 단순성을 놓친다.

### 패턴 2: 안전한 새 버전 배포

- **요구사항**: 장애 시 빠르게 롤백하고 다운타임 최소화.
- **정답 단서**: blue/green, immutable deployment, rollback.
- **선택할 구성**: Beanstalk immutable/blue-green deployment.
- **오답 함정**: all-at-once 배포는 빠르지만 장애 영향이 크다.

## 7. 헷갈리는 포인트

> [!warning] 주의
> Beanstalk는 완전 서버리스가 아니라 EC2 기반 애플리케이션 플랫폼이다.

- 생성된 AWS 리소스 비용과 보안 설정은 여전히 사용자 책임이다.
- RDS를 environment 안에 만들면 lifecycle coupling을 주의해야 한다.
- 컨테이너 지원이 있지만 ECS/Fargate 수준의 오케스트레이션 제어를 제공하는 서비스는 아니다.

## 8. 암기 문장

- “코드를 올리면 EC2/ALB/ASG 웹 환경을 자동 구성”하면 Elastic Beanstalk다.
- Beanstalk는 App Runner보다 제어가 많고, EC2 직접 구성보다 운영 부담이 낮다.

## 9. 참고 링크

- [What is AWS Elastic Beanstalk?](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
- [Elastic Beanstalk deployment policies and settings](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.deploy-existing-version.html)
- [AWS Elastic Beanstalk - deployment options](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/aws-elastic-beanstalk.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
