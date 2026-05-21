---
type: aws-service
service_name: "AWS Auto Scaling"
category: "03-Computing/Virtual Machine"
exam: SAP-C02
exam_domains:
  - "3. 기존 솔루션 개선"
status: draft
priority: medium
aliases:
  - AWS Auto Scaling
tags:
  - aws
  - sap-c02
  - compute
  - scaling
created: 2026-05-20
updated: 2026-05-20
---

# AWS Auto Scaling

> [!summary] 한 줄 요약
> AWS Auto Scaling은 여러 AWS 리소스의 확장 정책을 한곳에서 계획·관리하는 상위 서비스로, EC2 Auto Scaling 자체와 구분해야 한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 다중 리소스 확장 관리, 비용/성능 균형, scaling plan |
| 핵심 의사결정 | EC2만 직접 조정할지, 여러 scalable resource를 통합 정책으로 관리할지 |
| 대표 키워드 | scaling plan, target tracking, multiple resources, predictive scaling |
| 자주 비교되는 서비스 | [[EC2 Auto Scaling]], [[Amazon ECS]], [[DynamoDB]], [[Aurora]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 애플리케이션의 여러 확장 가능 리소스에 대해 scaling plan을 만들고 target tracking/predictive scaling 등을 적용하는 서비스.
- **왜 쓰는가?**: 단일 ASG가 아니라 여러 리소스의 확장을 일관되게 관리해 성능과 비용을 균형 있게 맞추기 위해 사용한다.
- **관리형/비관리형 여부**: scaling plan 관리는 AWS가 제공하지만, 어떤 리소스/지표/목표를 사용할지는 사용자가 설계한다.
- **리전/글로벌 서비스 여부**: 리전별 리소스 확장을 관리한다.
- **핵심 제약/한계**: EC2 인스턴스 교체·health check·launch template 같은 ASG 세부 기능은 [[EC2 Auto Scaling]] 영역이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Scaling plan | 확장 리소스와 정책을 묶어 관리 | 다중 리소스 확장 정책을 중앙화할 때 등장한다. |
| Target tracking | 목표 사용률을 유지 | EC2 ASG, ECS, DynamoDB 등 리소스별 지표 목표를 잡는다. |
| Predictive scaling | 과거 패턴 기반 예측 확장 | 반복적인 트래픽 패턴이 있는 경우 사전 용량 확보에 유리하다. |
| Resource discovery | CloudFormation stack/tag 기반 탐색 | 애플리케이션 단위 리소스 관리를 떠올린다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Auto Scaling]] vs [[EC2 Auto Scaling]] | AWS Auto Scaling은 scaling plan, EC2 Auto Scaling은 ASG의 직접 용량/교체 제어 | 여러 리소스를 묶어 정책화하면 AWS Auto Scaling | EC2 장애 인스턴스 교체 자체는 EC2 Auto Scaling의 핵심 기능이다. |
| [[AWS Auto Scaling]] vs Application Auto Scaling | Application Auto Scaling은 ECS/DynamoDB 등 개별 서비스의 scalable target API | 특정 서비스별 세부 scaling은 Application Auto Scaling 기반 | 시험에서는 이름이 비슷해도 대상 리소스를 먼저 봐야 한다. |

## 4. 언제 사용하는가

- 여러 계층의 리소스를 하나의 애플리케이션 관점에서 확장 계획으로 관리해야 할 때.
- 반복 트래픽 패턴이 있고 예측 확장을 사용해 성능 저하를 줄여야 할 때.
- 태그나 CloudFormation stack 기준으로 확장 가능한 리소스를 묶어 관리하고 싶을 때.

## 5. 언제 사용하지 않는가

- 단일 웹 계층 EC2 인스턴스 수를 제어하고 health replacement가 핵심이면 [[EC2 Auto Scaling]]을 직접 설계한다.
- Lambda처럼 서비스 자체가 요청 기반으로 자동 확장되는 경우에는 별도 scaling plan이 핵심 정답이 아닐 수 있다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> AWS Auto Scaling과 EC2 Auto Scaling은 이름이 비슷하지만 시험에서는 “무엇을 확장하는가”를 먼저 구분한다.

- AWS Auto Scaling은 EC2만을 위한 서비스가 아니다.
- EC2 Auto Scaling group의 launch template, lifecycle hook, instance refresh는 AWS Auto Scaling이 아니라 ASG 세부 기능이다.
- 데이터베이스나 큐 병목까지 자동 해결해 주지는 않는다. 각 계층별 scaling 가능성과 제한을 확인해야 한다.

## 7. 암기 문장

- EC2 인스턴스 그룹 자체는 EC2 Auto Scaling, 여러 리소스의 확장 계획은 AWS Auto Scaling이다.
- “scaling plan”이라는 단어가 보이면 AWS Auto Scaling을 떠올린다.

## 8. 참고 링크

- [AWS Auto Scaling documentation](https://docs.aws.amazon.com/autoscaling/)
- [Amazon EC2 Auto Scaling documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
