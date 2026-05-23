---
type: aws-service
service_name: "Amazon Route 53"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Route 53", "R53"]
tags: [aws, sap-c02, networking, dns, global]
created: 2026-05-23
updated: 2026-05-23
---

# Amazon Route 53

> [!summary] 한 줄 요약
> 도메인 등록, 권한 DNS, 상태 확인, 라우팅 정책을 제공해 사용자를 적절한 엔드포인트로 연결하는 AWS 글로벌 DNS 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | DNS 라우팅, 글로벌/DR 트래픽 제어, health check 기반 failover, private DNS |
| 핵심 의사결정 | 도메인 이름을 기반으로 위치/지연시간/가중치/상태에 따라 엔드포인트를 선택해야 하면 Route 53 |
| 대표 키워드 | hosted zone, record, alias, health check, failover, latency, weighted, geolocation, private hosted zone |
| 자주 비교되는 서비스 | [[Amazon CloudFront]], [[AWS Global Accelerator]], [[Elastic Load Balancer (ELB)]], [[Amazon VPC]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS의 확장 가능한 DNS 및 도메인 등록 서비스.
- **왜 쓰는가?**: 사용자 DNS 질의를 ALB/CloudFront/S3/API/온프레미스 등 적절한 대상으로 라우팅하기 위해 사용한다.
- **관리형 여부**: DNS 서비스는 관리형이지만 레코드, TTL, health check, 라우팅 정책 설계는 사용자 책임이다.
- **리전/글로벌**: 공개 DNS는 글로벌 서비스이고 private hosted zone은 VPC와 연결해 사용한다.
- **핵심 제약/한계**: DNS는 캐시/TTL 때문에 즉시 트래픽 전환을 보장하는 L4 프록시가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Hosted zone | 도메인 DNS 레코드 컨테이너 | public/private hosted zone 구분. |
| Alias record | AWS 리소스에 apex 포함 alias | ALB/CloudFront/S3 등에 CNAME 대신 사용. |
| Health check | 엔드포인트 상태 확인 | DNS failover 단서. |
| Weighted routing | 비율 기반 분산 | blue/green, canary, A/B. |
| Latency routing | 낮은 지연시간 리전 선택 | 글로벌 사용자 성능. |
| Geolocation/Geoproximity | 위치 기반 라우팅 | 규정/지역별 서비스 분기. |
| Resolver endpoints | 온프레미스와 VPC DNS 통합 | 하이브리드 DNS 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Route 53]] | DNS 기반 라우팅 | 도메인/레코드/health check/라우팅 정책 | TTL 캐시로 즉시 전환 보장 아님 |
| [[AWS Global Accelerator]] | Anycast IP 기반 L4 글로벌 가속 | 고정 IP, 빠른 failover, TCP/UDP | HTTP 캐싱/DNS 관리 서비스가 아님 |
| [[Amazon CloudFront]] | CDN/edge cache | 정적/동적 콘텐츠 edge 최적화 | 권한 DNS 라우팅 정책 자체는 Route 53 |
| [[Elastic Load Balancer (ELB)]] | 리전 내 트래픽 분산 | 타깃 그룹/헬스체크 기반 분산 | 글로벌 DNS 라우팅은 Route 53 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 리전 장애 DNS failover

- **요구사항**: Primary 리전 장애 시 Secondary로 DNS 전환
- **정답 단서**: DNS failover, health check, DR
- **선택할 구성**: Route 53 failover routing + health checks
- **오답 함정**: TTL 때문에 클라이언트 전환 지연이 있을 수 있다.

### 패턴 2: 점진적 배포

- **요구사항**: 새 ALB로 일부 트래픽만 전송
- **정답 단서**: weighted routing, canary, blue/green
- **선택할 구성**: Route 53 weighted records
- **오답 함정**: ALB target weight와 DNS weight의 계층을 혼동하지 않는다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- Alias는 AWS 리소스에 대한 Route 53 확장 레코드이고, zone apex에도 사용할 수 있다.
- Route 53 health check는 DNS 응답 선택에 영향을 주지만 이미 캐시된 클라이언트 레코드는 TTL 영향을 받는다.
- Private hosted zone은 연결된 VPC 내부 이름 해석용이다.

## 6. 암기 문장

- DNS 이름으로 글로벌/DR 라우팅을 제어하면 Route 53이다.
- 고정 Anycast IP와 빠른 L4 failover는 Global Accelerator와 비교한다.

## 참고 링크

- [What is Amazon Route 53?](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)
- [Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
- [Route 53 alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
