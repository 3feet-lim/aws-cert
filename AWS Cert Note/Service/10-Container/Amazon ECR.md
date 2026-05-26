---
type: aws-service
service_name: "Amazon ECR"
category: "10-Container"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["ECR", "Elastic Container Registry"]
tags: [aws, sap-c02, container, registry, ecr]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon ECR

> [!summary] 한 줄 요약
> 컨테이너 이미지를 저장·스캔·복제·수명주기 관리하는 AWS 관리형 컨테이너 이미지 레지스트리다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | container image registry, private/public repository, vulnerability scanning, lifecycle policy, cross-Region replication |
| 핵심 의사결정 | ECS/EKS/App Runner/Lambda 컨테이너 이미지의 안전한 저장소와 배포 경로가 필요하면 ECR을 선택한다. |
| 대표 키워드 | container image, repository, image scanning, lifecycle policy, replication, pull through cache, private registry |
| 자주 비교되는 서비스 | [[Amazon ECS]], [[Amazon EKS]], [[AWS Fargate]], [[Amazon S3]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Docker/OCI 컨테이너 이미지를 저장하는 완전관리형 private/public registry.
- **왜 쓰는가?**: 컨테이너 이미지를 IAM으로 보호하고 ECS/EKS/Lambda/App Runner가 안정적으로 pull하게 한다.
- **관리형 여부**: 레지스트리 인프라는 AWS 관리형이며 repository policy, lifecycle, scanning, replication 설정은 사용자 책임이다.
- **범위/적용 위치**: 리전 단위 private registry가 기본이며 cross-Region/account replication과 public gallery 용도도 고려한다.
- **핵심 제약/한계**: ECR은 이미지를 실행하지 않는다. 실행은 ECS/EKS/Fargate/App Runner가 담당한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Private repository | 계정/리전별 이미지 저장소 | IAM 기반 pull/push 제어 |
| Image scanning | 기본/향상된 취약점 스캔 | 컨테이너 공급망 보안 단서 |
| Lifecycle policy | 오래된 tag/image 정리 | 스토리지 비용과 repository 위생 |
| Replication | 리전/계정 간 이미지 복제 | DR/멀티리전 배포 속도 |
| Pull through cache | 외부 public registry 캐시 | 빌드 안정성과 rate limit 완화 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon ECR]] | 컨테이너 이미지 저장소 | 이미지 저장/스캔/복제/배포 | 오케스트레이션/실행 서비스가 아님 |
| [[Amazon ECS]] | 컨테이너 실행/오케스트레이션 | Task/Service 운영 | 이미지 저장은 ECR |
| [[Amazon EKS]] | Kubernetes 실행 플랫폼 | Pod 이미지 pull 대상 중 하나 | 레지스트리 기능과 구분 |
| [[Amazon S3]] | 객체 저장소 | 일반 파일/아티팩트 저장 | 컨테이너 registry API 제공 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-container-selection-map.png]]

- ECR은 ECS/EKS와 같은 실행 플랫폼이 아니라 이미지 저장·배포·스캔 축이다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 멀티리전 컨테이너 배포

- **요구사항**: 각 리전 ECS/EKS가 로컬에서 이미지를 빠르게 pull해야 함
- **정답 단서**: cross-Region replication, repository
- **선택할 구성**: ECR replication
- **오답 함정**: S3에 tar 파일 저장 후 수동 배포

### 패턴 2: 이미지 취약점 관리

- **요구사항**: 배포 전 컨테이너 이미지 CVE 확인 필요
- **정답 단서**: image scanning, Inspector integration
- **선택할 구성**: ECR image scanning / enhanced scanning
- **오답 함정**: 런타임 GuardDuty만 사용

## 6. 헷갈리는 포인트

> [!warning] 주의
> Container 문제는 서비스 이름보다 **Kubernetes 필요 여부, 서버 관리 책임, 배포 위치, 이미지 저장소, 네트워크/권한 통합** 단서를 먼저 읽어야 한다.

- ECR은 컨테이너 런타임이 아니라 registry다.
- Private Subnet의 ECS/EKS가 ECR에 접근하려면 NAT 또는 ECR VPC endpoint 경로를 설계한다.
- 태그 latest만 의존하면 재현성과 롤백이 어려우므로 immutable tag 전략을 고려한다.

## 7. 암기 문장

- 컨테이너 이미지 저장소는 ECR이다.
- ECS/EKS는 실행, ECR은 저장/스캔/복제다.

## 참고 링크

- [What is Amazon ECR?](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
- [Image scanning in Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)
- [Private registry settings](https://docs.aws.amazon.com/AmazonECR/latest/userguide/registry-settings.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
