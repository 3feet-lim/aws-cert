---
type: aws-service
service_name: "Amazon EC2 Auto Scaling"
category: "03-Computing/Virtual Machine"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: high
aliases:
  - EC2 Auto Scaling
  - Auto Scaling group
  - ASG
tags:
  - aws
  - sap-c02
  - compute
  - scaling
created: 2026-05-20
updated: 2026-05-20
---

# Amazon EC2 Auto Scaling

> [!summary] 한 줄 요약
> Amazon EC2 Auto Scaling은 Auto Scaling group의 EC2 인스턴스 수를 상태·일정·수요에 맞춰 유지하고 조정해 가용성과 비용을 동시에 관리하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 웹 계층 고가용성, 트래픽 변화 대응, 인스턴스 자동 교체, 배포/교체 전략 |
| 핵심 의사결정 | 어떤 지표/일정/예측으로 scale out/in할지, 여러 AZ에 어떻게 분산할지 |
| 대표 키워드 | Auto Scaling group, launch template, desired/min/max capacity, target tracking, health check, instance refresh |
| 자주 비교되는 서비스 | [[AWS Auto Scaling]], [[Elastic Load Balancer (ELB)]], [[Amazon EC2]], [[AWS Elastic Beanstalk]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: EC2 Auto Scaling group(ASG)에 원하는 용량을 정의하고, 인스턴스 상태나 CloudWatch 지표에 따라 EC2 인스턴스를 추가/제거/교체하는 기능.
- **왜 쓰는가?**: 장애 인스턴스를 자동 대체하고, 부하 증가에는 확장하며, 유휴 시간에는 축소해 비용을 줄이기 위해 사용한다.
- **관리형/비관리형 여부**: 스케일링 제어는 관리형이지만, AMI/launch template/애플리케이션 상태/스케일링 지표 설계는 사용자 책임이다.
- **리전/글로벌 서비스 여부**: ASG는 리전 내 여러 AZ의 subnet에 걸쳐 구성할 수 있다.
- **핵심 제약/한계**: stateless 웹/앱 계층에 가장 자연스럽다. 세션/로컬 상태를 인스턴스에 고정하면 scale-in과 교체가 장애가 될 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Desired/Min/Max capacity | 유지할 현재/최소/최대 인스턴스 수 | 비용과 가용성 경계. 스케일링 정책도 이 범위 안에서 동작한다. |
| Launch template | 새 인스턴스 생성 설정 | launch configuration보다 launch template이 최신 권장 패턴이다. |
| Health check | EC2 또는 ELB 상태 기반 교체 | ALB 뒤 웹 계층은 ELB health check를 함께 쓰는 문제가 자주 나온다. |
| Target tracking | 목표 지표값을 유지하도록 자동 조정 | CPU 50%, ALB RequestCountPerTarget 같은 목표 기반 스케일링에 적합하다. |
| Step/Simple scaling | 알람 단계에 따라 증감 | 급격한 부하 변화나 세밀한 단계 조정이 필요할 때 고려한다. |
| Scheduled scaling | 특정 시간에 용량 변경 | 예측 가능한 업무 시간/이벤트 트래픽에 적합하다. |
| Predictive scaling | 과거 패턴 기반 사전 확장 | 반복 패턴이 있는 워크로드의 사전 용량 확보에 유리하다. |
| Instance refresh | 새 launch template/AMI로 점진 교체 | immutable 업데이트와 롤링 교체 시나리오에 맞다. |

## 3. 스케일링 방식 선택 기준

| 요구사항 | 선택할 방식 | 오답 함정 |
|---|---|---|
| 평균 CPU나 요청 수를 일정하게 유지 | Target tracking | 여러 정책이 동시에 있을 때 더 큰 용량을 요구하는 정책이 우선될 수 있다. |
| 매주 특정 시간에 트래픽 증가 | Scheduled scaling | 예측 가능한 패턴에는 CloudWatch 알람만 기다리는 것보다 일정 확장이 낫다. |
| 알람 임계치 초과 정도에 따라 다르게 확장 | Step scaling | cooldown/warmup을 고려하지 않으면 과도한 scale out/in이 생긴다. |
| 반복 패턴을 미리 예측해 확장 | Predictive scaling | 완전히 불규칙한 이벤트에는 효과가 제한적이다. |
| 새 AMI로 안전하게 교체 | Instance refresh | 단순 scale out은 기존 인스턴스를 교체하지 않는다. |

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[EC2 Auto Scaling]] vs [[AWS Auto Scaling]] | EC2 Auto Scaling은 EC2 ASG 중심, AWS Auto Scaling은 여러 리소스 scaling plan 관리 | EC2 그룹의 직접 제어/정책은 EC2 Auto Scaling | AWS Auto Scaling이 EC2 health replacement 자체를 대체한다고 생각하면 안 된다. |
| [[EC2 Auto Scaling]] vs [[Elastic Load Balancer (ELB)]] | ASG는 용량 조정, ELB는 트래픽 분산 | 웹 계층은 보통 둘을 함께 사용 | ALB만 두면 인스턴스 수가 자동으로 늘지 않는다. |
| [[EC2 Auto Scaling]] vs [[AWS Elastic Beanstalk]] | Beanstalk가 ASG/ELB를 추상화 | 플랫폼 관리형 웹 앱이면 Beanstalk, 세밀 제어는 ASG 직접 구성 | Beanstalk 내부에도 ASG가 생성될 수 있다. |

## 5. 설계 시 고려사항

- 여러 AZ의 subnet을 ASG에 지정해 AZ 장애 시에도 용량을 유지한다.
- ALB/NLB와 연결하고 ELB health check를 켜면 애플리케이션 상태 기준으로 교체할 수 있다.
- scale-in 보호, lifecycle hook, warm pool은 종료 전 작업/느린 부팅/상태 정리에 유용하다.
- 세션은 ElastiCache/DynamoDB/RDS 등 외부 저장소로 분리하거나 sticky session 사용 여부를 명확히 판단한다.

## 6. 비용 / 운영 포인트

- Spot, On-Demand, Reserved/Savings Plans 조합은 launch template의 mixed instances policy와 함께 출제될 수 있다.
- 과도한 scale out을 막기 위해 max capacity와 CloudWatch alarm/예산 경계를 함께 설계한다.
- 너무 공격적인 scale-in은 사용자 세션과 배치 작업을 중단시킬 수 있으므로 cooldown/warmup/lifecycle hook을 고려한다.

## 7. SAP-C02 시나리오 패턴

### 패턴 1: ALB 뒤 웹 서버 고가용성

- **요구사항**: 트래픽 변화에 대응하고 장애 인스턴스를 자동 교체.
- **정답 단서**: multiple AZ, health check, automatic replacement, web tier.
- **선택할 구성**: ALB + Multi-AZ ASG + target tracking scaling.
- **오답 함정**: 수동 EC2 추가나 단일 인스턴스 vertical scaling은 HA 요구에 약하다.

### 패턴 2: 매일 오전 트래픽 급증

- **요구사항**: 특정 시간 전에 용량을 미리 확보.
- **정답 단서**: predictable daily pattern, business hours.
- **선택할 구성**: Scheduled scaling + dynamic scaling 보완.
- **오답 함정**: 동적 스케일링만 쓰면 지표 상승 후 반응하므로 초기 지연이 생길 수 있다.

## 8. 헷갈리는 포인트

> [!warning] 주의
> Auto Scaling은 애플리케이션을 stateless로 만들어 주지 않는다. 인스턴스 교체에 안전하도록 앱을 설계해야 한다.

- desired capacity는 현재 목표 용량이고 min/max는 경계다.
- EC2 health check만으로는 애플리케이션 HTTP 오류를 감지하지 못할 수 있다.
- ASG는 EC2 수를 조정하지만 데이터베이스 병목을 자동 해결하지 않는다.
- scale-in 때 어떤 인스턴스를 종료할지 termination policy가 영향을 준다.

## 9. 암기 문장

- 웹/앱 계층 HA의 기본 조합은 “ALB + Multi-AZ EC2 Auto Scaling group”이다.
- 예측 가능하면 scheduled, 지표 목표 유지면 target tracking, 새 AMI 교체는 instance refresh를 떠올린다.

## 10. 참고 링크

- [What is Amazon EC2 Auto Scaling?](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
- [Choose your scaling method](https://docs.aws.amazon.com/autoscaling/ec2/userguide/scaling-overview.html)
- [Dynamic scaling for Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html)
- [Scheduled scaling for Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-scheduled-scaling.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
