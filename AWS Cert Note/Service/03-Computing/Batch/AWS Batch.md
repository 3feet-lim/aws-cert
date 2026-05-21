---
type: aws-service
service_name: "AWS Batch"
category: "03-Computing/Batch"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: medium
aliases:
  - Batch
tags:
  - aws
  - sap-c02
  - compute
  - batch
created: 2026-05-20
updated: 2026-05-20
---

# AWS Batch

> [!summary] 한 줄 요약
> AWS Batch는 대규모 배치 작업을 큐에 넣고 ECS/EKS/Fargate/EC2 기반 컴퓨팅 리소스에 자동 스케줄링해 실행하는 관리형 배치 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 대규모 비동기 계산, HPC/분석/ML 전처리, 비용 최적화, Spot 활용 |
| 핵심 의사결정 | 작업 큐/우선순위/재시도/컴퓨팅 환경을 관리형으로 운영할 것인가 |
| 대표 키워드 | batch jobs, job queue, compute environment, containerized jobs, Spot, high-scale compute |
| 자주 비교되는 서비스 | [[AWS Lambda]], [[AWS Fargate]], [[Amazon EC2]], [[AWS Step Functions]], [[Amazon ECS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 작업 정의, 작업 큐, 컴퓨팅 환경을 기반으로 컨테이너화된 배치 작업을 스케줄링하고 실행하는 서비스.
- **왜 쓰는가?**: 사용자가 직접 배치 스케줄러와 클러스터를 운영하지 않고, 작업량에 따라 컴퓨팅 리소스를 자동 프로비저닝하기 위해 사용한다.
- **관리형/비관리형 여부**: Batch 스케줄링과 리소스 프로비저닝은 관리형이지만, 작업 컨테이너, 데이터 입출력, 재시도/의존성, IAM은 사용자가 설계한다.
- **리전/글로벌 서비스 여부**: 리전 서비스.
- **핵심 제약/한계**: 실시간 요청 처리 서비스가 아니라 큐 기반 비동기 작업에 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Job definition | 컨테이너 이미지, vCPU, 메모리, 명령 등 | 재현 가능한 배치 실행 단위다. |
| Job queue | 제출된 작업 대기열 | 우선순위와 compute environment 매핑이 중요하다. |
| Compute environment | EC2, Spot, Fargate, EKS 등 실행 용량 | 비용/성능/운영 요구에 따라 선택한다. |
| Managed compute environment | Batch가 용량을 자동 관리 | 인프라 운영 부담 제거가 핵심이다. |
| Retry/timeout | 실패 작업 재시도와 제한 | 중단 허용/오류 복구 배치에 필요하다. |
| Array jobs / dependencies | 대량 병렬 작업과 선후 관계 | HPC/대규모 분석 작업 패턴에 적합하다. |
| Spot 활용 | 중단 허용 작업 비용 절감 | checkpoint와 재시도 설계가 필요하다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Batch]] vs [[AWS Lambda]] | Batch는 컨테이너 기반 장기/대규모 작업, Lambda는 짧은 이벤트 함수 | 실행 시간이 길고 리소스가 큰 배치 작업은 Batch | 짧은 이벤트 처리까지 Batch로 만들면 지연과 운영이 과하다. |
| [[AWS Batch]] vs [[AWS Fargate]] | Fargate는 실행 엔진, Batch는 큐/스케줄러 | 작업 큐·우선순위·재시도·대량 스케줄링은 Batch | Fargate만으로는 배치 큐/의존성 관리가 부족할 수 있다. |
| [[AWS Batch]] vs [[Amazon EC2]] 직접 운영 | Batch가 스케줄러와 용량을 관리 | 클러스터 운영 없이 대량 작업이면 Batch | 특수 HPC 스케줄러/커스텀 클러스터는 EC2 직접 운영이 필요할 수 있다. |
| [[AWS Batch]] vs [[AWS Step Functions]] | Step Functions는 워크플로 오케스트레이션, Batch는 작업 실행/스케줄링 | 여러 서비스 단계 제어는 Step Functions, 대량 compute job은 Batch | 둘은 함께 사용할 수 있다. |

## 4. 설계 시 고려사항

- 데이터는 보통 S3/EFS/FSx/RDS 등 외부 저장소에 두고 작업은 stateless/재시도 가능하게 설계한다.
- Spot 기반 compute environment는 비용 최적화에 좋지만 중단을 전제로 checkpoint와 retry를 설계해야 한다.
- 작업 우선순위와 큐 분리는 팀/워크로드 간 자원 경합을 줄인다.
- 컨테이너 이미지는 ECR에 저장하고 IAM role로 데이터 접근 권한을 최소화한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 대규모 이미지/과학 계산 배치

- **요구사항**: 수천 개 작업을 병렬 실행하고 완료 후 결과 저장.
- **정답 단서**: batch jobs, queue, large-scale compute, no scheduler management.
- **선택할 구성**: AWS Batch + managed compute environment + S3/EFS 결과 저장.
- **오답 함정**: Lambda는 실행 시간/리소스 제약으로 장기 대규모 작업에 부적합할 수 있다.

### 패턴 2: 비용 최적화 배치

- **요구사항**: 중단 가능하고 마감 시간이 유연한 분석 작업 비용 최소화.
- **정답 단서**: fault tolerant, flexible, Spot, retry.
- **선택할 구성**: AWS Batch + Spot compute environment + retry/checkpoint.
- **오답 함정**: 중단 불가 작업을 Spot에만 두면 SLA를 만족하지 못한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> AWS Batch는 컨테이너 실행 서비스가 아니라 “배치 작업 스케줄링 + 컴퓨팅 환경 관리” 서비스다.

- ECS/EKS/Fargate/EC2는 Batch가 사용할 수 있는 실행 기반이다.
- 실시간 API 요청 처리에는 Batch가 아니라 Lambda/ECS/App Runner/API Gateway 계열을 검토한다.
- Spot 비용 절감은 자동 복구가 아니라 애플리케이션 재시도 가능성이 전제다.

## 7. 암기 문장

- 큐에 쌓이는 대규모 컨테이너 배치 작업은 AWS Batch다.
- Batch는 실행 엔진(Fargate/EC2/EKS)을 고르는 서비스가 아니라 작업 큐와 스케줄링을 관리하는 서비스다.

## 8. 참고 링크

- [What is AWS Batch?](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)
- [Components of AWS Batch](https://docs.aws.amazon.com/batch/latest/userguide/batch_components.html)
- [AWS Batch compute environments](https://docs.aws.amazon.com/batch/latest/userguide/compute_environments.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
