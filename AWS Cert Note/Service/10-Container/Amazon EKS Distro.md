---
type: aws-service
service_name: "Amazon EKS Distro"
category: "10-Container"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: low
aliases: ["EKS Distro", "EKS-D"]
tags: [aws, sap-c02, container, eks, kubernetes, distro]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon EKS Distro

> [!summary] 한 줄 요약
> Amazon EKS에서 사용하는 Kubernetes 구성요소와 패치를 기반으로 직접 Kubernetes 클러스터를 만들 수 있게 제공되는 배포판이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | Kubernetes distribution, upstream components, EKS-compatible components, self-managed cluster building block |
| 핵심 의사결정 | 관리형 서비스가 아니라 EKS와 일관된 Kubernetes 배포판이 필요할 때 EKS Distro를 이해한다. |
| 대표 키워드 | Kubernetes distribution, upstream Kubernetes, CoreDNS, kube-proxy, self-managed, build your own cluster |
| 자주 비교되는 서비스 | [[Amazon EKS]], [[Amazon EKS Anywhere]], [[Amazon ECS]], [[AWS Outposts]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: Amazon EKS가 사용하는 Kubernetes 구성요소를 오픈소스 배포판 형태로 제공하는 것.
- **왜 쓰는가?**: EKS와 유사한 구성요소로 자체 Kubernetes 클러스터를 구성하거나 검증된 배포판을 기반으로 삼기 위해 사용한다.
- **관리형 여부**: 관리형 서비스가 아니며 설치, 업그레이드, 운영, 보안, HA는 사용자 책임이다.
- **범위/적용 위치**: AWS, 온프레미스, 로컬 개발 등 사용자가 원하는 환경에 배포판 구성요소로 활용할 수 있다.
- **핵심 제약/한계**: EKS Distro만으로 cluster lifecycle 관리나 AWS support 수준의 managed EKS 운영이 제공되는 것은 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| EKS-aligned components | Kubernetes, CoreDNS, kube-proxy 등 EKS와 정렬된 구성요소 | 호환성/일관성 이해 |
| Open source distribution | 직접 다운로드/빌드 가능 | 자체 K8s 구성 재료 |
| Security patches | EKS 기준 패치/빌드 제공 | 검증된 구성요소 사용 |
| No managed control plane | 운영 자동화 없음 | 시험 오답 함정 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EKS Distro]] | Kubernetes 배포판 | 자체 클러스터 구성요소 필요 | 관리형 Kubernetes 서비스 아님 |
| [[Amazon EKS]] | AWS 관리형 Kubernetes | control plane 운영 위임 | Distro보다 운영 부담 낮음 |
| [[Amazon EKS Anywhere]] | 온프레미스 lifecycle 도구 | 온프레미스 클러스터 설치/운영 표준화 | Distro보다 상위 운영 도구 |
| [[Amazon ECS]] | Kubernetes가 아닌 AWS-native 오케스트레이션 | K8s 불필요한 컨테이너 운영 | Kubernetes 배포판과 무관 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/amazon-eks-hybrid-comparison.png]]

- EKS Distro는 EKS/EKS Anywhere의 기반이 되는 배포판이며 관리형 서비스가 아니다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 자체 Kubernetes 배포판 요구

- **요구사항**: 조직이 자체 플랫폼 위에 EKS와 정렬된 K8s 구성요소를 사용하고 싶음
- **정답 단서**: Kubernetes distribution, build your own
- **선택할 구성**: EKS Distro
- **오답 함정**: Amazon EKS처럼 AWS가 운영해준다고 가정

### 패턴 2: 관리형 K8s 운영 요구

- **요구사항**: control plane 운영 부담을 줄이고 싶음
- **정답 단서**: managed control plane
- **선택할 구성**: Amazon EKS
- **오답 함정**: EKS Distro만 선택

## 6. 헷갈리는 포인트

> [!warning] 주의
> Container 문제는 서비스 이름보다 **Kubernetes 필요 여부, 서버 관리 책임, 배포 위치, 이미지 저장소, 네트워크/권한 통합** 단서를 먼저 읽어야 한다.

- EKS Distro는 시험에서 자주 정답이기보다 EKS/EKS Anywhere와의 책임 경계 함정으로 나온다.
- 배포판은 운영 서비스가 아니다. 모니터링/업그레이드/보안은 직접 설계해야 한다.

## 7. 암기 문장

- EKS Distro는 배포판이다.
- 관리형 Kubernetes는 EKS, 온프레미스 lifecycle 도구는 EKS Anywhere다.

## 참고 링크

- [Amazon EKS Distro](https://distro.eks.amazonaws.com/)
- [EKS Distro GitHub](https://github.com/aws/eks-distro)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
