---
type: aws-service
service_name: "AWS Network Firewall"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Network Firewall"]
tags: [aws, sap-c02, security, network-firewall, vpc]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Network Firewall

> [!summary] 한 줄 요약
> VPC 트래픽에 stateful/stateless 규칙과 Suricata 호환 룰을 적용하는 관리형 네트워크 방화벽이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | VPC firewall, egress filtering, stateful inspection, Suricata, centralized inspection |
| 핵심 의사결정 | VPC 내부/아웃바운드/인바운드 네트워크 트래픽을 중앙 검사해야 하면 Network Firewall을 선택한다. |
| 대표 키워드 | stateful firewall, stateless, Suricata, inspection VPC, egress filtering, firewall endpoint |
| 자주 비교되는 서비스 | [[AWS WAF]], [[AWS Shield]], [[Security Group]], [[Network ACL]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Network Firewall의 시험 역할은 VPC firewall, egress filtering, stateful inspection, Suricata, centralized inspection 요구를 해결하는 것이다.
- **왜 쓰는가?**: VPC 트래픽에 stateful/stateless 규칙과 Suricata 호환 룰을 적용하는 관리형 네트워크 방화벽이다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Firewall endpoint | 서브넷별 방화벽 엔드포인트 | 라우팅으로 트래픽 삽입 |
| Stateful rules | 세션 기반 검사/Suricata | 도메인/프로토콜/침입 패턴 |
| Stateless rules | 고성능 패킷 필터 | 단순 네트워크 조건 |
| Centralized inspection | TGW/Inspection VPC 패턴 | 멀티 VPC egress/ingress 검사 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Network Firewall]] | VPC 네트워크 트래픽 검사 | 중앙 egress/ingress/동서 트래픽 검사 | HTTP 웹 ACL은 WAF |
| [[AWS WAF]] | 웹 L7 요청 필터 | CloudFront/ALB/API Gateway 보호 | VPC 라우팅 방화벽 아님 |
| Security Group | 인스턴스/ENI 상태 저장 ACL | 워크로드 단위 허용 | 관리형 IDS/Suricata 룰 기능 없음 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-edge-network-protection.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 중앙 egress 검사

- **요구사항**: 모든 VPC 인터넷 outbound를 검사 VPC로 통과
- **정답 단서**: inspection VPC, stateful firewall
- **선택할 구성**: Network Firewall + TGW routing
- **오답 함정**: NACL만으로 도메인 기반 차단

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Network Firewall은 라우팅 설계가 핵심이다. 배치만 해서는 트래픽이 통과하지 않는다.
- WAF/Shield와 계층이 다르다.

## 7. 암기 문장

- VPC 네트워크 방화벽은 Network Firewall이다.
- HTTP 요청 필터는 WAF와 구분한다.

## 참고 링크

- [What is AWS Network Firewall?](https://docs.aws.amazon.com/network-firewall/latest/developerguide/what-is-aws-network-firewall.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
