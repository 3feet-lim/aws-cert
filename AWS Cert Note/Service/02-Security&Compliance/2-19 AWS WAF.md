---
type: aws-service
service_name: "AWS WAF"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["WAF", "Web Application Firewall"]
tags: [aws, sap-c02, security, waf, edge]
created: 2026-05-26
updated: 2026-05-26
---

# AWS WAF

> [!summary] 한 줄 요약
> CloudFront, ALB, API Gateway 등에 대한 HTTP(S) 요청을 Web ACL 규칙으로 필터링하는 웹 애플리케이션 방화벽이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | web application firewall, SQL injection, XSS, rate-based rule, managed rules |
| 핵심 의사결정 | L7 HTTP 요청의 공격 패턴/봇/국가/IP/rate 제한이 필요하면 AWS WAF를 선택한다. |
| 대표 키워드 | Web ACL, managed rule, SQLi, XSS, rate-based, CloudFront, ALB, API Gateway |
| 자주 비교되는 서비스 | [[AWS Shield]], [[AWS Network Firewall]], [[Amazon CloudFront]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS WAF의 시험 역할은 web application firewall, SQL injection, XSS, rate-based rule, managed rules 요구를 해결하는 것이다.
- **왜 쓰는가?**: CloudFront, ALB, API Gateway 등에 대한 HTTP(S) 요청을 Web ACL 규칙으로 필터링하는 웹 애플리케이션 방화벽이다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Web ACL | 규칙 그룹을 리소스에 연결 | CloudFront/ALB/API 보호 |
| Managed rules | AWS/벤더 관리형 룰 | OWASP 공격 빠른 방어 |
| Rate-based rules | 요청 속도 제한 | 봇/스크래핑 완화 |
| IP/Geo/Header match | 조건 기반 차단/허용 | L7 요청 필터링 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS WAF]] | HTTP(S) L7 필터 | SQLi/XSS/rate limit/bot 제어 | VPC 전체 네트워크 방화벽 아님 |
| [[AWS Shield]] | DDoS 보호 | 대규모 공격/DRT/비용 보호 | 세부 HTTP 룰은 WAF |
| [[AWS Network Firewall]] | VPC L3-L7 네트워크 검사 | egress/서브넷 경계 | CloudFront 웹 ACL과 다름 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-edge-network-protection.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: API SQL Injection 방어

- **요구사항**: API Gateway 앞에서 SQLi/XSS 차단
- **정답 단서**: Web ACL, managed rules
- **선택할 구성**: AWS WAF
- **오답 함정**: Security Group으로 HTTP payload 검사

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- WAF는 보안 그룹처럼 포트만 보는 서비스가 아니라 HTTP 요청 속성을 본다.
- DDoS 문제는 Shield와 함께 읽어야 한다.

## 7. 암기 문장

- 웹 L7 방화벽은 AWS WAF다.
- DDoS는 Shield, VPC 트래픽 검사는 Network Firewall이다.

## 참고 링크

- [What is AWS WAF?](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
