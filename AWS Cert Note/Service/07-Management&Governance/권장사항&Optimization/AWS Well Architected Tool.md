---
type: aws-service
service_name: "AWS Well-Architected Tool"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Well-Architected Tool", "AWS WA Tool"]
tags: [aws, sap-c02, well-architected, review]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Well-Architected Tool

> [!summary] 한 줄 요약
> Well-Architected Framework의 6개 Pillar 기준으로 워크로드를 리뷰하고 위험과 개선 계획을 관리하는 아키텍처 리뷰 도구다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 아키텍처 리뷰, 위험 식별, 6 Pillars, 개선 계획, milestone |
| 핵심 의사결정 | 특정 워크로드의 아키텍처 품질과 위험을 체계적으로 평가해야 하면 Well-Architected Tool |
| 대표 키워드 | 6 pillars, workload review, high risk issues, milestones, improvement plan |
| 자주 비교되는 서비스 | [[AWS Trusted Advisor]], [[AWS Compute Optimizer]], [[AWS Config]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 운영 우수성, 보안, 신뢰성, 성능 효율성, 비용 최적화, 지속 가능성 관점에서 워크로드를 리뷰하는 도구.
- **왜 쓰는가?**: 아키텍처 위험을 문서화하고 개선 우선순위를 정한다.
- **핵심 제약**: 리소스를 자동 점검/변경하는 서비스가 아니라 질문 기반 리뷰와 개선 추적 도구다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Workload | 리뷰 대상 시스템 | 아키텍처 단위 평가 |
| 6 Pillars | 운영/보안/신뢰성/성능/비용/지속가능성 | SAP-C02 설계 기준 |
| Lens | 산업/기술별 추가 질문 | 특화 리뷰 |
| Milestones | 리뷰 시점 스냅샷 | 개선 전후 추적 |
| Improvement plan | 위험과 개선 항목 | 우선순위 관리 |

## 3. 선택 맵

![[attachments/aws/aws-optimization-advisory-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 워크로드 아키텍처 리뷰 | Well-Architected Tool | Trusted Advisor는 계정 리소스 체크 중심 |
| 리소스 right-sizing | Compute Optimizer | WA Tool은 권장 크기 계산 도구가 아님 |
| 정책 준수 자동 평가 | AWS Config | WA Tool은 설문/리뷰 기반 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Well-Architected Tool은 아키텍처 의사결정과 위험 관리 도구다. 리소스 자동 변경이나 실시간 모니터링이 아니다.

- 6 Pillars는 SAP-C02 설계 문제의 사고 프레임이다.
- High risk issues를 개선 계획으로 관리한다.
- Trusted Advisor와 함께 사용하면 계정 체크 + 아키텍처 리뷰를 보완할 수 있다.

## 6. 암기 문장

- 워크로드를 6 Pillars로 리뷰하면 Well-Architected Tool이다.
- 자동 리소스 추천은 Compute Optimizer, 계정 best practice 체크는 Trusted Advisor다.

## 참고 링크

- [AWS Well-Architected Tool](https://docs.aws.amazon.com/wellarchitected/latest/userguide/intro.html)
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
