---
type: aws-service
service_name: "Amazon VPC"
category: "01-Network"
exam: SAP-C02
exam_domains:
  - "1. 조직 복잡성"
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
  - "4. 마이그레이션/현대화"
status: draft
priority: high
aliases:
  - VPC
  - Virtual Private Cloud
tags:
  - aws
  - sap-c02
  - networking
created: 2026-05-19
updated: 2026-05-19
---

# Amazon VPC

> [!summary] 한 줄 요약
> Amazon VPC는 AWS 계정 안에 격리된 가상 네트워크를 만들고, 서브넷·라우팅·보안 경계·연결 옵션을 설계해 워크로드의 네트워크 동작을 결정하는 기반 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 신규 아키텍처 네트워크 설계, 멀티 계정/멀티 VPC 연결, 온프레미스 연동, private access, 보안 경계 |
| 핵심 의사결정 | CIDR/서브넷/AZ/라우팅/게이트웨이/엔드포인트/연결 방식을 요구사항에 맞게 조합하는 것 |
| 대표 키워드 | public/private subnet, route table, NAT Gateway, Internet Gateway, VPC endpoint, PrivateLink, peering, Transit Gateway, hybrid connectivity |
| 자주 비교되는 서비스 | [[AWS Transit Gateway]], [[AWS PrivateLink]], [[AWS VPN]], [[AWS Direct Connect]], [[Amazon Route 53]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS 계정 전용의 논리적으로 격리된 가상 네트워크. IP 범위, 서브넷, 라우팅, 게이트웨이, 보안 그룹 등을 직접 설계한다.
- **왜 쓰는가?**: 애플리케이션을 어느 네트워크 경계에 배치하고, 어떤 경로로 인터넷/다른 VPC/온프레미스/AWS 서비스에 접근할지 통제하기 위해 사용한다.
- **관리형/비관리형 여부**: VPC 자체와 라우터는 AWS 관리형이지만, CIDR·라우팅·보안·연결 설계 책임은 사용자에게 있다.
- **리전/글로벌 서비스 여부**: VPC는 리전 단위 리소스이며, 한 VPC는 해당 리전의 여러 AZ에 걸칠 수 있다. 서브넷은 하나의 AZ에 속한다.
- **핵심 제약/한계**: CIDR 중복은 VPC Peering/TGW/하이브리드 연결 설계의 큰 제약이 된다. 서브넷 라우팅은 route table association에 의해 결정된다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| VPC CIDR | VPC의 IPv4/IPv6 주소 범위 | 온프레미스, 다른 VPC, 인수합병 환경과 연결하려면 CIDR 중복을 피해야 한다. |
| Subnet | VPC CIDR 일부를 AZ 단위로 나눈 네트워크 범위 | 고가용성은 보통 여러 AZ의 private subnet에 워크로드를 분산하는 방식으로 출제된다. |
| Route Table | 서브넷 트래픽의 목적지와 타깃을 결정 | public/private subnet의 본질은 이름이 아니라 route table이다. |
| Internet Gateway | VPC와 인터넷 간 IPv4/IPv6 인바운드·아웃바운드 경로 | public subnet은 IGW로 향하는 기본 경로와 퍼블릭 주소 조건이 필요하다. |
| NAT Gateway | private subnet 리소스의 아웃바운드 IPv4 인터넷 접근 | 인바운드 인터넷 접근을 열지 않고 패치/업데이트를 허용할 때 사용한다. AZ별 배치와 비용을 고려한다. |
| Egress-only Internet Gateway | IPv6 아웃바운드 전용 인터넷 경로 | IPv6에는 NAT Gateway 개념이 없다는 함정과 함께 출제될 수 있다. |
| Security Group | ENI/리소스 수준 stateful 방화벽 | 허용 규칙 중심. 응답 트래픽은 자동 허용된다. |
| Network ACL | 서브넷 수준 stateless 방화벽 | inbound/outbound와 ephemeral port를 모두 고려해야 한다. 명시적 deny가 가능하다. |
| VPC Flow Logs | VPC/Subnet/ENI 단위 IP 트래픽 메타데이터 로깅 | 보안 분석, 연결 문제 진단, 과도하게 제한/허용된 규칙 탐지에 사용한다. |
| VPC Endpoint | VPC에서 AWS 서비스로 private access | S3/DynamoDB gateway endpoint와 PrivateLink 기반 interface endpoint를 구분해야 한다. |

## 3. 설계 시 고려사항

### 네트워크 / 라우팅

- **public subnet**: `0.0.0.0/0` 또는 `::/0` 경로가 Internet Gateway로 향하고, 리소스에 퍼블릭 주소가 있어 인터넷과 직접 통신 가능하다.
- **private subnet**: 인터넷에서 직접 들어오는 경로를 만들지 않고, 필요 시 NAT Gateway나 VPC endpoint를 통해 outbound 또는 AWS 서비스 접근을 제공한다.
- **route table은 서브넷 단위로 적용**된다. 명시적으로 연결하지 않은 서브넷은 main route table을 따른다.
- **라우팅은 보안 허용과 다르다**. route table이 경로를 열어도 Security Group/NACL에서 막히면 통신되지 않는다.

### 보안 경계

- Security Group은 리소스/ENI 중심, stateful, allow rule 기반이다.
- NACL은 서브넷 중심, stateless, allow/deny rule 기반이다.
- 민감 워크로드는 private subnet에 두고, ALB/NLB, NAT Gateway, VPC endpoint, PrivateLink 등 필요한 통로만 열어야 한다.
- Flow Logs는 payload가 아니라 IP 트래픽 메타데이터를 기록한다. 패킷 내용을 봐야 하는 경우 Traffic Mirroring을 검토한다.

### 계정 / 조직 구조

- 멀티 계정에서는 VPC를 계정별로 분리하고, 공유 서비스 VPC·보안 VPC·워크로드 VPC를 Transit Gateway로 연결하는 패턴이 자주 나온다.
- VPC sharing은 Organizations/RAM과 함께 서브넷을 여러 계정에 공유할 수 있지만, 네트워크 소유권과 리소스 소유권을 구분해야 한다.
- 중앙 egress, 중앙 inspection, shared services DNS 같은 요구사항은 VPC 단독보다 Transit Gateway/Network Firewall/Route 53 Resolver와 함께 설계한다.

### 성능 / 확장성

- VPC 자체 라우터는 관리형이므로 일반적으로 사용자가 라우터 용량을 프로비저닝하지 않는다.
- NAT Gateway, Transit Gateway attachment, VPN, Direct Connect, endpoint 등 연결 구성 요소별 처리량/가용성/비용이 병목 또는 설계 포인트가 된다.
- AZ 장애 대응을 위해 private subnet과 NAT Gateway를 여러 AZ에 배치하는 구성이 선호된다.

## 4. 연결 옵션 / 선택 기준

| 요구사항 | 선택 후보 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| 소수 VPC 간 단순 private 연결 | [[VPC Peering]] | CIDR이 겹치지 않고, 전이 라우팅이 필요 없고, 연결 수가 적을 때 | Peering은 transitive routing을 지원하지 않는다. |
| 수십~수천 VPC와 온프레미스 중앙 연결 | [[AWS Transit Gateway]] | hub-and-spoke, 중앙 라우팅, 멀티 계정 네트워크 통합 | 단순 1:1 연결에 TGW를 쓰면 비용/복잡도가 과할 수 있다. |
| 다른 계정/VPC의 서비스만 private로 노출 | [[AWS PrivateLink]] | 소비자는 서비스 제공자 VPC와 CIDR이 겹쳐도 private endpoint로 접근 가능 | 전체 네트워크 간 라우팅이 아니라 특정 서비스 접근이다. |
| 온프레미스와 빠른 구축 암호화 연결 | [[AWS VPN]] | 인터넷 기반 IPsec VPN, 빠른 구축, 백업 회선 | 일관된 대역폭/지연시간 요구에는 Direct Connect가 더 적합할 수 있다. |
| 온프레미스와 전용선 기반 안정 연결 | [[AWS Direct Connect]] | 예측 가능한 성능, 대역폭, 전용 연결 | 암호화는 기본 제공이 아니므로 필요 시 VPN over DX/MACsec 등을 검토한다. |
| AWS 서비스에 인터넷 없이 접근 | VPC Endpoint | S3/DynamoDB는 gateway endpoint, 많은 AWS 서비스는 interface endpoint | gateway endpoint는 PrivateLink가 아니다. |

## 5. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Security Group]] vs [[Network ACL]] | SG는 리소스/ENI 수준 stateful, NACL은 서브넷 수준 stateless | 인스턴스별 접근 제어는 SG, 서브넷 경계의 명시적 deny/대략적 제어는 NACL | NACL은 outbound/ephemeral port도 열어야 한다. |
| [[NAT Gateway]] vs [[Internet Gateway]] | NAT GW는 private subnet의 outbound IPv4, IGW는 VPC 인터넷 경로 | 외부에서 직접 접근 금지 + outbound만 필요하면 NAT GW | NAT GW를 둔다고 private subnet이 inbound public이 되지는 않는다. |
| Gateway Endpoint vs Interface Endpoint | Gateway는 route table 대상, Interface는 ENI/PrivateLink 기반 | S3/DynamoDB는 gateway endpoint가 비용/라우팅상 자주 정답 | 모든 VPC endpoint가 PrivateLink라고 생각하면 틀린다. |
| VPC Peering vs Transit Gateway | Peering은 1:1 비전이 연결, TGW는 중앙 허브 라우팅 | 규모와 중앙 통제가 필요하면 TGW | Peering으로 대규모 mesh를 만들면 운영 복잡도가 커진다. |
| PrivateLink vs Peering/TGW | PrivateLink는 특정 서비스 endpoint 노출, 네트워크 전체 연결 아님 | 공급자 서비스를 소비자 VPC에 private하게 제공 | 양방향 전체 통신이나 라우팅 전파 요구에는 부적합하다. |

## 6. 아키텍처 / 그림

> [!note] PNG 그림
> `attachments/aws/amazon-vpc-architecture.png` 파일을 바로 Obsidian에서 볼 수 있게 추가했다.
> 스타일은 draw.io처럼 박스·화살표 중심의 선형 아키텍처로 유지한다.

![[attachments/aws/amazon-vpc-architecture.png]]

그림은 다음 요소만 포함한다.

- Region / VPC / 2개 AZ 경계
- Public subnet: ALB, NAT Gateway, Internet Gateway route
- Private subnet: EC2/Application, NAT Gateway outbound route
- Gateway VPC endpoint: S3 접근
- 빨간 콜아웃: private subnet outbound와 inbound public 접근을 혼동하지 말 것

## 7. 보안 / 거버넌스

- **IAM 권한 모델**: VPC 리소스 생성/변경은 IAM으로 통제하지만, 실제 패킷 허용은 route table, SG, NACL, endpoint policy 등 네트워크 제어가 담당한다.
- **암호화**: VPC 자체가 트래픽을 자동으로 전부 암호화한다는 식으로 이해하면 안 된다. 전송 중 암호화는 TLS, VPN, DX 암호화 옵션, 서비스별 설정으로 설계한다.
- **네트워크 접근 제어**: SG/NACL/route table/endpoint policy를 조합한다.
- **감사/로깅**: CloudTrail로 API 변경을 추적하고, VPC Flow Logs로 IP 트래픽 메타데이터를 분석한다.
- **조직 단위 통제**: SCP로 네트워크 리소스 생성 권한을 제한하거나, Control Tower/Organizations 기반으로 계정별 네트워크 경계를 표준화할 수 있다.

## 8. 가용성 / 복원력

- VPC는 리전 범위이고 서브넷은 AZ 범위이므로, 워크로드는 여러 AZ의 private subnet에 배치한다.
- NAT Gateway는 AZ별로 두고 각 AZ의 private subnet이 같은 AZ의 NAT Gateway를 사용하게 하면 AZ 장애 영향을 줄일 수 있다.
- VPC endpoint를 사용하면 NAT Gateway/IGW 경유 없이 AWS 서비스 접근 경로를 줄여 보안과 가용성을 개선할 수 있다.
- 온프레미스 연결은 VPN 이중 터널, Direct Connect 이중화, DX + VPN 백업, Transit Gateway 중앙 연결 등을 요구사항에 맞게 조합한다.

## 9. 비용 / 운영 포인트

- VPC 자체보다 NAT Gateway, Transit Gateway, VPC endpoints, VPN, Direct Connect, 데이터 처리/전송 비용이 시험 포인트다.
- S3/DynamoDB 접근이 많은 private subnet은 NAT Gateway 대신 gateway endpoint를 사용하면 보안과 비용 측면에서 유리한 경우가 많다.
- 중앙 집중형 NAT/inspection은 운영 통제를 단순화할 수 있지만, cross-AZ/cross-VPC 데이터 처리 비용과 장애 blast radius를 함께 검토해야 한다.

## 10. 헷갈리는 포인트

> [!warning] 주의
> VPC 문제는 “서비스 이름”보다 **라우팅 경로 + 보안 경계 + 연결 범위**를 묻는 경우가 많다.

- public/private subnet은 이름이 아니라 route table과 public IP 조건으로 결정된다.
- Security Group은 deny rule을 만들 수 없다. 명시적 차단이 필요하면 NACL 또는 다른 네트워크 보안 서비스를 검토한다.
- NACL은 stateless이므로 응답 트래픽 포트도 고려해야 한다.
- NAT Gateway는 IPv4 outbound용이다. IPv6 outbound 전용은 egress-only Internet Gateway를 사용한다.
- VPC Peering은 transitive routing이 안 된다. A-B, B-C가 연결되어도 A-C가 자동 통신되는 구조가 아니다.
- PrivateLink는 특정 서비스 접근이지 VPC 전체 네트워크 연결이 아니다.
- Gateway endpoint는 S3/DynamoDB용이며 PrivateLink 기반 interface endpoint와 다르다.

## 11. SAP-C02 시나리오 패턴

### 패턴 1: Private subnet에서 S3 접근, 인터넷 노출 금지

- **요구사항**: EC2가 S3에 접근해야 하지만 인터넷 경로를 사용하지 않아야 한다.
- **정답 단서**: private subnet, no internet exposure, S3, cost-effective/private access.
- **선택할 구성**: S3 Gateway VPC Endpoint + route table 연결 + endpoint policy.
- **오답 함정**: NAT Gateway를 통해 S3 public endpoint로 나가는 구성은 가능하지만 “인터넷 경로 없이/private access” 요구에는 덜 적합하다.

### 패턴 2: 수십 개 VPC와 온프레미스 네트워크 중앙 연결

- **요구사항**: 여러 계정/VPC와 온프레미스를 중앙에서 라우팅하고 분리된 라우팅 도메인을 운영한다.
- **정답 단서**: many VPCs, hub-and-spoke, centralized routing, hybrid.
- **선택할 구성**: AWS Transit Gateway + TGW route tables + VPN/DX attachment.
- **오답 함정**: VPC Peering mesh는 전이 라우팅 부재와 운영 복잡도 때문에 대규모 중앙 연결에 부적합하다.

### 패턴 3: SaaS/공유 서비스 private 제공, CIDR 중복 가능

- **요구사항**: 서비스 제공자 VPC의 특정 애플리케이션을 여러 소비자 VPC가 private하게 접근한다. VPC 간 CIDR이 겹칠 수 있다.
- **정답 단서**: provider/consumer, private service access, overlapping CIDR, no full network connectivity.
- **선택할 구성**: AWS PrivateLink / Interface Endpoint / Endpoint Service.
- **오답 함정**: Peering/TGW는 CIDR 중복과 전체 네트워크 연결 문제 때문에 요구사항과 맞지 않을 수 있다.

## 12. 암기 문장

- VPC 문제는 “어디에 배치할지”보다 “어떤 경로와 경계로 통신시킬지”를 묻는다.
- public subnet은 IGW route와 public address, private subnet은 NAT/endpoint/TGW 등 통제된 경로가 핵심이다.
- 대규모 연결은 Transit Gateway, 특정 서비스 private 노출은 PrivateLink, S3/DynamoDB private access는 gateway endpoint를 먼저 떠올린다.

## 13. 참고 링크

- [Amazon VPC - How Amazon VPC works](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
- [VPC basics](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnet-basics.html)
- [Subnet route tables](https://docs.aws.amazon.com/vpc/latest/userguide/subnet-route-tables.html)
- [Ensure internetwork traffic privacy in Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html)
- [Gateway endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html)
- [AWS PrivateLink concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html)
- [How AWS Transit Gateway works](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-isolated.html)
