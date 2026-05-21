---
type: aws-service
service_name: "AWS Outposts"
category: "03-Computing/Hybrid&Edge"
exam: SAP-C02
exam_domains:
  - "1. 조직 복잡성"
  - "4. 마이그레이션/현대화"
status: draft
priority: high
aliases:
  - Outposts
  - AWS Outposts rack
  - AWS Outposts server
tags:
  - aws
  - sap-c02
  - compute
  - hybrid
  - edge
created: 2026-05-20
updated: 2026-05-20
---

# AWS Outposts

> [!summary] 한 줄 요약
> AWS Outposts는 AWS가 관리하는 하드웨어와 일부 AWS 서비스를 고객 온프레미스 위치에 배치해 로컬 지연시간·데이터 상주 요구와 AWS 운영 모델을 동시에 만족시키는 하이브리드 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 하이브리드 아키텍처, 온프레미스 저지연, 데이터 상주/로컬 처리, AWS API 일관성 |
| 핵심 의사결정 | 워크로드를 고객 시설 안에 둬야 하지만 AWS 인프라/API/운영 모델을 사용해야 하는가 |
| 대표 키워드 | on premises, low latency to local systems, data residency, AWS managed hardware, same AWS APIs, service link |
| 자주 비교되는 서비스 | [[AWS Local Zones]], [[AWS Wavelength]], [[AWS Direct Connect]], [[Amazon EC2]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 인프라, 서비스, API, 도구를 고객 데이터센터/시설로 확장하는 완전관리형 하드웨어/서비스.
- **왜 쓰는가?**: 로컬 시스템과 매우 낮은 지연시간이 필요하거나 데이터/처리를 현장에 둬야 하지만 AWS 운영 방식을 유지해야 할 때 사용한다.
- **관리형/비관리형 여부**: Outposts 하드웨어는 AWS가 소유·운영·모니터링하지만, 고객은 시설, 전원, 네트워크 연결, 애플리케이션을 책임진다.
- **리전/글로벌 서비스 여부**: Outpost는 특정 home Region에 연결되며, 해당 리전의 VPC를 Outpost subnet으로 확장한다.
- **핵심 제약/한계**: 지원 서비스/인스턴스/용량이 리전과 동일하지 않으며, service link와 온프레미스 시설 요구사항이 중요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Outpost site | 고객 시설 위치 | 전원/공간/네트워크 요구를 고객이 충족해야 한다. |
| Outpost rack/server | AWS 관리 하드웨어 폼팩터 | 온프레미스에 AWS compute/storage 용량을 배치한다. |
| Home Region | Outpost가 연결되는 AWS 리전 | 제어 plane과 관리가 home Region과 연결된다. |
| Service link | Outpost와 AWS Region 간 연결 | 관리/제어/리전 서비스 접근에 필수 경로다. |
| Outpost subnet | VPC를 Outpost로 확장한 subnet | EC2/EBS/ECS/RDS 등 지원 리소스를 로컬에 배치한다. |
| Local gateway | 온프레미스 네트워크와 Outpost 리소스 연결 | 로컬 시스템 저지연 접근의 핵심이다. |
| Capacity management | 설치된 하드웨어 용량 한계 | 클라우드 리전처럼 즉시 무한 확장되지 않는다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Outposts]] vs [[AWS Local Zones]] | Outposts는 고객 시설, Local Zones는 AWS가 운영하는 metro edge 위치 | 고객 건물 안 로컬 시스템/데이터 상주가 필요하면 Outposts | 단순 도시권 저지연이면 Local Zones가 더 적합할 수 있다. |
| [[AWS Outposts]] vs [[AWS Wavelength]] | Wavelength는 통신사 5G edge, Outposts는 고객 온프레미스 | 모바일/5G 사용자 초저지연은 Wavelength | 온프레미스 공장/병원 시스템 연동은 Outposts가 더 자연스럽다. |
| [[AWS Outposts]] vs [[AWS Direct Connect]] | Direct Connect는 연결, Outposts는 현장 AWS 인프라 | 온프레미스에 compute/storage 자체가 필요하면 Outposts | 네트워크 연결만 개선하려면 Direct Connect로 충분할 수 있다. |
| [[AWS Outposts]] vs [[Amazon EC2]] in Region | Outposts는 로컬 배치, Region EC2는 리전 데이터센터 | 현장 지연시간/데이터 상주가 핵심이면 Outposts | 일반 확장성과 서비스 다양성은 Region이 더 크다. |

## 4. 설계 시 고려사항

- Outpost subnet은 리전 VPC의 확장으로 보고, route table/security group/NACL 등 VPC 개념을 함께 사용한다.
- service link가 끊겨도 일부 로컬 데이터 plane은 계속 동작할 수 있지만, 관리 plane/리전 서비스 의존성을 설계해야 한다.
- 용량은 설치된 하드웨어에 묶이므로 사전 capacity planning과 장애 시 여유 용량이 중요하다.
- 온프레미스 네트워크와 통합하려면 local gateway, Direct Connect/VPN, 라우팅 설계를 명확히 한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 공장/병원 로컬 시스템 저지연 처리

- **요구사항**: 현장 장비와 ms 단위 지연시간, 데이터 현장 처리, AWS API 사용.
- **정답 단서**: on-premises, low latency to local systems, data residency, AWS managed infrastructure.
- **선택할 구성**: AWS Outposts + local gateway + Outpost subnet.
- **오답 함정**: 리전 EC2 + VPN/DX는 네트워크 왕복 지연이 요구사항을 넘을 수 있다.

### 패턴 2: 동일한 AWS 운영 모델의 하이브리드 확장

- **요구사항**: 온프레미스에서도 EC2/EBS/ECS/RDS 일부를 AWS 방식으로 운영.
- **정답 단서**: same AWS APIs/tools on premises.
- **선택할 구성**: Outposts rack/server.
- **오답 함정**: VMware/기존 서버 운영은 AWS API 일관성을 제공하지 않는다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Outposts는 “AWS 리전을 더 가까운 곳에 복제”하는 서비스가 아니라, 제한된 AWS 인프라 용량을 고객 시설에 배치하는 서비스다.

- 모든 AWS 서비스가 Outposts에서 동작하는 것은 아니다.
- 용량은 설치된 하드웨어에 제한된다.
- Outposts는 home Region과 연결되어 관리된다.
- 고객은 시설/전원/물리 네트워크 준비 책임이 있다.

## 7. 암기 문장

- 고객 사이트 안에 AWS 관리 인프라가 필요하면 Outposts다.
- 도시권 edge는 Local Zones, 5G 통신사 edge는 Wavelength, 전용 연결은 Direct Connect와 구분한다.

## 8. 참고 링크

- [What is AWS Outposts?](https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html)
- [How AWS Outposts works](https://docs.aws.amazon.com/outposts/latest/userguide/how-outposts-works.html)
- [Outpost networking](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-networking-components.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
