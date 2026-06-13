---
type: aws-service
service_name: "Amazon CloudFront"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["CloudFront", "CF"]
tags: [aws, sap-c02, networking, cdn, edge]
created: 2026-05-23
updated: 2026-06-13
---

# Amazon CloudFront

> [!summary] 한 줄 요약
> 전 세계 edge location에서 콘텐츠를 캐싱하고 TLS, WAF, origin 보호, edge compute로 사용자 지연시간과 origin 부하를 줄이는 CDN 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | CDN, 정적/동적 콘텐츠 가속, 전역 edge 보안, origin offload, S3/ALB/API 보호 |
| 핵심 의사결정 | HTTP/HTTPS 콘텐츠를 전 세계 사용자에게 캐싱/가속/보호해야 하면 CloudFront |
| 대표 키워드 | CDN, edge location, distribution, origin, cache behavior, OAC/OAI, signed URL, WAF, Lambda@Edge |
| 자주 비교되는 서비스 | [[Amazon Route 53]], [[AWS Global Accelerator]], [[Elastic Load Balancer (ELB)]], [[Amazon S3]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 글로벌 edge network 기반 CDN.
- **왜 쓰는가?**: 사용자 가까운 edge에서 콘텐츠를 제공하고, 캐싱/압축/TLS/WAF로 성능과 보안을 개선하기 위해 사용한다.
- **관리형 여부**: edge 인프라는 관리형이지만 cache policy, origin, invalidation, 보안 헤더, 접근 제어는 설계해야 한다.
- **리전/글로벌**: 글로벌 서비스 성격이며 distribution은 여러 origin을 가질 수 있다.
- **핵심 제약/한계**: TCP/UDP 임의 프로토콜 가속이나 고정 Anycast IP 서비스가 아니라 HTTP(S) 콘텐츠 배포가 중심이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Distribution | CloudFront 설정 단위 | 도메인, origin, behavior 관리. |
| Origin | S3, ALB, API Gateway, custom origin | origin 보호와 failover 설계. |
| Cache behavior/policy | 경로별 캐시/헤더/쿼리 처리 | cache hit ratio와 보안/개인화 균형. |
| OAC/OAI | S3 origin private 접근 | S3 public 차단 패턴. |
| Signed URL/Cookie | 제한 콘텐츠 접근 제어 | 유료/비공개 콘텐츠 배포. |
| Lambda@Edge/CloudFront Functions | edge 요청/응답 조작 | 가벼운 인증/리다이렉션/헤더 처리. |
| Origin Shield | origin 부하 추가 감소 | 대규모 글로벌 캐시 최적화. |
| Origin group / origin failover | Primary/Secondary origin을 묶고 장애 조건 시 보조 origin으로 전환 | CloudFront 앞단에서 빠른 HTTP(S) origin 장애 조치가 필요하면 Route 53 DNS failover보다 우선 검토. |
| Origin timeout/attempts | origin 연결 timeout, 연결 시도 횟수, response timeout 조정 | failover 속도는 DNS TTL이 아니라 CloudFront가 origin 장애를 판단하는 시간에도 좌우된다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon CloudFront]] | HTTP(S) CDN/edge cache | 웹 콘텐츠 가속, S3/ALB origin 보호 | DNS 라우팅 자체는 Route 53 |
| [[AWS Global Accelerator]] | Anycast IP L4 가속 | TCP/UDP, 고정 IP, 빠른 failover | 콘텐츠 캐싱 없음 |
| [[Amazon Route 53]] | DNS 라우팅 정책 | 도메인/health check 기반 선택 | edge cache와 TLS/CDN 기능 없음 |
| [[Elastic Load Balancer (ELB)]] | 리전 내 로드 밸런싱 | origin 또는 앱 계층 분산 | 전 세계 edge cache가 아님 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: S3 정적 웹 콘텐츠 전역 배포

- **요구사항**: 전 세계 사용자에게 낮은 지연시간과 S3 비공개 origin 필요
- **정답 단서**: CDN, S3 origin, private bucket, cache
- **선택할 구성**: CloudFront + S3 OAC + WAF
- **오답 함정**: S3 public website만 쓰면 보안/성능/edge 제어가 부족하다.

### 패턴 2: 동적 API 앞 가속과 보호

- **요구사항**: ALB/API Gateway origin 앞에서 TLS/WAF/edge routing 필요
- **정답 단서**: HTTP acceleration, WAF, origin offload
- **선택할 구성**: CloudFront distribution + ALB/API origin
- **오답 함정**: Global Accelerator는 캐싱/HTTP behavior가 없다.

### 패턴 3: 단일 CloudFront distribution에서 가장 빠른 DR origin failover

- **요구사항**: CloudFront 뒤에 Primary Region과 DR Region origin이 있고, DNS failover보다 빠른 전환 필요
- **정답 단서**: single CloudFront distribution, origin, primary/secondary backend, fastest failover
- **선택할 구성**: CloudFront origin group + cache behavior의 origin failover
- **오답 함정**: Route 53 failover는 DNS 캐시/TTL 영향을 받으므로 CloudFront가 직접 보조 origin으로 재시도하는 것보다 느릴 수 있다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- CloudFront는 DNS 서비스가 아니므로 도메인 등록/권한 DNS는 Route 53과 조합한다.
- 캐시 키에 헤더/쿠키/쿼리를 과도하게 포함하면 cache hit ratio가 떨어진다.
- S3 origin 보호는 OAC/OAI를 사용하고 bucket public access와 혼동하지 않는다.
- origin failover는 cache miss 또는 origin 요청 시 동작한다. 이미 edge에 캐시된 객체는 origin 장애와 무관하게 캐시에서 응답될 수 있다.
- CloudFront origin failover는 주로 `GET`, `HEAD`, `OPTIONS` 요청에서 동작한다. 쓰기 요청(`POST`, `PUT` 등)까지 자동 DR 전환된다고 가정하면 안 된다.

## 6. 암기 문장

- HTTP 콘텐츠를 edge에서 캐싱/보호하면 CloudFront다.
- Anycast L4 가속은 Global Accelerator, DNS 라우팅은 Route 53과 구분한다.

## 참고 링크

- [What is Amazon CloudFront?](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [CloudFront cache behavior settings](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DownloadDistValuesCacheBehavior.html)
- [Optimize high availability with CloudFront origin failover](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html)
- [Restrict access to an Amazon S3 origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
