---
type: aws-service
service_name: "AWS Global Accelerator"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Global Accelerator", "AGA"]
tags: [aws, sap-c02, networking, global, anycast]
created: 2026-05-23
updated: 2026-05-23
---

# AWS Global Accelerator

> [!summary] 한 줄 요약
> 고정 Anycast IP와 AWS 글로벌 네트워크를 사용해 사용자 트래픽을 가장 건강하고 가까운 리전 엔드포인트로 빠르게 라우팅하는 L4 글로벌 가속 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 글로벌 애플리케이션 가속, 고정 IP, 빠른 장애 조치, TCP/UDP 성능 개선 |
| 핵심 의사결정 | 캐싱이 아니라 TCP/UDP 트래픽을 고정 Anycast IP로 빠르게/안정적으로 라우팅해야 하면 Global Accelerator |
| 대표 키워드 | Anycast static IP, accelerator, listener, endpoint group, health check, traffic dial, TCP/UDP |
| 자주 비교되는 서비스 | [[Amazon CloudFront]], [[Amazon Route 53]], [[Elastic Load Balancer (ELB)]], [[AWS WAF]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS edge location의 Anycast static IP를 통해 리전 엔드포인트로 트래픽을 전달하는 네트워크 서비스.
- **왜 쓰는가?**: 인터넷 경로 변동을 줄이고 고정 IP, 빠른 failover, 글로벌 트래픽 제어가 필요한 앱에 사용한다.
- **관리형 여부**: 가속 네트워크는 관리형이지만 endpoint group, traffic dial, health check, endpoint weight는 설계해야 한다.
- **리전/글로벌**: 글로벌 서비스이며 엔드포인트는 ALB/NLB/EC2/EIP 등이 될 수 있다.
- **핵심 제약/한계**: CDN 캐싱이나 HTTP 객체 최적화 기능은 CloudFront 영역이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Static Anycast IP | 전 세계 공통 고정 진입 IP | 방화벽 allowlist와 DNS 변경 최소화. |
| Accelerator/listener | 포트/프로토콜 진입점 | TCP/UDP 글로벌 라우팅. |
| Endpoint group | 리전별 endpoint 묶음 | 리전 failover와 traffic dial. |
| Health check | 비정상 endpoint 제외 | DNS TTL보다 빠른 장애 조치 단서. |
| Traffic dial/weight | 리전/엔드포인트 비율 조정 | blue/green, 리전 트래픽 제어. |
| Client affinity | 소스 IP 기반 stickiness | stateful 앱 고려. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Global Accelerator]] | Anycast IP L4 가속 | TCP/UDP, 고정 IP, 빠른 failover | 캐싱 없음 |
| [[Amazon CloudFront]] | HTTP(S) CDN 캐싱 | 웹 콘텐츠/edge 보안/캐시 behavior | TCP/UDP 범용 가속 아님 |
| [[Amazon Route 53]] | DNS 기반 라우팅 | 도메인 정책과 health check | TTL 캐시로 failover 지연 가능 |
| [[Elastic Load Balancer (ELB)]] | 리전 내 로드밸런서 | 앱 타깃 분산 | 글로벌 Anycast 진입점은 GA |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 글로벌 게임/TCP 앱 가속

- **요구사항**: 전 세계 사용자가 TCP/UDP 앱에 낮은 지연시간으로 접속
- **정답 단서**: TCP/UDP, static IP, Anycast, low latency
- **선택할 구성**: Global Accelerator + NLB/ALB endpoints
- **오답 함정**: CloudFront는 HTTP 콘텐츠 캐싱 중심이다.

### 패턴 2: 고정 IP 기반 글로벌 failover

- **요구사항**: 고객 방화벽에 등록할 IP를 바꾸지 않고 리전 장애 조치
- **정답 단서**: static IP, fast failover, multi-Region
- **선택할 구성**: Global Accelerator endpoint groups
- **오답 함정**: Route 53 DNS failover는 TTL 영향이 있다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- Global Accelerator는 콘텐츠를 캐싱하지 않는다.
- Route 53처럼 DNS 답을 바꾸는 방식이 아니라 Anycast IP로 진입한다.
- 엔드포인트 자체의 애플리케이션 HA는 ALB/NLB/Auto Scaling 등으로 별도 설계해야 한다.

## 6. 암기 문장

- 고정 Anycast IP + 빠른 글로벌 TCP/UDP failover는 Global Accelerator다.
- HTTP 캐싱은 CloudFront, DNS 정책은 Route 53이다.

## 참고 링크

- [What is AWS Global Accelerator?](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)
- [How AWS Global Accelerator works](https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-how-it-works.html)
- [AWS Global Accelerator components](https://docs.aws.amazon.com/global-accelerator/latest/dg/about-accelerators.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
