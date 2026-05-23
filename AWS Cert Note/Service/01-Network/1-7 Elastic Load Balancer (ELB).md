---
type: aws-service
service_name: "Elastic Load Balancer (ELB)"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["ELB", "ALB", "NLB", "GWLB", "Elastic Load Balancing"]
tags: [aws, sap-c02, networking, load-balancing, ha]
created: 2026-05-23
updated: 2026-05-23
---

# Elastic Load Balancer (ELB)

> [!summary] 한 줄 요약
> 애플리케이션 트래픽을 여러 AZ의 대상에 분산하고 상태 확인과 고가용성 진입점을 제공하는 관리형 로드 밸런싱 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 고가용성 웹/앱 계층, L7/L4 분산, TLS 종료, 마이크로서비스, 네트워크 appliance |
| 핵심 의사결정 | 프로토콜/성능/대상/라우팅 요구에 맞춰 ALB, NLB, GWLB를 선택해야 함 |
| 대표 키워드 | ALB, NLB, GWLB, target group, health check, listener, cross-zone, TLS termination |
| 자주 비교되는 서비스 | [[Amazon Route 53]], [[Amazon CloudFront]], [[AWS Global Accelerator]], [[EC2 Auto Scaling]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 관리형 로드 밸런서 패밀리로 ALB, NLB, GWLB가 있다.
- **왜 쓰는가?**: 단일 인스턴스/컨테이너 장애를 숨기고 여러 AZ 대상에 트래픽을 분산하기 위해 사용한다.
- **관리형 여부**: 로드 밸런서 인프라는 관리형이지만 listener, target group, health check, 보안, TLS 정책은 설계해야 한다.
- **리전/글로벌**: 리전 서비스이며 여러 AZ subnet에 배치해 고가용성을 구성한다.
- **핵심 제약/한계**: 글로벌 CDN/Anycast 가속이 아니라 리전 내 또는 VPC 경계의 로드 밸런싱이 핵심이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Application Load Balancer | HTTP/HTTPS L7 로드 밸런서 | path/host/header routing, Lambda/ECS/EKS 웹 서비스. |
| Network Load Balancer | TCP/UDP/TLS L4 고성능 | 고정 IP, 초고성능, low latency, preserve source IP. |
| Gateway Load Balancer | 보안 appliance 투명 삽입 | 방화벽/IDS/IPS 중앙 검사. |
| Target group | 대상과 health check 단위 | EC2/IP/Lambda/ALB 등 대상 유형. |
| Listener/rules | 포트/프로토콜과 라우팅 규칙 | HTTPS 종료와 host/path 라우팅. |
| Cross-zone load balancing | AZ 간 균등 분산 | 비용/가용성/대상 분포 고려. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| ALB | L7 HTTP/HTTPS | 웹앱, path/host routing, WAF 연동 | TCP/UDP 초고성능에는 NLB |
| NLB | L4 TCP/UDP/TLS | 고정 IP, 초고성능, source IP 보존 | HTTP 경로 기반 라우팅 불가 |
| GWLB | GENEVE 기반 appliance 삽입 | 중앙 보안 검사/third-party firewall | 일반 웹 로드밸런서가 아님 |
| [[Amazon Route 53]] | DNS 라우팅 | 글로벌/DR DNS 선택 | 타깃 상태 기반 실제 요청 분산은 ELB |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 웹 서비스 Multi-AZ

- **요구사항**: EC2/ECS 웹 서버를 여러 AZ에 두고 HTTP 라우팅
- **정답 단서**: HTTP, path-based routing, health check
- **선택할 구성**: ALB + target groups + Auto Scaling
- **오답 함정**: Route 53만으로 인스턴스 상태 기반 세밀 분산을 대체하지 않는다.

### 패턴 2: 초고성능 TCP 서비스

- **요구사항**: TCP/UDP 트래픽, 고정 IP, source IP 보존 필요
- **정답 단서**: TCP, static IP, low latency
- **선택할 구성**: NLB
- **오답 함정**: ALB는 L7 HTTP 기능 중심이다.

### 패턴 3: 중앙 방화벽 삽입

- **요구사항**: 트래픽을 보안 appliance fleet로 투명하게 전달
- **정답 단서**: firewall appliance, transparent inspection
- **선택할 구성**: GWLB
- **오답 함정**: ALB/NLB로 appliance 투명 삽입을 구현하려 하면 복잡하다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- ALB는 L7, NLB는 L4, GWLB는 appliance insertion이다.
- ELB는 리전 서비스이므로 글로벌 성능/Anycast는 CloudFront/Global Accelerator와 비교한다.
- Health check가 맞지 않으면 정상 대상도 제외될 수 있다.

## 6. 암기 문장

- 웹 HTTP 라우팅은 ALB, TCP/UDP 고성능은 NLB, 보안 장비 삽입은 GWLB다.
- ELB는 보통 Auto Scaling과 함께 HA 웹 계층의 기본 구성이다.

## 참고 링크

- [What is Elastic Load Balancing?](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
- [Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
- [Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)
- [Gateway Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
