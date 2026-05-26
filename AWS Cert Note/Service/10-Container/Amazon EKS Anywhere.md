---
type: aws-service
service_name: "Amazon EKS Anywhere"
category: "10-Container"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["EKS Anywhere"]
tags: [aws, sap-c02, container, eks, kubernetes, hybrid]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon EKS Anywhere

> [!summary] 한 줄 요약
> 온프레미스/엣지 환경에서 EKS와 일관된 Kubernetes 클러스터를 고객이 직접 운영하도록 제공하는 배포/운영 도구다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | on-premises Kubernetes, customer-managed cluster lifecycle, VMware/bare metal/Nutanix/CloudStack/Snow, hybrid operations |
| 핵심 의사결정 | Kubernetes 표준을 온프레미스/엣지에서 유지해야 하고 고객이 인프라를 운영할 수 있으면 EKS Anywhere를 선택한다. |
| 대표 키워드 | on-premises, edge, Kubernetes, cluster lifecycle, disconnected/connected, customer-managed, EKS tooling |
| 자주 비교되는 서비스 | [[Amazon EKS]], [[Amazon EKS Distro]], [[Amazon ECS Anywhere]], [[AWS Outposts]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS 외부 인프라에 EKS 방식 Kubernetes 클러스터를 만들고 운영하는 소프트웨어/도구.
- **왜 쓰는가?**: 데이터센터/공장/엣지에 Kubernetes 워크로드를 두면서 AWS와 유사한 클러스터 운영 경험을 사용한다.
- **관리형 여부**: AWS Cloud EKS처럼 control plane을 AWS가 운영하지 않는다. 클러스터 lifecycle과 인프라 운영은 고객 책임이다.
- **범위/적용 위치**: VMware, bare metal, Nutanix, CloudStack, AWS Snow 등 지원 환경에서 사용한다.
- **핵심 제약/한계**: 관리형 서비스가 아니라 고객 관리 Kubernetes이므로 패치, 업그레이드, HA, 모니터링을 설계해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Cluster lifecycle tooling | 클러스터 생성/업그레이드/운영 도구 제공 | 온프레미스 K8s 표준화 |
| Supported platforms | VMware/bare metal/Nutanix/CloudStack/Snow 등 | 엣지/데이터센터 배포 단서 |
| AWS integrations | 선택적 관측성/ID/관리 연동 | 하이브리드 운영 |
| EKS Distro 기반 | EKS와 같은 Kubernetes 배포 구성요소 사용 | 호환성/일관성 단서 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EKS Anywhere]] | 온프레미스 고객 관리 Kubernetes | 로컬 K8s 실행 + EKS 일관성 | AWS가 control plane 운영한다고 오해 금지 |
| [[Amazon EKS]] | AWS Cloud 관리형 Kubernetes | AWS가 control plane 운영 | 온프레미스 로컬 실행 요구에는 부적합 |
| [[Amazon ECS Anywhere]] | ECS 모델 온프레미스 확장 | Kubernetes가 필요 없고 ECS 도구 선호 | K8s API/Helm/Operator 요구에는 부적합 |
| [[Amazon EKS Distro]] | K8s 배포판 | 직접 클러스터를 구성할 재료 | lifecycle 도구/운영 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/amazon-eks-hybrid-comparison.png]]

- EKS Anywhere는 온프레미스/엣지의 고객 관리 Kubernetes 영역에 위치한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 온프레미스 Kubernetes 표준화

- **요구사항**: 데이터센터에 K8s를 유지하면서 AWS와 운영 일관성 필요
- **정답 단서**: on-premises, Kubernetes, EKS tooling
- **선택할 구성**: EKS Anywhere
- **오답 함정**: AWS Cloud EKS가 온프레미스 control plane을 대신 운영한다고 가정

### 패턴 2: 엣지/공장 워크로드

- **요구사항**: 네트워크 지연과 데이터 위치 때문에 로컬 클러스터 필요
- **정답 단서**: edge, local cluster
- **선택할 구성**: EKS Anywhere on supported platform
- **오답 함정**: 리전 EKS만 사용

## 6. 헷갈리는 포인트

> [!warning] 주의
> Container 문제는 서비스 이름보다 **Kubernetes 필요 여부, 서버 관리 책임, 배포 위치, 이미지 저장소, 네트워크/권한 통합** 단서를 먼저 읽어야 한다.

- EKS Anywhere는 “Anywhere에서 AWS가 관리해주는 EKS”가 아니다. 고객 관리 클러스터다.
- EKS Distro는 구성요소 배포판이고 EKS Anywhere는 설치/운영 도구까지 포함한 선택지다.

## 7. 암기 문장

- 온프레미스 Kubernetes는 EKS Anywhere다.
- 관리형 control plane이 필요하면 AWS Cloud의 Amazon EKS다.

## 참고 링크

- [What is EKS Anywhere?](https://anywhere.eks.amazonaws.com/docs/)
- [EKS Anywhere concepts](https://anywhere.eks.amazonaws.com/docs/concepts/)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
