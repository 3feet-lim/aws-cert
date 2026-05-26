---
type: aws-service
service_name: "AWS License Manager"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["License Manager", "BYOL"]
tags: [aws, sap-c02, license, governance]
created: 2026-05-26
updated: 2026-05-26
---

# AWS License Manager

> [!summary] 한 줄 요약
> Microsoft, Oracle, SAP 등 소프트웨어 라이선스 사용을 AWS와 온프레미스 전반에서 추적·제어하는 라이선스 거버넌스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | BYOL, 라이선스 규정 준수, EC2/RDS 사용 제한, Organizations 중앙 관리 |
| 핵심 의사결정 | 기존 라이선스를 AWS로 가져오고 사용량 초과를 방지해야 하면 License Manager |
| 대표 키워드 | BYOL, license configuration, vCPU/core/socket, hard/soft limit, Organizations |
| 자주 비교되는 서비스 | [[AWS Trusted Advisor]], [[AWS Compute Optimizer]], [[Service Quotas]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 라이선스 규칙을 정의하고 EC2/RDS/온프레미스 사용량을 추적·제한하는 서비스.
- **왜 쓰는가?**: BYOL 비용과 컴플라이언스 리스크를 관리한다.
- **핵심 제약**: 일반 비용 최적화 도구가 아니라 소프트웨어 라이선스 준수/제어 도구다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| License configuration | vCPU/socket/core 등 규칙 | 계약 조건 반영 |
| Enforcement | hard/soft limit | 초과 배포 방지/경고 |
| Discovery | EC2/RDS/온프레미스 사용 추적 | 하이브리드 라이선스 관리 |
| Organizations 통합 | 멀티계정 중앙 관리 | 기업 governance |
| Managed entitlements | 구매/배포 권한 관리 | Marketplace/ISV 연계 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-access-license-governance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| BYOL 사용량 추적/제한 | License Manager | Trusted Advisor는 일반 모범 사례 점검 |
| 컴퓨팅 right-sizing | Compute Optimizer | License Manager는 성능 추천 도구가 아님 |
| AWS 서비스 한도 증가 | Service Quotas | 라이선스 계약 한도와 AWS quota는 다름 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> License Manager는 라이선스 준수 도구다. 비용 절감 추천만 요구하면 Compute Optimizer/Cost Explorer도 본다.

- BYOL 계약 조건을 vCPU/core/socket 등으로 모델링한다.
- Organizations 환경에서 중앙 라이선스 관리가 중요하다.
- hard limit은 배포 차단, soft limit은 경고 성격으로 이해한다.

## 6. 암기 문장

- BYOL 라이선스 초과 방지는 License Manager다.
- AWS quota는 Service Quotas, 소프트웨어 계약 한도는 License Manager다.

## 참고 링크

- [What is AWS License Manager?](https://docs.aws.amazon.com/license-manager/latest/userguide/license-manager.html)
- [License configurations in License Manager](https://docs.aws.amazon.com/license-manager/latest/userguide/license-configurations.html)
