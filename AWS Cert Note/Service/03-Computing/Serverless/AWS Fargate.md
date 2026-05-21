---
type: aws-service
service_name: "AWS Fargate"
category: "03-Computing/Serverless"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: high
aliases:
  - Fargate
tags:
  - aws
  - sap-c02
  - compute
  - serverless
  - container
created: 2026-05-20
updated: 2026-05-20
---

# AWS Fargate

> [!summary] 한 줄 요약
> AWS Fargate는 ECS/EKS 컨테이너를 EC2 인스턴스 관리 없이 실행하게 해주는 서버리스 컨테이너 컴퓨팅 엔진이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 컨테이너 워크로드 운영 부담 감소, 마이크로서비스, 배치/장기 실행 컨테이너, 보안 격리 |
| 핵심 의사결정 | 컨테이너는 필요하지만 클러스터 EC2 노드 관리는 피하고 싶은가 |
| 대표 키워드 | serverless containers, ECS task, EKS pod, no EC2 management, task-level CPU/memory |
| 자주 비교되는 서비스 | [[AWS Lambda]], [[Amazon ECS]], [[Amazon EKS]], [[Amazon EC2]], [[AWS App Runner]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: ECS task 또는 EKS pod를 실행할 때 서버/노드 프로비저닝을 AWS가 대신 관리하는 컴퓨팅 엔진.
- **왜 쓰는가?**: 컨테이너 이미지와 태스크 정의에 집중하고, EC2 클러스터 패치/용량 관리 부담을 줄이기 위해 사용한다.
- **관리형/비관리형 여부**: 하부 인프라는 AWS가 관리하지만, 컨테이너 이미지, 태스크 리소스, 네트워크, IAM, 오토스케일링은 사용자가 설계한다.
- **리전/글로벌 서비스 여부**: 리전 서비스이며 ECS/EKS, VPC subnet/AZ와 함께 설계한다.
- **핵심 제약/한계**: 호스트 수준 커스터마이징, daemon, 특수 커널/스토리지 요구, 일부 네트워킹 요구에는 EC2 launch type이 더 적합할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| ECS Fargate task | 서버리스 컨테이너 실행 단위 | ECS에서 EC2 용량 관리 없이 서비스/태스크를 실행한다. |
| EKS on Fargate | EKS pod를 Fargate에서 실행 | Kubernetes 노드 관리 제거가 핵심이지만 모든 DaemonSet/노드 기능이 맞지는 않는다. |
| Task CPU/Memory | 태스크 단위 리소스 선택 | Lambda보다 컨테이너 리소스 제어가 명확하다. |
| awsvpc networking | 태스크가 ENI/IP를 가짐 | 보안 그룹과 subnet 설계가 컨테이너 단위로 중요하다. |
| IAM role for tasks | 태스크별 AWS 권한 | EC2 instance profile에 권한을 몰아주는 것보다 안전하다. |
| Fargate Spot | 중단 허용 태스크 비용 절감 | stateless/batch/비핵심 워크로드에 적합하다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Fargate]] vs [[AWS Lambda]] | Fargate는 컨테이너 태스크, Lambda는 함수 실행 | 장기 실행, 컨테이너 이미지, 세밀한 CPU/메모리 요구는 Fargate | 짧은 이벤트 처리를 Fargate 상시 서비스로 만들면 비용이 커질 수 있다. |
| [[AWS Fargate]] vs ECS on EC2 | Fargate는 노드 관리 제거, EC2 launch type은 호스트 제어 | 운영 부담 최소화는 Fargate, 특수 호스트 제어/비용 최적화는 EC2 | Fargate라고 컨테이너 설계/스케일링이 자동으로 완성되지는 않는다. |
| [[AWS Fargate]] vs [[AWS App Runner]] | App Runner는 웹앱 배포 추상화, Fargate는 ECS/EKS 런타임 | 컨테이너 오케스트레이션 제어가 필요하면 Fargate | 단순 웹 API 배포만이면 App Runner가 더 간단할 수 있다. |
| [[AWS Fargate]] vs [[Amazon EC2]] | Fargate는 서버리스 컨테이너, EC2는 VM 제어 | 컨테이너만 필요하고 OS 제어가 불필요하면 Fargate | 커널/에이전트/라이선스 제어는 EC2가 맞다. |

## 4. 설계 시 고려사항

- ECS Service Auto Scaling 또는 EKS scaling 설계가 필요하다. Fargate는 인프라 관리를 줄이지만 애플리케이션 스케일 정책을 자동으로 결정하지 않는다.
- private subnet에서 이미지를 pull하거나 AWS 서비스에 접근하려면 NAT Gateway 또는 VPC endpoint(ECR, CloudWatch Logs 등)를 고려한다.
- ALB/NLB와 연결해 서비스 트래픽을 분산하고 health check 기준을 명확히 설정한다.
- 상태 저장 컨테이너는 EFS 등 외부 스토리지와 복원 전략을 검토한다.

## 5. 비용 / 운영 포인트

- vCPU와 메모리로 과금되므로, 상시 실행 서비스는 리소스 요청을 과대 산정하면 비용이 증가한다.
- 중단 허용 워크로드는 Fargate Spot으로 비용을 줄일 수 있다.
- EC2 launch type은 큰 규모/높은 사용률에서 더 저렴할 수 있지만 노드 운영 부담이 생긴다.

## 6. SAP-C02 시나리오 패턴

### 패턴 1: 컨테이너 마이크로서비스 운영 부담 감소

- **요구사항**: 컨테이너 기반 서비스, EC2 패치/클러스터 용량 관리 제거.
- **정답 단서**: containers, no server management, microservices.
- **선택할 구성**: ECS Service on Fargate + ALB + Auto Scaling.
- **오답 함정**: Lambda는 컨테이너 이미지를 지원해도 함수 실행 모델이라 장기 실행 서비스에는 맞지 않을 수 있다.

### 패턴 2: 중단 허용 컨테이너 배치

- **요구사항**: 비용 절감, 재시도 가능한 컨테이너 작업.
- **정답 단서**: fault tolerant, batch, containers, cost optimization.
- **선택할 구성**: AWS Batch/ECS on Fargate Spot.
- **오답 함정**: 상태 저장 단일 작업을 Spot에 의존하면 중단 시 복구가 어렵다.

## 7. 헷갈리는 포인트

> [!warning] 주의
> Fargate는 컨테이너 서버리스이지 컨테이너 오케스트레이션 서비스 자체가 아니다. 보통 ECS/EKS와 함께 나온다.

- Fargate는 EC2 인스턴스를 직접 볼 필요가 없지만 VPC/subnet/security group은 여전히 중요하다.
- host-level daemon이나 특수 privileged 작업은 Fargate에 맞지 않을 수 있다.
- App Runner는 더 높은 수준의 웹앱 추상화이고, Fargate는 더 많은 컨테이너 제어를 제공한다.

## 8. 암기 문장

- 컨테이너는 필요하지만 EC2 노드는 관리하기 싫으면 Fargate다.
- 함수형 이벤트 처리면 Lambda, 웹앱 간편 배포면 App Runner, 호스트 제어면 ECS/EKS on EC2를 비교한다.

## 9. 참고 링크

- [AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html)
- [Amazon ECS on AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/what-is-fargate.html)
- [AWS Fargate or AWS Lambda?](https://docs.aws.amazon.com/decision-guides/latest/fargate-or-lambda/fargate-or-lambda.html)
- [AWS Fargate for Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/fargate.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
