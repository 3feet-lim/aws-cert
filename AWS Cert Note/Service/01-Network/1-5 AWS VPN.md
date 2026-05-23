---
type: aws-service
service_name: "AWS VPN"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Site-to-Site VPN", "Client VPN", "AWS VPN"]
tags: [aws, sap-c02, networking, vpn, hybrid]
created: 2026-05-23
updated: 2026-05-23
---

# AWS VPN

> [!summary] 한 줄 요약
> 인터넷 기반 IPsec site-to-site 터널 또는 사용자 클라이언트 VPN으로 AWS와 온프레미스/사용자를 암호화 연결하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 빠른 하이브리드 연결, 암호화 터널, Direct Connect 백업, 원격 사용자 접속 |
| 핵심 의사결정 | 전용선 없이 빠르게 암호화 연결이 필요하면 VPN, 안정 대역폭은 Direct Connect와 비교 |
| 대표 키워드 | IPsec, Site-to-Site VPN, Client VPN, customer gateway, virtual private gateway, BGP, backup for DX |
| 자주 비교되는 서비스 | [[AWS Direct Connect]], [[AWS Transit Gateway]], [[AWS Client VPN]], [[AWS PrivateLink]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Site-to-Site VPN과 Client VPN을 포함하는 AWS 암호화 네트워크 연결 서비스.
- **왜 쓰는가?**: 온프레미스 네트워크나 원격 사용자가 AWS VPC에 안전하게 접근하도록 구성한다.
- **관리형 여부**: AWS는 VPN endpoint를 제공하지만 고객 게이트웨이 장비, 라우팅, 터널 이중화, 인증은 설계해야 한다.
- **리전/글로벌**: 리전 서비스이며 VGW 또는 TGW에 연결할 수 있다.
- **핵심 제약/한계**: 인터넷 경로를 사용하므로 대역폭/지연시간은 Direct Connect보다 예측성이 낮을 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Site-to-Site VPN | 온프레미스-AWS IPsec 터널 | 빠른 하이브리드 연결과 DX 백업. |
| Client VPN | 사용자 단말-AWS OpenVPN 기반 접속 | 원격 근무자 private 접속. |
| Customer Gateway | 고객 측 라우터/장비 정의 | 온프레미스 장비 설정 단서. |
| Virtual Private Gateway | 단일 VPC VPN endpoint | 단순 VPC 연결. |
| Transit Gateway attachment | VPN을 TGW에 연결 | 여러 VPC와 온프레미스 확장. |
| Static/BGP routing | 정적 또는 동적 라우팅 | 경로 전파와 장애 조치. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS VPN]] | 인터넷 기반 암호화 터널 | 빠른 구축, 암호화, DX 백업 | 대역폭/지연시간 예측성은 낮음 |
| [[AWS Direct Connect]] | 전용 네트워크 연결 | 일관된 성능/대용량 | 기본 암호화 터널은 아님 |
| [[AWS Transit Gateway]] | 중앙 라우팅 허브 | 여러 VPC에 VPN 연결 확장 | VPN 암호화 터널 자체가 아님 |
| [[AWS PrivateLink]] | 서비스 단위 private access | 특정 서비스 노출 | 온프레미스 전체 네트워크 연결 아님 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: 빠른 하이브리드 PoC

- **요구사항**: 며칠 안에 온프레미스와 VPC를 암호화 연결
- **정답 단서**: quick setup, IPsec, hybrid
- **선택할 구성**: Site-to-Site VPN + VGW/TGW
- **오답 함정**: Direct Connect는 회선 준비 시간이 더 길 수 있다.

### 패턴 2: Direct Connect 장애 대비

- **요구사항**: 전용선 장애 시 암호화된 백업 경로 필요
- **정답 단서**: backup, failover, encrypted tunnel
- **선택할 구성**: Site-to-Site VPN backup over internet
- **오답 함정**: VPN을 주 경로로 쓰면 대역폭 변동을 감수해야 한다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- VPN은 암호화되지만 인터넷 경로의 성능 변동을 피하지 못한다.
- Site-to-Site VPN은 네트워크 간, Client VPN은 사용자 단말 접속이다.
- VPN 두 터널을 제공해도 고객 장비/라우팅 이중화가 없으면 전체 HA가 아니다.

## 6. 암기 문장

- 빠른 암호화 하이브리드 연결은 VPN이다.
- 안정 성능은 Direct Connect, 다수 VPC 확장은 TGW와 조합한다.

## 참고 링크

- [What is AWS Site-to-Site VPN?](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html)
- [What is AWS Client VPN?](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html)
- [Site-to-Site VPN routing options](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPNRoutingTypes.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
