---
type: aws-service
service_name: "Amazon EC2"
category: "03-Computing/Virtual Machine"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
  - "4. 마이그레이션/현대화"
status: draft
priority: high
aliases:
  - EC2
  - Amazon Elastic Compute Cloud
tags:
  - aws
  - sap-c02
  - compute
  - virtual-machine
created: 2026-05-20
updated: 2026-05-20
---

# Amazon EC2

> [!summary] 한 줄 요약
> Amazon EC2는 인스턴스 유형·구매 옵션·스토리지·네트워크를 직접 조합해 가장 세밀하게 제어할 수 있는 AWS 기본 가상 서버 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 신규 워크로드 배치, 기존 서버 마이그레이션, 비용 최적화, HA/DR, 성능 튜닝 |
| 핵심 의사결정 | 서버 제어가 필요한가, 어떤 인스턴스 패밀리/구매 옵션/스토리지/네트워크 구성이 요구사항에 맞는가 |
| 대표 키워드 | full control, custom OS, lift-and-shift, instance family, AMI, EBS, Spot, Reserved Instance, Savings Plans |
| 자주 비교되는 서비스 | [[AWS Lambda]], [[AWS Fargate]], [[AWS Elastic Beanstalk]], [[Amazon Lightsail]], [[AWS Outposts]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS에서 제공하는 크기 조정 가능한 가상 서버. AMI로 부팅하고, 인스턴스 타입/스토리지/네트워크/보안 그룹을 선택한다.
- **왜 쓰는가?**: OS, 런타임, 에이전트, 네트워크, 라이선스, 성능 특성을 세밀하게 제어해야 할 때 사용한다.
- **관리형/비관리형 여부**: 물리 인프라는 AWS가 관리하지만, 게스트 OS 패치·애플리케이션·용량 설계는 사용자가 책임진다.
- **리전/글로벌 서비스 여부**: 인스턴스는 AZ 단위 리소스이며, AMI/EBS/ENI/보안 그룹 등은 리전 또는 AZ 범위 제약을 가진다.
- **핵심 제약/한계**: 단일 인스턴스는 장애 지점이므로 Auto Scaling, Load Balancer, Multi-AZ 배치, 백업/복구 설계가 필요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| AMI | 인스턴스 부팅 이미지 | 표준 이미지, golden AMI, 계정/리전 복사, 패치 표준화와 연결된다. |
| Instance type | vCPU, 메모리, 스토리지, 네트워크 성능 조합 | compute/memory/storage/GPU 최적화 요구사항을 패밀리 선택으로 매칭한다. |
| EBS-backed instance | 영구 블록 스토리지 사용 | 중지/시작 가능, 스냅샷 기반 백업, 볼륨 타입 선택이 시험 포인트다. |
| Instance store | 호스트 로컬 임시 스토리지 | 고성능 임시 데이터용. 중지/종료/호스트 장애 시 데이터 보존을 기대하면 안 된다. |
| Security Group | ENI 수준 stateful 방화벽 | 인스턴스 접근 제어의 기본. deny가 필요하면 NACL 등 다른 수단을 검토한다. |
| Placement group | 인스턴스 배치 전략 | cluster는 low latency/HPC, spread는 장애 격리, partition은 대규모 분산 시스템에 맞다. |
| User data | 부팅 시 초기화 스크립트 | 자동 구성에는 유용하지만 장기 구성 관리는 SSM/이미지 파이프라인이 더 적합할 수 있다. |
| EC2 Fleet / Spot Fleet | 여러 타입·구매 옵션 조합 | 용량 유연성과 비용 최적화 요구에서 Spot/On-Demand 조합이 출제된다. |

## 3. 구매 옵션 / 비용 선택 기준

| 옵션 | 선택 기준 | 오답 함정 |
|---|---|---|
| On-Demand | 예측 어려운 단기 워크로드, 약정 없이 시작 | 장기 상시 실행에는 비용이 높다. |
| Savings Plans | 일정 사용량을 약정하고 유연하게 할인 | 인스턴스 예약과 다르게 사용량 약정이라는 점을 구분한다. |
| Reserved Instances | 특정 인스턴스 패밀리/리전/AZ 용량·할인 요구 | 유연성은 Savings Plans보다 제한적일 수 있다. |
| Spot Instances | 중단 허용, stateless, batch, CI, 분석 작업 | 언제든 중단될 수 있으므로 체크포인트/재시도/분산 설계가 필요하다. |
| Dedicated Hosts | 라이선스/규정 준수, 물리 서버 단위 제어 | 일반 비용 절감용이 아니라 라이선스·격리 요구용이다. |

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EC2]] vs [[AWS Lambda]] | EC2는 서버 제어, Lambda는 이벤트 기반 함수 | OS/에이전트/장기 실행/특수 런타임이 필요하면 EC2 | 짧은 이벤트 작업에 EC2를 직접 운영하면 운영 부담이 과하다. |
| [[Amazon EC2]] vs [[AWS Fargate]] | EC2는 서버 운영, Fargate는 컨테이너 서버리스 런타임 | 컨테이너만 필요하고 호스트 제어가 불필요하면 Fargate | Fargate에서도 VPC/보안/태스크 리소스 설계는 필요하다. |
| [[Amazon EC2]] vs [[AWS Elastic Beanstalk]] | Beanstalk가 EC2/ALB/ASG를 오케스트레이션 | 웹 앱을 빠르게 배포하되 EC2 기반 제어도 일부 필요하면 Beanstalk | Beanstalk는 인프라를 숨기지만 완전 서버리스는 아니다. |
| [[Amazon EC2]] vs [[Amazon Lightsail]] | Lightsail은 단순 패키지형 VPS | 소규모 웹사이트/고정 월비용/단순 운영이면 Lightsail | 복잡한 VPC/오토스케일/엔터프라이즈 아키텍처에는 EC2가 적합하다. |

## 5. 가용성 / 확장성 / 복원력

- 단일 EC2 인스턴스는 AZ 장애와 인스턴스 장애에 취약하므로, 일반적인 프로덕션 웹 계층은 여러 AZ의 Auto Scaling group + ALB로 구성한다.
- 상태 저장 데이터는 EBS snapshot, AMI, AWS Backup, 애플리케이션 복제 전략을 별도로 설계한다.
- 장애 자동 복구에는 Auto Scaling health check, ELB health check, CloudWatch alarm, Systems Manager Automation 등을 조합한다.
- Capacity Reservation은 특정 AZ의 EC2 용량 보장이 필요할 때 고려한다.

## 6. 보안 / 운영 포인트

- IAM role for EC2를 사용해 장기 액세스 키를 인스턴스에 저장하지 않는다.
- Systems Manager Session Manager를 사용하면 SSH/RDP 포트 노출을 줄일 수 있다.
- IMDSv2 사용, 보안 그룹 최소 권한, EBS 암호화, 패치 관리, CloudWatch Agent/SSM Agent가 운영 포인트다.
- EC2는 shared responsibility에서 사용자 책임이 큰 서비스다. OS/미들웨어 패치 누락이 자주 함정이다.

## 7. SAP-C02 시나리오 패턴

### 패턴 1: 기존 애플리케이션 Lift-and-shift

- **요구사항**: 커스텀 OS 설정과 에이전트가 필요하고 빠르게 AWS로 이전해야 한다.
- **정답 단서**: existing server, minimal code change, custom software, control over OS.
- **선택할 구성**: EC2 + AMI 표준화 + ALB/Auto Scaling + EBS snapshot/Backup.
- **오답 함정**: Lambda/Fargate로 바로 전환하려면 애플리케이션 구조 변경이 필요할 수 있다.

### 패턴 2: 비용 최적화된 중단 허용 배치 작업

- **요구사항**: 대규모 계산, 작업 재시도 가능, 비용 최소화.
- **정답 단서**: fault tolerant, flexible start/end, checkpoint.
- **선택할 구성**: Spot Instances 또는 AWS Batch의 Spot 기반 compute environment.
- **오답 함정**: 상태 저장 단일 서버를 Spot에만 의존하면 중단 시 장애가 된다.

## 8. 헷갈리는 포인트

> [!warning] 주의
> EC2는 “가장 기본 정답”이 아니라 “서버 제어가 정답 조건일 때” 선택한다.

- public subnet에 있어도 public IPv4/EIP와 라우팅/보안 그룹이 맞아야 인터넷 접근이 된다.
- EBS는 AZ 리소스다. 다른 AZ 인스턴스에 붙이려면 스냅샷/복제 방식이 필요하다.
- Instance store는 영구 저장소가 아니다.
- Auto Scaling은 애플리케이션 상태 저장 문제를 자동으로 해결하지 않는다.

## 9. 암기 문장

- OS와 인프라를 직접 제어해야 하면 EC2, 이벤트 기반 짧은 실행은 Lambda, 컨테이너 서버 관리를 없애려면 Fargate를 먼저 비교한다.
- EC2 시험 문제는 인스턴스 타입보다 “구매 옵션 + HA 배치 + 스토리지 지속성 + 운영 책임” 조합을 묻는다.

## 10. 참고 링크

- [What is Amazon EC2?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [Amazon EC2 instance types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html)
- [Amazon EC2 purchasing options](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)
- [Amazon EC2 security](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
