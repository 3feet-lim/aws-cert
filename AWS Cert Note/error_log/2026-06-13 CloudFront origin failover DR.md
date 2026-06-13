---
type: aws-exam-error-log
exam: SAP-C02
created: 2026-06-13
updated: 2026-06-13
question_source: "미제공"
services: ["Amazon CloudFront", "Amazon Route 53"]
related_notes: ["[[Amazon CloudFront]]", "[[Amazon Route 53]]"]
tags: [aws, sap-c02, error-log, cloudfront, route53, dr]
---

# CloudFront origin failover로 DR 전환 시간 단축

> [!summary] 오답 요약
> 단일 [[Amazon CloudFront]] distribution 뒤의 Primary/DR backend 장애 조치를 가장 빠르게 만들려면 DNS 레코드 TTL을 더 줄이는 것이 아니라 CloudFront origin group의 origin failover를 사용한다.

## 1. 문제 상황 요약

- **시나리오**: 대규모 웹사이트가 단일 CloudFront distribution을 사용하고, backend는 기본 AWS Region과 DR Region에 배포되어 있다.
- **현재 구성**: CloudFront origin이 [[Amazon Route 53]] failover record set을 바라보고, Route 53이 primary backend health check와 secondary DR endpoint로 DNS 장애 조치를 수행한다.
- **핵심 요구사항**: 60초 TTL 기반 DNS failover보다 빠른 장애 조치 시간.
- **제약 조건**: 이미 CloudFront가 웹사이트 앞단에 있으므로 viewer traffic은 CloudFront를 통과한다.
- **관련 서비스**: [[Amazon CloudFront]], [[Amazon Route 53]]

## 2. 정답과 오답

| 구분 | 선택지/서비스 | 판단 |
|---|---|---|
| 정답 | d) 두 Region backend를 CloudFront origin group으로 구성하고 cache behavior에서 origin failover 설정 | CloudFront가 primary origin 실패를 감지하면 secondary origin으로 직접 요청을 전환하므로 DNS TTL/recursive resolver cache 대기보다 빠르다. |
| 오답 | a) CloudFront distribution을 추가하고 Route 53 failover로 두 distribution 전환 | 여전히 DNS failover 구조라 TTL과 DNS cache 영향을 받는다. CloudFront distribution을 늘려도 origin 장애 판단이 edge 내부에서 즉시 처리되는 구조가 아니다. |
| 오답 | b) 기존 Route 53 record TTL을 4초로 낮춤 | TTL을 낮추면 DNS cache 시간은 줄 수 있지만 recursive resolver 동작, health check 판정, 전파 지연을 완전히 제거하지 못한다. 문제의 “가장 빠른” 장애 조치에는 CloudFront origin failover가 더 적합하다. |
| 오답 | c) latency-based routing으로 새 record set 생성 | 지연시간 기반 라우팅은 가까운/낮은 지연 Region 선택용이지 active-passive DR failover를 가장 빠르게 만드는 기능이 아니다. |

## 3. 왜 정답인가

- CloudFront origin failover는 **origin group** 안에 primary/secondary origin을 두고 cache behavior가 이 origin group을 사용하게 만드는 구조다.
- primary origin이 지정된 장애 HTTP status code를 반환하거나, 연결 실패/timeout 조건에 걸리면 CloudFront가 secondary origin으로 요청을 라우팅한다.
- 이 판단은 CloudFront의 origin 요청 경로에서 일어나므로, CloudFront origin 이름이 가리키는 Route 53 DNS 응답이 TTL 만료될 때까지 기다리는 구조보다 빠른 DR 전환을 기대할 수 있다.
- Route 53 DNS failover는 DNS 계층에서 유용하지만, 이미 CloudFront가 앞에 있고 origin만 바꾸면 되는 문제에서는 CloudFront origin failover가 더 직접적인 해법이다.

## 4. 다시 풀 때의 판단 규칙

- **키워드**: `single CloudFront distribution`, `origin`, `primary Region + DR Region`, `fastest failover`, `TTL 60 seconds`
- **바로 떠올릴 서비스/기능**: [[Amazon CloudFront]] origin group / origin failover
- **버릴 선택지**:
  - DNS TTL만 낮추는 선택지: DNS cache 의존성을 줄일 뿐 가장 빠른 origin 전환은 아님.
  - latency-based routing: 성능 최적화/지역 선택이지 DR 우선순위 장애 조치가 핵심이 아님.
  - CloudFront distribution 추가 + Route 53 failover: 구조가 커지고 여전히 DNS failover 의존.
- **암기 문장**: CloudFront 뒤 origin 간 빠른 DR 전환은 Route 53 TTL 튜닝보다 CloudFront origin group failover다.

## 5. 서비스 노트 보강 여부

- [x] 관련 서비스 노트가 존재한다: [[Amazon CloudFront]], [[Amazon Route 53]]
- [x] 정답 개념이 서비스 노트에 있다: CloudFront origin group / origin failover 항목 보강
- [x] 오답 비교/함정이 서비스 노트에 있다: Route 53 TTL/DNS cache 함정 및 CloudFront 패턴 보강
- [x] 필요 시 서비스 노트를 업데이트했다: `Service/01-Network/1-8 Amazon CloudFront.md`

## 6. 참고 링크

- [Optimize high availability with CloudFront origin failover](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html)
- [Route 53 TTL values](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values-basic.html#rrsets-values-basic-ttl)
- [Configuring DNS failover in Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover-configuring.html)

## 7. 복습 질문

- CloudFront 앞단이 이미 존재할 때 backend Region 장애 조치를 DNS에서 처리해야 하는가, CloudFront origin에서 처리해야 하는가?
- 문제에서 “TTL 60초인데 1분 이상 걸린다”가 나오면 어떤 계층의 failover 한계를 암시하는가?
