---
type: aws-service
service_name: "AWS Snow Family"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Snowball Edge", "AWS Snowball", "AWS Snowcone", "Snow Family"]
tags: [aws, sap-c02, migration, data-transfer, edge]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Snow Family

> [!summary] 한 줄 요약
> 네트워크 전송이 현실적이지 않은 대용량 데이터를 AWS 소유 물리 장비로 운송하거나 엣지에서 로컬 스토리지/컴퓨팅을 수행하는 서비스 제품군이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 오프라인 대용량 데이터 이전, 제한된 네트워크, 엣지/단절 환경, 로컬 처리 |
| 핵심 의사결정 | 수백 TB~PB 데이터를 인터넷/DX로 옮기기 어렵거나 엣지에서 로컬 처리가 필요하면 Snow Family |
| 대표 키워드 | physical device, offline transfer, Snowball Edge, rugged device, edge compute, S3 import/export |
| 자주 비교되는 서비스 | [[AWS DataSync]], [[AWS Storage Gateway]], [[AWS Transfer Family]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS가 제공하는 보안 물리 장비를 고객 위치로 배송해 데이터를 적재/처리한 뒤 AWS로 반입하거나 반출하는 서비스.
- **왜 쓰는가?**: 네트워크 대역폭·시간·비용 제약 때문에 온라인 전송이 비현실적인 대량 데이터를 이동한다.
- **관리형 여부**: 장비 주문/추적/보안 체인은 AWS가 제공하지만 현장 연결, 복사, 검증, 반송은 운영 절차가 필요하다.
- **리전/글로벌**: Snow job을 지원 리전에서 생성하고, 데이터는 주로 Amazon S3로 import/export한다.
- **핵심 제약**: 반복적 온라인 동기화나 실시간 복제 서비스가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Snowball Edge | 대용량 스토리지와 일부 컴퓨팅 지원 | 데이터센터 마이그레이션, 엣지 처리 |
| Physical shipping | 장비를 배송해 데이터를 운송 | 네트워크 부족/대량 일회성 이전 |
| Encryption | KMS 기반 암호화, 장비 보안 | 데이터 물리 운송 보안 |
| Local compute/storage | 현장 로컬 처리와 S3 호환 스토리지 | 단절/저연결 엣지 워크로드 |
| Job workflow | 주문→수령→잠금 해제→복사→반송→S3 적재 | 운영 절차 이해 |

## 3. 선택 맵

![[attachments/aws/aws-data-transfer-selection-map.png]]

1. 전송 데이터량과 사용 가능한 네트워크 대역폭으로 전송 시간을 계산한다.
2. 온라인 전송이 비현실적이면 Snowball Edge 장비를 주문한다.
3. 현장에서 데이터를 장비에 복사하고 검증한 뒤 AWS로 반송한다.
4. AWS가 데이터를 대상 S3 버킷으로 가져오고 장비 데이터를 안전하게 삭제한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 수백 TB~PB, 네트워크 부족 | Snow Family | DataSync는 네트워크 기반이라 시간이 과도할 수 있음 |
| NFS/SMB 데이터를 반복적으로 온라인 동기화 | DataSync | Snow는 반복 동기화 기본 답이 아님 |
| 파트너 SFTP 업로드 endpoint | Transfer Family | Snow는 파일 전송 서버가 아님 |
| 온프레미스 앱이 AWS 스토리지를 계속 마운트 | Storage Gateway | Snow는 영구 게이트웨이 아님 |
| 엣지/단절 환경 로컬 처리 | Snowball Edge | 단순 클라우드 분석이면 AWS 네이티브 서비스 사용 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Snow Family의 시험 단서는 “대역폭이 부족해서 네트워크 전송이 오래 걸림” 또는 “단절/엣지 현장에서 로컬 처리 필요”다.

- Snowball Edge는 물리 배송과 로컬 compute/storage를 제공하지만, 일반적인 온라인 파일 동기화는 DataSync가 더 적합하다.
- 데이터베이스 최소 다운타임 이전은 DMS이고, 서버 rehost는 MGN이다.
- 장비 주문, 반송, 현장 보안, 데이터 검증 시간이 프로젝트 일정에 포함된다.

## 6. 암기 문장

- 네트워크보다 트럭이 빠른 대용량 이전은 Snow Family다.
- 반복 온라인 복사는 DataSync, 프로토콜 endpoint는 Transfer Family와 구분한다.

## 참고 링크

- [What is Snowball Edge?](https://docs.aws.amazon.com/snowball/latest/developer-guide/whatisedge.html)
- [How AWS Snowball Edge works](https://docs.aws.amazon.com/snowball/latest/developer-guide/how-it-works.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
