---
type: aws-service
service_name: "AWS Compute Optimizer"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Compute Optimizer"]
tags: [aws, sap-c02, optimization, rightsizing]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Compute Optimizer

> [!summary] 한 줄 요약
> CloudWatch 지표를 분석해 EC2, Auto Scaling groups, EBS, Lambda, ECS Fargate, RDS 등의 리소스 크기와 설정 최적화를 추천하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | right-sizing, 과대/과소 프로비저닝, 비용/성능 최적화, 리소스별 추천 |
| 핵심 의사결정 | 컴퓨팅 리소스의 적정 크기와 성능/비용 개선 추천이 필요하면 Compute Optimizer |
| 대표 키워드 | right-sizing, over-provisioned, under-provisioned, CloudWatch metrics, recommendations |
| 자주 비교되는 서비스 | [[AWS Trusted Advisor]], [[AWS Cost Explorer]], [[Amazon CloudWatch]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 과거 사용 지표를 분석해 리소스 타입/크기/구성을 추천하는 최적화 서비스.
- **왜 쓰는가?**: 비용을 줄이면서 성능 위험을 낮추고 적정 용량을 찾는다.
- **핵심 제약**: 추천은 자동 변경이 아니며 업무 특성과 성능 테스트 후 적용한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| EC2 recommendations | 인스턴스 타입/크기 추천 | right-sizing |
| ASG recommendations | Auto Scaling group 최적화 | fleet 비용/성능 |
| EBS recommendations | 볼륨 타입/크기/IOPS 추천 | 스토리지 비용/성능 |
| Lambda recommendations | 메모리 크기 추천 | 서버리스 성능/비용 |
| RDS/ECS Fargate | DB/컨테이너 리소스 최적화 | 최신 출제 가능 영역 |

## 3. 선택 맵

![[attachments/aws/aws-optimization-advisory-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 리소스 right-sizing 추천 | Compute Optimizer | Trusted Advisor는 계정 전반 체크 |
| 비용 보고/예산 | Cost Explorer/Budgets | Compute Optimizer는 권장 설정 중심 |
| 실시간 지표 알람 | CloudWatch | Compute Optimizer는 분석/추천 서비스 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Compute Optimizer 추천은 자동 변경이 아니다. 피크/계절성/업무 SLA를 검증해야 한다.

- 과소 프로비저닝 추천은 비용 절감이 아니라 성능 위험 해결일 수 있다.
- CloudWatch Agent로 메모리 지표를 추가하면 추천 품질이 좋아질 수 있다.
- 절감액만 보지 말고 performance risk를 함께 본다.

## 6. 암기 문장

- EC2/Lambda/EBS/RDS 같은 리소스 right-sizing은 Compute Optimizer다.
- 계정 전반 best practice는 Trusted Advisor와 구분한다.

## 참고 링크

- [What is AWS Compute Optimizer?](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is.html)
- [Compute Optimizer recommendations](https://docs.aws.amazon.com/compute-optimizer/latest/ug/viewing-recommendations.html)
