---
type: aws-service
service_name: "AWS RAM"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션"]
status: complete
priority: medium
aliases: ["RAM", "Resource Access Manager"]
tags: [aws, sap-c02, security, governance, resource-sharing]
created: 2026-05-26
updated: 2026-05-26
---

# AWS RAM

> [!summary] 한 줄 요약
> 계정 간에 지원되는 AWS 리소스를 복제 없이 안전하게 공유하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | cross-account resource sharing, shared VPC subnet, TGW sharing, Organizations |
| 핵심 의사결정 | 여러 계정이 같은 네트워크/리소스를 공유해야 하지만 소유권은 중앙에 두고 싶으면 RAM을 사용한다. |
| 대표 키워드 | resource share, shared subnet, Transit Gateway, Route 53 Resolver rules, license configurations |
| 자주 비교되는 서비스 | [[AWS Organizations]], [[AWS Transit Gateway]], [[Amazon VPC]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS RAM의 시험 역할은 cross-account resource sharing, shared VPC subnet, TGW sharing, Organizations 요구를 해결하는 것이다.
- **왜 쓰는가?**: 계정 간에 지원되는 AWS 리소스를 복제 없이 안전하게 공유하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Resource share | 공유 단위 생성 | 계정/OU/조직 대상 리소스 공유 |
| Shared VPC subnet | 중앙 네트워크 계정 서브넷 공유 | 워크로드 계정 ENI 배치 패턴 |
| TGW sharing | 중앙 네트워크 허브 공유 | 멀티 계정 네트워크 표준화 |
| Organizations integration | 조직 내 초대 없이 공유 | 대규모 운영 단순화 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS RAM]] | 리소스 공유 | 중앙 소유 리소스를 여러 계정에서 사용 | 데이터 복제/권한 부여 전체 대체 아님 |
| [[AWS Organizations]] | 계정/OU 관리 | 공유 대상 조직 구조 | 리소스 공유 자체는 RAM |
| [[VPC Peering]] | VPC 간 네트워크 연결 | 네트워크 통신 필요 | 서브넷 자체 공유와 다름 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 중앙 네트워크 계정

- **요구사항**: 워크로드 계정이 공통 서브넷 사용
- **정답 단서**: shared subnet, multi-account
- **선택할 구성**: AWS RAM + Shared VPC
- **오답 함정**: 각 계정에 VPC 중복 생성

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- 모든 리소스가 RAM 공유를 지원하는 것은 아니다.
- 공유는 소유권 이전이 아니라 사용 권한 부여다.

## 7. 암기 문장

- 계정 간 리소스 공유는 RAM이다.
- 멀티 계정 네트워크 표준화에서 Shared VPC subnet을 떠올린다.

## 참고 링크

- [What is AWS RAM?](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
