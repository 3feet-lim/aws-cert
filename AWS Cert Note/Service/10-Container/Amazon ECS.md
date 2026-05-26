---
type: aws-service
service_name: "Amazon ECS"
category: "10-Container"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["ECS", "Elastic Container Service"]
tags: [aws, sap-c02, container, ecs, orchestration]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon ECS

> [!summary] 한 줄 요약
> 컨테이너 애플리케이션을 AWS-native 방식으로 스케줄링하고 서비스로 운영하는 관리형 컨테이너 오케스트레이션 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | AWS-native container orchestration, Fargate/EC2 launch, service discovery, ALB 연동, task definition |
| 핵심 의사결정 | Kubernetes API가 필수는 아니고 AWS 통합과 운영 단순성이 중요하면 ECS를 우선 고려한다. |
| 대표 키워드 | task definition, service, cluster, Fargate, EC2 capacity provider, ALB, task role, service auto scaling |
| 자주 비교되는 서비스 | [[Amazon EKS]], [[AWS Fargate]], [[Amazon ECR]], [[AWS App Runner]], [[Amazon ECS Anywhere]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 컨테이너 Task를 클러스터에 배치하고 Service로 원하는 개수와 배포 상태를 유지하는 AWS 관리형 오케스트레이터.
- **왜 쓰는가?**: 컨테이너화된 웹/API/worker를 Kubernetes 운영 없이 ALB, IAM, CloudWatch, Service Auto Scaling과 통합해 운영한다.
- **관리형 여부**: ECS control plane은 AWS 관리형이고, 실행 용량은 Fargate(serverless) 또는 EC2/Auto Scaling으로 선택한다.
- **범위/적용 위치**: 리전 서비스이며 VPC 서브넷, 보안 그룹, ALB/NLB, Cloud Map 등 네트워크 설계와 함께 사용한다.
- **핵심 제약/한계**: Kubernetes API/CRD/Helm 생태계 요구가 강하면 EKS가 더 자연스럽다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Task Definition | 컨테이너 이미지, CPU/Memory, port, env, logging 정의 | 배포 단위와 실행 설정의 핵심 |
| Service | Task 수 유지, rolling/blue-green 배포, ALB 대상 등록 | 장기 실행 웹/API 워크로드 |
| Launch type / Capacity Provider | Fargate 또는 EC2 용량 선택 | 서버 관리 최소화는 Fargate, 인스턴스 제어/비용 최적화는 EC2 |
| IAM task role / execution role | 앱 권한과 이미지 Pull/로그 권한 분리 | 컨테이너에 access key 저장 금지 |
| Service Auto Scaling | CPU/Memory/ALB 요청 등 기반 확장 | 가변 트래픽 대응 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon ECS]] | AWS-native 컨테이너 오케스트레이션 | Kubernetes 불필요, AWS 통합/단순 운영 | Kubernetes 호환 요구에는 부적합 |
| [[Amazon EKS]] | 관리형 Kubernetes | K8s API, Helm, Operator, CNCF 생태계 필요 | 운영 복잡도와 비용이 ECS보다 클 수 있음 |
| [[AWS Fargate]] | 서버리스 컨테이너 실행 컴퓨트 | ECS Task/EKS Pod를 EC2 없이 실행 | 오케스트레이터 자체가 아님 |
| [[AWS App Runner]] | 웹 앱 완전관리형 배포 | 단순 HTTP 서비스 빠른 배포 | 복잡한 VPC/서비스 메시/배치에는 ECS/EKS |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-container-selection-map.png]]

- ECS는 컨테이너 오케스트레이션 선택지 중 AWS-native 운영 단순화 축에 위치한다.

![[attachments/aws/amazon-ecs-fargate-architecture.png]]

- Fargate 사용 시 Task는 Private Subnet에서 실행하고 ALB/NAT/VPC Endpoint/IAM/CloudWatch 통합을 설계한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: Kubernetes가 필요 없는 컨테이너 웹 서비스

- **요구사항**: ALB 뒤에서 여러 컨테이너 Task를 자동 확장하고 배포해야 함
- **정답 단서**: task definition, service, Fargate, ALB
- **선택할 구성**: ECS Service on Fargate + ALB
- **오답 함정**: EKS를 선택해 불필요한 Kubernetes 운영 복잡도 증가

### 패턴 2: EC2 기반 컨테이너 비용 최적화

- **요구사항**: 특정 인스턴스 타입/GPU/예약 용량을 직접 활용해야 함
- **정답 단서**: EC2 capacity provider, cluster auto scaling
- **선택할 구성**: ECS on EC2 Capacity Provider
- **오답 함정**: Fargate만 고집해 인스턴스 제어 요구를 충족 못함

## 6. 헷갈리는 포인트

> [!warning] 주의
> Container 문제는 서비스 이름보다 **Kubernetes 필요 여부, 서버 관리 책임, 배포 위치, 이미지 저장소, 네트워크/권한 통합** 단서를 먼저 읽어야 한다.

- ECS는 Fargate와 같은 뜻이 아니다. ECS는 오케스트레이터, Fargate는 실행 컴퓨트다.
- ECS Task Role과 Execution Role을 구분한다. 앱 AWS API 권한은 Task Role이다.
- Private Subnet의 Task가 ECR/CloudWatch/Secrets Manager에 접근하려면 NAT 또는 VPC Endpoint 설계가 필요하다.

## 7. 암기 문장

- AWS-native 컨테이너 운영 단순화는 ECS다.
- Kubernetes가 지문에 강하게 나오면 EKS와 비교한다.

## 참고 링크

- [What is Amazon ECS?](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
- [Amazon ECS task definitions](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definitions.html)
- [Amazon ECS services](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs_services.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
