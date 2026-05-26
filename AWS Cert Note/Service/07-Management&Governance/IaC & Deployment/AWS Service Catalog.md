---
type: aws-service
service_name: "AWS Service Catalog"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Service Catalog", "Portfolio", "Product"]
tags: [aws, sap-c02, governance, self-service]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Service Catalog

> [!summary] 한 줄 요약
> 조직이 승인한 인프라/애플리케이션 제품만 포트폴리오로 제공해 사용자가 self-service로 안전하게 배포하게 하는 거버넌스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 표준 제품 배포, 권한 위임, guardrail, 멀티계정 self-service |
| 핵심 의사결정 | 개발자에게 직접 관리자 권한을 주지 않고 승인된 템플릿만 배포하게 하려면 Service Catalog |
| 대표 키워드 | portfolio, product, constraint, launch role, approved templates, self-service |
| 자주 비교되는 서비스 | [[AWS CloudFormation]], [[AWS Proton]], [[AWS Organizations]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: CloudFormation/Terraform 기반 제품을 포트폴리오로 관리하고 사용자에게 승인된 선택지만 제공한다.
- **왜 쓰는가?**: 보안/태그/네트워크 기준을 강제하면서 개발팀의 셀프서비스 속도를 높인다.
- **핵심 제약**: IaC 실행 엔진 자체라기보다 배포 제품의 거버넌스 계층이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Portfolio | 제품 묶음과 접근 권한 | 팀/OU별 카탈로그 |
| Product/Version | 배포 가능한 템플릿과 버전 | 승인된 표준만 배포 |
| Constraints | launch/template/tag 제약 | guardrail 강제 |
| Launch role | 최종 사용자가 직접 권한 없이 배포 | 최소 권한과 권한 위임 |
| Sharing | 계정/조직 공유 | 멀티계정 표준화 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-governed-iac-deployment-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 승인된 제품 self-service | Service Catalog | CloudFormation 단독은 카탈로그/제약 관리 부족 |
| IaC 템플릿 실행 | CloudFormation | 사용자에게 직접 stack 생성 권한을 주면 governance 약화 |
| 플랫폼 템플릿 기반 앱 배포 | Proton | Proton은 서비스/환경 템플릿 중심이며 수명주기 확인 필요 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Service Catalog는 “권한 있는 사용자가 승인된 제품만 배포”하도록 하는 서비스다.

- launch role을 사용하면 최종 사용자의 직접 AWS 권한을 줄일 수 있다.
- constraints로 인스턴스 타입, 리전, 태그, 네트워크 선택을 제한한다.
- Organizations와 공유해 여러 계정에 표준 포트폴리오를 제공할 수 있다.

## 6. 암기 문장

- CloudFormation은 IaC 엔진, Service Catalog는 승인된 IaC 제품의 self-service 카탈로그다.
- 개발자 자유도와 중앙 거버넌스를 동시에 요구하면 Service Catalog를 떠올린다.

## 참고 링크

- [What is AWS Service Catalog?](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/introduction.html)
- [AWS Service Catalog concepts](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/catalogs_portfolios_products.html)
