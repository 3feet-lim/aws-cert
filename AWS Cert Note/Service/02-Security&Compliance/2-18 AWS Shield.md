---
type: aws-service
service_name: "AWS Shield"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Shield", "Shield Advanced"]
tags: [aws, sap-c02, security, ddos, edge]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Shield

> [!summary] 한 줄 요약
> AWS 엣지와 주요 서비스에 대한 DDoS 보호를 제공하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | DDoS protection, Shield Standard, Shield Advanced, DRT, cost protection |
| 핵심 의사결정 | DDoS 공격 방어, 전문가 지원, 비용 보호가 핵심이면 Shield Advanced를 선택한다. |
| 대표 키워드 | DDoS, Shield Advanced, DRT, Route 53, CloudFront, ALB, Global Accelerator |
| 자주 비교되는 서비스 | [[AWS WAF]], [[Amazon CloudFront]], [[AWS Network Firewall]], [[Amazon Route 53]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Shield의 시험 역할은 DDoS protection, Shield Standard, Shield Advanced, DRT, cost protection 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS 엣지와 주요 서비스에 대한 DDoS 보호를 제공하는 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Shield Standard | 기본 DDoS 보호 | 모든 고객 자동 제공 |
| Shield Advanced | 강화 DDoS 보호/DRT/비용 보호 | 고위험 인터넷 서비스 |
| Protected resources | CloudFront/Route 53/ALB/NLB/EIP 등 | 엣지/프론트도어 보호 |
| WAF integration | L7 규칙과 조합 | DDoS와 웹 공격 함께 대응 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Shield]] | DDoS 보호 | L3/L4 및 일부 L7 DDoS 방어 | 일반 웹 취약점 필터링은 WAF |
| [[AWS WAF]] | HTTP(S) L7 요청 필터 | SQLi/XSS/rate limit | 대규모 DDoS 비용 보호는 Shield Advanced |
| [[AWS Network Firewall]] | VPC 네트워크 방화벽 | 서브넷 간/egress 검사 | 엣지 DDoS 서비스 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-edge-network-protection.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 퍼블릭 서비스 DDoS 우려

- **요구사항**: CloudFront/Route 53/ALB 보호와 DRT 필요
- **정답 단서**: DDoS, cost protection
- **선택할 구성**: Shield Advanced + WAF
- **오답 함정**: Network Firewall만 배치

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Shield Standard는 기본 제공이지만 DRT와 비용 보호는 Shield Advanced 영역이다.
- WAF는 웹 요청 규칙, Shield는 DDoS 맥락이다.

## 7. 암기 문장

- DDoS는 Shield다.
- HTTP 규칙은 WAF와 같이 쓴다.

## 참고 링크

- [What is AWS Shield?](https://docs.aws.amazon.com/waf/latest/developerguide/shield-chapter.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
