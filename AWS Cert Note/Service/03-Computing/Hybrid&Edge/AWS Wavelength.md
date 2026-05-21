---
type: aws-service
service_name: "AWS Wavelength"
category: "03-Computing/Hybrid&Edge"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: medium
aliases:
  - Wavelength
  - Wavelength Zones
tags:
  - aws
  - sap-c02
  - compute
  - edge
  - 5g
created: 2026-05-20
updated: 2026-05-20
---

# AWS Wavelength

> [!summary] 한 줄 요약
> AWS Wavelength는 통신사 5G 네트워크 edge에 AWS compute/storage를 배치해 모바일·엣지 사용자에게 초저지연 애플리케이션을 제공하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 모바일/5G 초저지연, 통신사 edge, 실시간 미디어/게임/AR/VR/차량 애플리케이션 |
| 핵심 의사결정 | 최종 사용자가 통신사 5G망에 있고 ms 단위 지연시간이 가장 중요한가 |
| 대표 키워드 | 5G, mobile edge, ultra-low latency, carrier network, Wavelength Zone, carrier gateway |
| 자주 비교되는 서비스 | [[AWS Outposts]], [[AWS Local Zones]], [[Amazon CloudFront]], [[Amazon EC2]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: AWS compute/storage 서비스를 통신사 5G 네트워크 내부 또는 가까운 edge 위치인 Wavelength Zone에 배치하는 서비스.
- **왜 쓰는가?**: 모바일 사용자/기기와 애플리케이션 서버 사이의 네트워크 홉을 줄여 초저지연을 달성하기 위해 사용한다.
- **관리형/비관리형 여부**: AWS가 Wavelength Zone 인프라를 제공하지만, 애플리케이션/EC2/네트워크/보안 구성은 사용자가 설계한다.
- **리전/글로벌 서비스 여부**: Wavelength Zone은 parent Region과 연결된 edge zone이며 opt-in이 필요할 수 있다.
- **핵심 제약/한계**: 지원 리전/통신사/서비스가 제한적이고, 일반 글로벌 캐싱이나 온프레미스 배치 요구와 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Wavelength Zone | 통신사 edge에 있는 AWS zone | 모바일/5G 사용자와 가까운 compute 배치가 핵심이다. |
| Carrier gateway | Wavelength subnet과 통신사망/인터넷 연결 | Wavelength 네트워킹의 대표 구성요소다. |
| Wavelength subnet | VPC를 Wavelength Zone으로 확장 | 리전 VPC와 edge subnet 개념을 함께 이해한다. |
| EC2 at edge | Wavelength Zone에 EC2 배치 | 애플리케이션 서버를 사용자 가까이에 둔다. |
| Regional services connection | 리전 AWS 서비스와 연동 | edge 처리와 리전 backend를 분리하는 설계가 자주 나온다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Wavelength]] vs [[AWS Outposts]] | Wavelength는 통신사 5G edge, Outposts는 고객 온프레미스 | 모바일/5G 사용자 초저지연이면 Wavelength | 고객 데이터센터 안 배치는 Outposts다. |
| [[AWS Wavelength]] vs [[AWS Local Zones]] | Local Zones는 대도시권 AWS edge, Wavelength는 carrier 5G edge | 통신사망 내부 모바일 지연시간이 핵심이면 Wavelength | 일반 도시권 사용자/미디어 제작 지연시간은 Local Zones일 수 있다. |
| [[AWS Wavelength]] vs [[Amazon CloudFront]] | CloudFront는 콘텐츠 캐싱/CDN, Wavelength는 애플리케이션 compute edge | 동적 실시간 처리와 5G edge compute는 Wavelength | 정적 콘텐츠 전송 최적화는 CloudFront가 더 적합하다. |
| [[AWS Wavelength]] vs Region EC2 | Wavelength는 사용자 가까운 edge, Region EC2는 리전 데이터센터 | 초저지연이 핵심이면 Wavelength | 일반 웹앱은 리전 + CloudFront/Global Accelerator로 충분할 수 있다. |

## 4. 설계 시 고려사항

- Wavelength Zone을 opt-in하고, VPC/subnet/carrier gateway/route table을 구성한다.
- Edge에는 지연시간 민감 처리만 두고, 데이터 저장/관리/분석은 Region 서비스와 분리하는 패턴이 많다.
- 통신사와 지역 가용성을 확인해야 하며, 멀티 리전/멀티 edge DR 전략은 서비스 가용 범위에 좌우된다.
- 사용자 단말이 어느 통신사/지역에서 접속하는지가 설계의 핵심이다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 5G AR/VR 초저지연 처리

- **요구사항**: 모바일 기기에서 실시간 렌더링/분석, 지연시간 최소화.
- **정답 단서**: 5G, mobile users, ultra-low latency, carrier network.
- **선택할 구성**: EC2 in Wavelength Zone + carrier gateway + regional backend.
- **오답 함정**: CloudFront는 정적/캐시 가능한 콘텐츠에는 좋지만 실시간 동적 compute edge와 다르다.

### 패턴 2: 연결 차량/스마트팩토리 모바일 edge

- **요구사항**: 통신사망 근처에서 실시간 판단 후 리전으로 데이터 집계.
- **정답 단서**: connected vehicles, real-time, telco edge.
- **선택할 구성**: Wavelength Zone compute + Region analytics/storage.
- **오답 함정**: Outposts는 고객 시설에 장비를 설치하는 패턴이다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Wavelength의 핵심 단서는 “5G/mobile carrier edge”다. 단순 edge라는 단어만으로 선택하지 않는다.

- 모든 리전과 통신사에서 사용할 수 있는 것은 아니다.
- 일반 CDN 캐싱은 CloudFront가 더 적합하다.
- 온프레미스 저지연은 Outposts, 대도시권 AWS edge는 Local Zones와 비교한다.

## 7. 암기 문장

- 5G 통신사망 가까이 compute를 두면 Wavelength다.
- 고객 시설은 Outposts, 도시권 AWS edge는 Local Zones, 정적 콘텐츠 edge는 CloudFront다.

## 8. 참고 링크

- [AWS Wavelength Documentation](https://docs.aws.amazon.com/wavelength/)
- [Get started with AWS Wavelength](https://docs.aws.amazon.com/wavelength/latest/developerguide/get-started-wavelength.html)
- [Use cases for AWS Wavelength](https://docs.aws.amazon.com/wavelength/latest/developerguide/wavelength-use-cases.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
