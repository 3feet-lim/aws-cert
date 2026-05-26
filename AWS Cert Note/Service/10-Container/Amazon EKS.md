---
type: aws-service
service_name: "Amazon EKS"
category: "10-Container"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["EKS", "Elastic Kubernetes Service"]
tags: [aws, sap-c02, container, eks, kubernetes]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon EKS

> [!summary] 한 줄 요약
> Kubernetes control plane을 AWS가 관리하고 AWS 네트워킹·IAM·스토리지와 통합해 Kubernetes 워크로드를 운영하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | managed Kubernetes, Kubernetes API, managed node groups, Fargate profile, hybrid nodes, CNCF ecosystem |
| 핵심 의사결정 | Kubernetes API/도구/운영 표준이 필수이면 EKS를 선택하고, 단순 AWS-native 컨테이너는 ECS와 비교한다. |
| 대표 키워드 | Kubernetes, control plane, managed node group, Fargate profile, IRSA, EBS CSI, ALB controller, Helm, Operator |
| 자주 비교되는 서비스 | [[Amazon ECS]], [[AWS Fargate]], [[Amazon EKS Anywhere]], [[Amazon EKS Distro]], [[Amazon ECR]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS가 Kubernetes control plane 가용성/운영을 관리하는 관리형 Kubernetes 서비스.
- **왜 쓰는가?**: Kubernetes API, Helm chart, Operator, 멀티클라우드/온프레미스 표준, CNCF 생태계를 AWS에서 사용하기 위해 선택한다.
- **관리형 여부**: Control plane은 AWS 관리형이며 worker는 Managed Node Groups, self-managed nodes, Fargate 등으로 선택한다.
- **범위/적용 위치**: 리전 서비스이며 VPC CNI, IAM, ALB/NLB, EBS/EFS, CloudWatch와 통합한다.
- **핵심 제약/한계**: Kubernetes 자체 운영 지식, 업그레이드, add-on, 보안 정책 설계 책임이 남는다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Managed control plane | API server/etcd 등 control plane 관리 | 고가용성 Kubernetes control plane 운영 부담 감소 |
| Managed Node Groups | EC2 worker node lifecycle 관리 | 노드 기반 workload와 DaemonSet/GPU 요구 |
| Fargate profiles | Pod를 서버리스로 실행 | 노드 관리 없이 Pod 실행하지만 DaemonSet 등 제약 확인 |
| IRSA / Pod Identity | Pod 단위 AWS IAM 권한 부여 | Access key 없이 AWS API 접근 |
| EKS add-ons | VPC CNI, CoreDNS, kube-proxy 등 관리 | 버전 호환성과 업그레이드 포인트 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EKS]] | 관리형 Kubernetes | K8s 생태계/호환성/표준화 요구 | 단순 컨테이너에는 과도할 수 있음 |
| [[Amazon ECS]] | AWS-native 오케스트레이션 | Kubernetes 불필요, 운영 단순성 | K8s API/Operator 요구 충족 못함 |
| [[Amazon EKS Anywhere]] | 온프레미스/엣지 K8s 클러스터 | 데이터센터에서 EKS 방식 운영 | AWS 관리형 control plane이 아님 |
| [[Amazon EKS Distro]] | K8s 배포판 | 직접 호환 클러스터 구성 | 관리형 서비스/운영 자동화 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-container-selection-map.png]]

- EKS는 Kubernetes API/CNCF 생태계가 선택 단서일 때 ECS와 구분한다.

![[attachments/aws/amazon-eks-hybrid-comparison.png]]

- EKS, EKS Anywhere, EKS Distro는 관리 책임과 배포 위치가 다르다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: Kubernetes 표준 플랫폼

- **요구사항**: 기존 Helm/Operator 기반 앱을 AWS에서 운영
- **정답 단서**: Kubernetes API, managed control plane
- **선택할 구성**: Amazon EKS + Managed Node Groups 또는 Fargate
- **오답 함정**: ECS로 옮겨 Kubernetes 종속 도구를 재작성

### 패턴 2: Pod별 AWS 권한

- **요구사항**: 앱 Pod가 S3/DynamoDB에 최소 권한 접근 필요
- **정답 단서**: IRSA, service account, IAM role
- **선택할 구성**: EKS Pod Identity/IRSA
- **오답 함정**: 노드 IAM Role에 과도한 권한 부여

## 6. 헷갈리는 포인트

> [!warning] 주의
> Container 문제는 서비스 이름보다 **Kubernetes 필요 여부, 서버 관리 책임, 배포 위치, 이미지 저장소, 네트워크/권한 통합** 단서를 먼저 읽어야 한다.

- EKS는 Kubernetes control plane을 관리하지만 클러스터 add-on, workload 보안, node 운영 책임은 설계에 남는다.
- Fargate profile은 EKS에서도 쓰지만 모든 Kubernetes 워크로드에 무조건 맞지는 않는다.
- EKS Anywhere와 EKS Distro는 AWS Cloud의 관리형 EKS와 운영 책임이 다르다.

## 7. 암기 문장

- Kubernetes가 요구사항이면 EKS다.
- AWS가 control plane을 관리하지만 Kubernetes 운영 책임이 0은 아니다.

## 참고 링크

- [What is Amazon EKS?](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)
- [Amazon EKS nodes](https://docs.aws.amazon.com/eks/latest/userguide/eks-compute.html)
- [IAM roles for service accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
