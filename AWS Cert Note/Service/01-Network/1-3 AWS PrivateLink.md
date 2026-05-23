---
type: aws-service
service_name: "AWS PrivateLink"
category: "01-Network"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["PrivateLink", "VPC endpoint service", "Interface endpoint"]
tags: [aws, sap-c02, networking, privatelink, private-access]
created: 2026-05-23
updated: 2026-05-23
---

# AWS PrivateLink

> [!summary] 한 줄 요약
> 소비자 VPC가 퍼블릭 인터넷이나 VPC 전체 연결 없이 특정 서비스에 사설 IP로 접근하게 하는 private connectivity 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 서비스 단위 private access, SaaS/공유 서비스 노출, CIDR 중복 회피, 인터넷 경로 제거 |
| 핵심 의사결정 | 네트워크 전체가 아니라 특정 서비스만 private하게 노출/소비해야 하면 PrivateLink |
| 대표 키워드 | interface endpoint, endpoint service, NLB, private IP, overlapping CIDR, no internet |
| 자주 비교되는 서비스 | [[AWS Transit Gateway]], [[VPC Peering]], [[VPC Endpoint]], [[Amazon API Gateway]] private API |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Interface VPC endpoint와 endpoint service를 기반으로 VPC 간/계정 간 특정 서비스 접근을 제공하는 기술.
- **왜 쓰는가?**: 서비스 제공자와 소비자가 네트워크 전체를 연결하지 않고 안전하게 서비스만 공유하기 위해 사용한다.
- **관리형 여부**: PrivateLink 데이터 경로는 관리형이지만 endpoint policy, 보안 그룹, NLB/서비스 설계는 사용자가 담당한다.
- **리전/글로벌**: 리전 서비스이며 interface endpoint는 subnet에 ENI 형태로 생성된다.
- **핵심 제약/한계**: 라우팅 전파나 양방향 전체 통신을 제공하지 않는다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Interface endpoint | 소비자 VPC의 ENI 기반 endpoint | AWS 서비스/SaaS/endpoint service private 접근. |
| Endpoint service | 제공자 서비스 노출 단위 | NLB/GWLB 뒤 서비스를 소비자에게 제공. |
| Private DNS | 서비스 DNS를 private endpoint로 해석 | 앱 변경 최소화 단서. |
| Endpoint policy | 지원 서비스 접근 제어 | S3 gateway endpoint policy와 구분. |
| Security group | interface endpoint ENI 접근 제어 | 소비자 측 보안 경계. |
| Overlapping CIDR support | 전체 라우팅이 아니므로 CIDR 중복 영향 감소 | M&A/파트너 VPC 단서. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS PrivateLink]] | 특정 서비스 private 접근 | CIDR 중복 가능, provider/consumer 서비스 모델 | VPC 전체 양방향 통신 아님 |
| [[AWS Transit Gateway]] | 네트워크 전체 라우팅 허브 | 다수 VPC/온프레미스 라우팅 | CIDR 중복 해결 못함 |
| [[VPC Peering]] | 두 VPC 전체 private 라우팅 | 단순 1:1 전체 통신 | CIDR 중복/전이 라우팅 불가 |
| Gateway VPC Endpoint | S3/DynamoDB route table endpoint | S3/DynamoDB private access | PrivateLink 기반 interface endpoint와 다름 |


## 4. SAP-C02 시나리오 패턴

### 패턴 1: SaaS 서비스를 고객 VPC에 private 제공

- **요구사항**: 소비자는 public internet 없이 서비스에 접근하고 VPC CIDR은 겹칠 수 있음
- **정답 단서**: provider/consumer, overlapping CIDR, private service access
- **선택할 구성**: PrivateLink endpoint service + interface endpoint
- **오답 함정**: TGW/Peering은 CIDR 중복과 전체 네트워크 연결 문제가 있다.

### 패턴 2: AWS API private 접근

- **요구사항**: private subnet에서 AWS service API를 인터넷 없이 호출
- **정답 단서**: interface endpoint, no NAT, private access
- **선택할 구성**: Interface VPC Endpoint
- **오답 함정**: NAT Gateway는 public endpoint로 나가는 경로라 private-only 요구와 다를 수 있다.

## 5. 헷갈리는 포인트

> [!warning] 주의
> 네트워크 문제는 서비스 이름보다 **연결 범위, 라우팅 전파, CIDR 중복, 암호화, 지연시간, 장애 도메인** 단서를 먼저 봐야 한다.

- PrivateLink는 특정 서비스 접근이지 VPC 간 라우팅이 아니다.
- S3/DynamoDB gateway endpoint는 PrivateLink 기반 interface endpoint와 다르다.
- 제공자 쪽은 보통 NLB/GWLB 뒤 endpoint service를 사용한다.

## 6. 암기 문장

- CIDR이 겹쳐도 특정 서비스만 private하게 제공하면 PrivateLink다.
- 전체 네트워크 연결은 TGW/Peering, S3/DynamoDB route endpoint는 gateway endpoint와 구분한다.

## 참고 링크

- [What is AWS PrivateLink?](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html)
- [AWS PrivateLink concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html)
- [Access AWS services through AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
