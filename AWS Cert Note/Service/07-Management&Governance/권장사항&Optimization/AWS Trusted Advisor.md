---
type: aws-service
service_name: "AWS Trusted Advisor"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Trusted Advisor", "TA"]
tags: [aws, sap-c02, optimization, best-practice]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Trusted Advisor

> [!summary] 한 줄 요약
> AWS 계정 전반을 비용, 성능, 보안, 내결함성, 서비스 한도 관점에서 점검하고 권장 사항을 제공하는 best practice advisor다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 계정 전반 모범 사례 점검, 비용 절감, 보안 노출, fault tolerance, service limits |
| 핵심 의사결정 | AWS 환경 전체의 best practice 권고를 빠르게 확인해야 하면 Trusted Advisor |
| 대표 키워드 | checks, cost optimization, security, fault tolerance, performance, service limits, support plan |
| 자주 비교되는 서비스 | [[AWS Compute Optimizer]], [[Service Quotas]], [[AWS Well Architected Tool]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 계정 설정과 리소스를 검사해 모범 사례 기반 추천을 제공한다.
- **왜 쓰는가?**: 비용 낭비, 보안 위험, fault tolerance 취약점, service limit 접근을 빠르게 찾는다.
- **핵심 제약**: 지원 플랜에 따라 사용할 수 있는 체크 범위가 다르며, 추천은 자동 변경이 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Cost optimization | 유휴/과소사용 리소스 등 | 비용 개선 단서 |
| Security | 공개 포트, IAM 등 | 보안 점검 |
| Fault tolerance | 백업/멀티 AZ 등 | 복원력 개선 |
| Performance | 성능 관련 체크 | 병목 후보 |
| Service Limits | 한도 접근성 체크 | Service Quotas와 연결 |

## 3. 선택 맵

![[attachments/aws/aws-optimization-advisory-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 계정 전반 best practice 점검 | Trusted Advisor | 리소스별 right-sizing은 Compute Optimizer |
| EC2/Lambda/RDS 권장 크기 | Compute Optimizer | Trusted Advisor는 세부 성능 모델링 도구가 아님 |
| quota 증가 요청 | Service Quotas | Trusted Advisor는 한도 접근 경고 중심 |
| 아키텍처 워크로드 리뷰 | Well-Architected Tool | Trusted Advisor는 계정 체크 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Trusted Advisor는 권고를 제공하지만 자동으로 변경하지 않는다. 운영 검증 후 적용해야 한다.

- 지원 플랜별 체크 가용성을 문제 조건에서 확인한다.
- service limits 체크는 Service Quotas의 증가 요청과 함께 생각한다.
- 조직 전체 운영은 Organizations/Support API 연계를 고려한다.

## 6. 암기 문장

- 계정 전반 모범 사례 빠른 점검은 Trusted Advisor다.
- 세부 right-sizing은 Compute Optimizer, quota 증가는 Service Quotas다.

## 참고 링크

- [AWS Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html)
- [Trusted Advisor check categories](https://docs.aws.amazon.com/awssupport/latest/user/check-categories.html)
