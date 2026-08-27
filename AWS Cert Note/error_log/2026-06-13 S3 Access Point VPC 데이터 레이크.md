---
type: aws-exam-error-log
exam: SAP-C02
created: 2026-06-13
updated: 2026-06-13
question_source: "미제공"
services: ["Amazon S3", "Amazon VPC"]
related_notes: ["[[Amazon S3]]", "[[Amazon VPC]]"]
tags: [aws, sap-c02, error-log, s3, vpc-endpoint, access-point, data-lake]
---

# S3 Access Point와 Gateway Endpoint로 데이터 레이크 private 접근

> [!summary] 오답 요약
> 여러 계정의 애플리케이션이 S3 데이터 레이크를 공용 인터넷 없이 최소 권한으로 접근하려면 **애플리케이션별 VPC-only S3 Access Point**와 **각 애플리케이션 VPC의 S3 Gateway Endpoint**를 함께 구성한다.

## 1. 문제 상황 요약

- **시나리오**: 한 기업이 여러 AWS 계정에 걸쳐 수백 개 애플리케이션이 접근하는 [[Amazon S3]] 데이터 레이크를 운영한다.
- **핵심 요구사항**: S3 버킷은 공용 인터넷을 통해 접근되면 안 되고, 각 애플리케이션은 필요한 최소 권한만 가져야 한다.
- **설계 방향**: 각 애플리케이션에 대해 특정 [[Amazon VPC]]로 제한된 S3 Access Point를 사용한다.
- **관련 서비스**: [[Amazon S3]], [[Amazon VPC]]

## 2. 정답과 오답

| 구분  | 선택지/서비스                                                                                                                              | 판단                                                                                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 정답  | c) 각 애플리케이션 VPC에 Amazon S3용 gateway endpoint를 생성하고 endpoint policy로 S3 access point 접근을 허용한 뒤 route table 지정                         | S3로 가는 트래픽을 인터넷/NAT가 아니라 VPC endpoint 경로로 보내고, endpoint policy로 access point/bucket 접근을 제한한다.                                                                         |
| 정답  | a) S3 버킷 소유 계정에서 각 애플리케이션용 S3 access point를 생성하고, 각 access point를 해당 애플리케이션 VPC로 제한하며, bucket policy가 access point 경유 접근을 요구하도록 업데이트 | 버킷 소유 계정이 데이터 레이크 접근 지점을 중앙 관리하면서 앱별 access point policy로 최소 권한을 분리하고, VPC-only origin으로 공용 인터넷 접근을 차단한다.                                                             |
| 오답  | d) 각 AWS 계정에서 각 애플리케이션 access point를 만들고 S3 버킷에 연결                                                                                   | cross-account access point는 가능한 패턴이지만, 이 문제의 구현 단계는 데이터 레이크 버킷을 소유한 계정에서 access point를 중앙 생성·통제하는 것이다. 각 애플리케이션 계정에 AP 생성을 분산하면 bucket owner 중심의 통제 요구와 시험 의도에서 벗어난다. |
| 오답  | b) S3용 interface endpoint 생성 + VPC gateway attachment 생성                                                                             | S3는 gateway endpoint가 기본 정답 패턴이다. `VPC gateway attachment`는 S3 endpoint 구성 단계가 아니며, 라우팅 테이블 연결이 핵심이다.                                                                 |
| 오답  | e) 데이터 레이크의 VPC에 S3 gateway endpoint 생성                                                                                              | S3 버킷은 VPC 안에 존재하지 않는다. endpoint는 S3에 접근하는 **애플리케이션 VPC**마다 만들어야 한다.                                                                                                  |

## 3. 왜 정답인가

- S3 Access Point는 버킷에 연결된 이름 있는 네트워크 엔드포인트이며, access point마다 별도 policy와 network control을 적용할 수 있다.
- VPC-only access point는 생성 시 특정 VPC를 지정하고, 그 VPC가 아닌 곳에서 온 요청을 S3가 거부한다. 이 설정은 생성 후 바꿀 수 없다.
- VPC-only access point를 실제로 사용하려면 애플리케이션 VPC에서 S3로 나가는 VPC endpoint가 필요하다. endpoint policy는 access point ARN과 underlying bucket ARN 접근을 모두 허용해야 한다.
- 여러 AWS 계정의 애플리케이션이 하나의 데이터 레이크 버킷을 사용할 때도 이 문제에서는 버킷 소유 계정에서 애플리케이션별 access point를 만들어 중앙 통제하고, 애플리케이션 IAM과 access point policy로 필요한 권한만 허용한다.
- S3 Gateway Endpoint는 route table에 S3 prefix list 경로를 추가해 VPC 내부 리소스가 인터넷 게이트웨이나 NAT 없이 S3에 접근하게 한다.

## 4. 다시 풀 때의 판단 규칙

- **키워드**: `S3 data lake`, `many applications`, `multiple AWS accounts`, `least privilege`, `specific VPC`, `must not access over public internet`
- **바로 떠올릴 구성**: 버킷 소유 계정의 [[Amazon S3]] Access Point per application + VPC-only network origin + [[Amazon VPC]] S3 Gateway Endpoint per application VPC + endpoint policy + route table
- **버릴 선택지**:
  - `interface endpoint`가 단독으로 나오면 먼저 S3 Gateway Endpoint와 비교한다.
  - `데이터 레이크의 VPC`라는 표현은 S3가 VPC 리소스가 아니므로 의심한다.
  - 각 애플리케이션 계정마다 access point를 만들라는 선택지는 cross-account AP 가능성과 문제의 중앙 통제 요구를 혼동한 함정이다.
- **암기 문장**: S3 데이터 레이크를 여러 계정 앱에 최소 권한으로 열 때는 버킷 소유 계정의 access point로 권한을 쪼개고, public internet 차단은 VPC-only AP와 애플리케이션 VPC의 S3 gateway endpoint로 완성한다.

## 5. 서비스 노트 보강 여부

- [x] 관련 서비스 노트가 존재한다: [[Amazon S3]], [[Amazon VPC]]
- [x] 정답 개념이 서비스 노트에 있다: 버킷 소유 계정의 S3 Access Point, VPC-only access point, S3 Gateway Endpoint policy 보강
- [x] 오답 비교/함정이 서비스 노트에 있다: interface endpoint/gateway attachment, 데이터 레이크 VPC 함정 보강
- [x] 필요 시 서비스 노트를 업데이트했다: `Service/04-Storage/Amazon S3.md`, `Service/01-Network/1-1 Amazon VPC.md`

## 6. 참고 링크

- [Managing access to shared datasets with S3 access points](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points.html)
- [Creating access points restricted to a VPC](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points-vpc.html)
- [Configuring IAM policies for using access points](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points-policies.html)
- [Gateway endpoints for Amazon S3](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html)

## 7. 복습 질문

- S3 access point policy만 허용하면 충분한가, underlying bucket policy도 허용해야 하는가?
- VPC-only access point를 쓸 때 endpoint는 S3 버킷 쪽에 만드는가, 애플리케이션 VPC 쪽에 만드는가?
- S3 private access 기본 패턴에서 gateway endpoint와 interface endpoint를 언제 구분해야 하는가?
