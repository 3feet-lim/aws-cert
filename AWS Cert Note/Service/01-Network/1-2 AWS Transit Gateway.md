---
type: aws-service
service_name: "AWS Transit Gateway"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Transit Gateway", "TGW"]
tags: [aws, sap-c02, networking, hybrid, multi-account]
created: 2026-05-23
updated: 2026-05-23
---

# AWS Transit Gateway

> [!summary] 한 줄 요약
> 여러 VPC와 온프레미스 네트워크를 허브-앤-스포크로 연결하고 라우팅 도메인을 중앙에서 제어하는 네트워크 허브 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 멀티 VPC/멀티 계정 연결, 하이브리드 네트워크, 중앙 라우팅, 네트워크 분리 |
| 핵심 의사결정 | VPC 수가 많거나 온프레미스까지 중앙 허브로 연결해야 하면 Transit Gateway |
| 대표 키워드 | hub-and-spoke, many VPCs, attachments, TGW route table, propagation, segmentation, hybrid |
| 자주 비교되는 서비스 | [[VPC Peering]], [[AWS PrivateLink]], [[AWS VPN]], [[AWS Direct Connect]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: VPC, VPN, Direct Connect gateway 등을 attachment로 붙이는 리전 단위 네트워크 전송 허브.
- **왜 쓰는가?**: 대규모 mesh peering을 단순화하고 중앙 라우팅/분리/공유 서비스를 구현하기 위해 사용한다.
- **관리형 여부**: TGW 자체는 관리형이지만 route table, propagation, association, CIDR 계획은 사용자가 설계한다.
- **리전/글로벌**: 리전 서비스이며 inter-Region peering으로 TGW 간 연결할 수 있다.
- **핵심 제약/한계**: CIDR 중복을 해결하지 못하며, 특정 서비스만 노출하는 PrivateLink와 역할이 다르다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Attachment | VPC/VPN/DXGW 등을 TGW에 연결 | 연결 대상과 과금/라우팅 단위. |
| TGW route table | attachment별 라우팅 도메인 | shared services/prod/dev 분리 단서. |
| Propagation/Association | 경로 전파와 라우팅 테이블 연결 | 라우팅 누락/과다 연결 문제의 핵심. |
| Appliance mode | stateful inspection 장비 대칭 라우팅 | 중앙 inspection VPC 설계. |
| Inter-Region peering | 리전 간 TGW 연결 | 글로벌 네트워크 확장. |
| Direct Connect gateway 연동 | 온프레미스 전용선과 다중 VPC 연결 | 하이브리드 대규모 연결 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Transit Gateway]] | 중앙 허브 라우팅 | 다수 VPC/계정/온프레미스 연결 | CIDR 중복 해결 서비스가 아님 |
| [[VPC Peering]] | 1:1 비전이 연결 | 소수 VPC 간 단순 연결 | transitive routing 불가 |
| [[AWS PrivateLink]] | 특정 서비스 private 노출 | CIDR 중복 가능, 소비자-제공자 서비스 접근 | 네트워크 전체 라우팅 아님 |
| [[AWS Direct Connect]] | 온프레미스-AWS 전용 연결 | 일관된 대역폭/지연시간 | VPC 간 중앙 라우터 역할은 TGW |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 수십 개 VPC 중앙 연결

- **요구사항**: 여러 계정 VPC와 온프레미스를 중앙에서 라우팅하고 분리해야 함
- **정답 단서**: many VPCs, hub-and-spoke, centralized routing
- **선택할 구성**: Transit Gateway + TGW route tables
- **오답 함정**: VPC Peering mesh는 운영 복잡도와 transitive routing 부재가 문제.

### 패턴 2: 중앙 보안 검사 VPC

- **요구사항**: 모든 egress/동서 트래픽을 방화벽 VPC로 통과
- **정답 단서**: centralized inspection, appliance, route domains
- **선택할 구성**: TGW + inspection VPC + appliance mode
- **오답 함정**: 라우팅 대칭성을 고려하지 않으면 stateful firewall이 깨진다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- TGW도 route table 설계가 핵심이다. 붙이기만 하면 모든 네트워크가 원하는 대로 통신하지 않는다.
- VPC Peering과 달리 중앙 허브 라우팅을 제공하지만 CIDR 중복은 여전히 제약이다.
- PrivateLink는 서비스 접근, TGW는 네트워크 라우팅이다.

## 6. 암기 문장

- 많은 VPC와 온프레미스를 허브로 묶으면 Transit Gateway다.
- 소수 1:1은 Peering, 특정 서비스 private 제공은 PrivateLink와 구분한다.

## 참고 링크

- [What is AWS Transit Gateway?](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)
- [Transit gateway route tables](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-route-tables.html)
- [Transit gateway scenarios](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-scenarios.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
