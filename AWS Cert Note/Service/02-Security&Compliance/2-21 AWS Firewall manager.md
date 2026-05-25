---
type: aws-service
service_name: "AWS Firewall Manager"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Firewall Manager", "FMS"]
tags: [aws, sap-c02, security, governance, firewall]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Firewall Manager

> [!summary] 한 줄 요약
> AWS Organizations 계정 전반에 WAF, Shield Advanced, Security Group, Network Firewall 정책을 중앙 적용하는 보안 정책 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | central firewall policy, multi-account, Organizations, WAF policy |
| 핵심 의사결정 | 여러 계정/리소스에 방화벽 정책을 일관되게 강제해야 하면 Firewall Manager를 선택한다. |
| 대표 키워드 | Firewall Manager, policy, Organizations, WAF, Shield Advanced, security group policy, Network Firewall |
| 자주 비교되는 서비스 | [[AWS WAF]], [[AWS Shield]], [[AWS Network Firewall]], [[AWS Organizations]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS Firewall Manager의 시험 역할은 central firewall policy, multi-account, Organizations, WAF policy 요구를 해결하는 것이다.
- **왜 쓰는가?**: AWS Organizations 계정 전반에 WAF, Shield Advanced, Security Group, Network Firewall 정책을 중앙 적용하는 보안 정책 관리 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Policy enforcement | 조직/OU 대상 정책 적용 | 멀티 계정 일관성 |
| WAF policy | Web ACL 자동 연결/관리 | 새 리소스 보호 자동화 |
| Shield Advanced policy | DDoS 보호 표준화 | 고위험 계정 중앙 관리 |
| Security group audit | 과도한 SG 규칙 탐지/수정 | 거버넌스 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Firewall Manager]] | 보안 정책 중앙 배포 | 멀티 계정 방화벽 거버넌스 | 트래픽 검사 엔진 자체가 아님 |
| [[AWS WAF]] | 웹 요청 필터링 | 개별 Web ACL 동작 | 조직 일괄 적용은 Firewall Manager |
| [[AWS Network Firewall]] | VPC 트래픽 검사 | 방화벽 엔드포인트/룰 엔진 | 다계정 정책 관리와 구분 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-org-governance-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 새 ALB 자동 WAF 적용

- **요구사항**: 여러 계정에서 ALB 생성 시 표준 Web ACL 강제
- **정답 단서**: Organizations, central policy
- **선택할 구성**: Firewall Manager WAF policy
- **오답 함정**: 각 계정 수동 설정

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Firewall Manager는 Organizations 기반이므로 멀티 계정 맥락에서 자주 정답이다.
- WAF/Shield/Network Firewall 기능 자체와 정책 배포 기능을 구분한다.

## 7. 암기 문장

- 다계정 방화벽 정책 강제는 Firewall Manager다.
- 개별 방어 서비스는 WAF/Shield/Network Firewall이다.

## 참고 링크

- [What is AWS Firewall Manager?](https://docs.aws.amazon.com/waf/latest/developerguide/fms-chapter.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
