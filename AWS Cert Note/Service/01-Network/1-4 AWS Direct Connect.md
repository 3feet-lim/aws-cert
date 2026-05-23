---
type: aws-service
service_name: "AWS Direct Connect"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Direct Connect", "DX"]
tags: [aws, sap-c02, networking, hybrid, direct-connect]
created: 2026-05-23
updated: 2026-05-23
---

# AWS Direct Connect

> [!summary] 한 줄 요약
> 온프레미스와 AWS 사이에 인터넷을 우회하는 전용 네트워크 연결을 제공해 예측 가능한 대역폭과 지연시간을 확보하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 하이브리드 연결, 일관된 대역폭/지연시간, 대용량 데이터 전송, 전용 회선 이중화 |
| 핵심 의사결정 | 인터넷 VPN보다 안정적이고 예측 가능한 전용 연결이 필요하면 Direct Connect |
| 대표 키워드 | dedicated connection, private VIF, public VIF, transit VIF, DX gateway, MACsec, hosted connection |
| 자주 비교되는 서비스 | [[AWS VPN]], [[AWS Transit Gateway]], [[AWS Direct Connect Gateway]], [[AWS DataSync]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS Direct Connect location을 통해 고객 라우터와 AWS를 전용 네트워크로 연결하는 서비스.
- **왜 쓰는가?**: 인터넷 경로의 변동성을 줄이고 대용량/지속 하이브리드 트래픽을 안정적으로 처리하기 위해 사용한다.
- **관리형 여부**: AWS는 DX 포트/연결을 제공하지만 회선 사업자, 고객 라우터, BGP, 이중화 설계는 사용자가 책임진다.
- **리전/글로벌**: 연결은 DX location에 있고 VIF/DX gateway로 리전/VPC에 연결한다.
- **핵심 제약/한계**: 기본적으로 암호화 터널은 아니며, 암호화 요구는 VPN over DX 또는 MACsec 지원 여부를 고려한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Dedicated/Hosted connection | 전용 또는 파트너 연결 | 대역폭/운영 모델 선택. |
| Private VIF | VPC private IP 대역 접근 | 단일 VPC/VGW 또는 DXGW 연결. |
| Public VIF | AWS public service endpoint 접근 | S3 public endpoint 등 인터넷 우회 경로. |
| Transit VIF | Direct Connect gateway와 TGW 연결 | 다수 VPC 하이브리드 연결 단서. |
| Direct Connect gateway | 여러 리전/VPC 연결 확장 | 글로벌 하이브리드 네트워크 설계. |
| Resiliency Toolkit | 이중 연결 권장 패턴 | 단일 DX 회선 장애 방지. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Direct Connect]] | 전용 네트워크 연결 | 예측 가능한 성능/대용량/장기 하이브리드 | 기본 암호화 터널로 오해 금지 |
| [[AWS VPN]] | 인터넷 기반 IPsec 터널 | 빠른 구축/암호화/백업 회선 | 대역폭/지연시간 변동 가능 |
| VPN over Direct Connect | DX 위에 IPsec 암호화 | 전용 회선 + 암호화 요구 | DX만으로 암호화 요구를 만족한다고 단정 금지 |
| [[AWS DataSync]] | 데이터 이동 서비스 | 파일/객체 데이터 마이그레이션 | 네트워크 회선 자체가 아님 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 데이터센터와 AWS 상시 연결

- **요구사항**: 대규모 트래픽과 예측 가능한 지연시간 필요
- **정답 단서**: dedicated, predictable bandwidth, hybrid
- **선택할 구성**: Dual Direct Connect + private/transit VIF
- **오답 함정**: Site-to-Site VPN은 빠르지만 인터넷 경로 변동성이 있다.

### 패턴 2: 암호화된 하이브리드 연결

- **요구사항**: 전용선 성능과 전송 암호화 모두 필요
- **정답 단서**: encryption required, dedicated connection
- **선택할 구성**: VPN over Direct Connect 또는 MACsec 지원 연결
- **오답 함정**: Direct Connect 자체를 항상 암호화된 터널로 착각하면 안 된다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- Direct Connect는 전용 연결이지만 기본적으로 IPsec VPN과 같은 암호화 터널은 아니다.
- 고가용성은 서로 다른 DX location/장비/회선 이중화가 핵심이다.
- 다수 VPC 연결은 DX 단독보다 DX gateway + TGW 조합을 본다.

## 6. 암기 문장

- 예측 가능한 전용 하이브리드 회선은 Direct Connect다.
- 빠른 암호화 연결은 VPN, 대규모 VPC 라우팅은 TGW와 조합한다.

## 참고 링크

- [What is AWS Direct Connect?](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
- [AWS Direct Connect virtual interfaces](https://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html)
- [AWS Direct Connect resiliency recommendations](https://docs.aws.amazon.com/directconnect/latest/UserGuide/resiliency_toolkit.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
