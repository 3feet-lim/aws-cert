---
type: aws-service
service_name: "AWS Storage Gateway"
category: "Storage"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Storage Gateway", "S3 File Gateway", "FSx File Gateway", "Volume Gateway", "Tape Gateway"]
tags: [aws, sap-c02, storage, hybrid, migration]
created: 2026-05-20
updated: 2026-05-20
---

# AWS Storage Gateway

> [!summary] 한 줄 요약
> 온프레미스 애플리케이션이 표준 파일/블록/테이프 인터페이스로 AWS 스토리지를 사용하게 하는 하이브리드 스토리지 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 하이브리드 클라우드, 백업/아카이브, 온프레미스 앱과 S3/FSx 연동, 마이그레이션 |
| 핵심 의사결정 | 온프레미스는 기존 프로토콜을 유지하고 데이터는 AWS에 저장/백업해야 하면 Storage Gateway |
| 대표 키워드 | on-premises, NFS/SMB, iSCSI, virtual tape library, cache, hybrid storage |
| 자주 비교되는 서비스 | [[Amazon S3]], [[Amazon FSx]], [[AWS Backup]], [[AWS Elastic Disaster Recovery]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 온프레미스 또는 EC2에 배포하는 gateway appliance와 AWS 스토리지를 연결하는 서비스.
- **왜 쓰는가?**: 기존 앱은 NFS/SMB/iSCSI/VTL을 계속 사용하고, 데이터 저장/아카이브/백업은 AWS로 확장한다.
- **관리형 여부**: 클라우드 서비스와 appliance 소프트웨어는 AWS가 제공하지만 로컬 VM/캐시/네트워크는 운영 설계가 필요하다.
- **리전/글로벌**: gateway는 활성화한 리전의 AWS 스토리지와 연결한다.
- **핵심 제약**: 애플리케이션 서버 DR 전체를 자동 복구하는 서비스가 아니다. 서버 DR은 AWS DRS와 비교한다.

## 2. Gateway 유형과 시험 포인트

| 유형 | 인터페이스 | AWS 저장소 | 선택 단서 |
|---|---|---|---|
| S3 File Gateway | NFS/SMB | Amazon S3 객체 | 온프레미스 파일을 S3 객체로 저장, 데이터 레이크 ingest |
| FSx File Gateway | SMB | FSx for Windows File Server | 온프레미스에서 AWS Windows 파일 공유 접근 |
| Volume Gateway - Cached | iSCSI block | 주 데이터 S3, 자주 쓰는 데이터 로컬 cache | 온프레미스 block storage 확장, 클라우드 백업 |
| Volume Gateway - Stored | iSCSI block | 주 데이터 로컬, snapshot AWS | 로컬 저지연 + AWS 백업 |
| Tape Gateway | VTL/iSCSI | S3 + Glacier 계열 | 기존 tape backup software 유지, 물리 테이프 대체 |

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 온프레미스 NFS/SMB 파일을 S3에 저장 | S3 File Gateway | S3 API 직접 변경과 파일 gateway 캐시 일관성 고려 |
| 온프레미스 Windows SMB share를 AWS FSx로 | FSx File Gateway | 단순 S3 객체 저장이면 S3 File Gateway |
| 온프레미스 앱이 iSCSI block 필요 | Volume Gateway | EC2 전용 block storage인 EBS와 혼동 금지 |
| 테이프 백업 소프트웨어 유지 | Tape Gateway | S3 Glacier만으로 VTL 인터페이스 제공 안 함 |
| 서버 전체 DR | AWS DRS | Storage Gateway는 스토리지 통합 서비스 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-storage-gateway-architecture.png]]

1. 온프레미스 앱은 기존 NFS/SMB/iSCSI/VTL 프로토콜로 gateway에 연결한다.
2. Gateway는 로컬 cache/upload buffer를 사용해 지연을 줄이고 AWS로 비동기 전송한다.
3. 목적지에 따라 S3, FSx, EBS snapshot, Glacier 계열에 저장된다.
4. CloudWatch/CloudTrail로 gateway 상태, 캐시, 업로드 오류를 모니터링한다.

## 5. 설계 시 고려사항

- **네트워크**: 안정적인 대역폭, 프록시/방화벽, Direct Connect/VPN, VPC endpoint를 고려한다.
- **캐시 용량**: working set이 cache에 맞지 않으면 지연과 egress가 증가한다.
- **백업 통합**: Volume Gateway 볼륨은 AWS Backup/EBS snapshot과 연결된다.
- **테이프 아카이브**: Tape Gateway는 VTL을 제공하고 archive는 S3 Glacier Flexible Retrieval 또는 Deep Archive를 사용한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Storage Gateway는 “온프레미스 프로토콜 호환성”이 핵심 단서다. AWS 네이티브 앱이면 S3/EFS/FSx를 직접 쓰는 편이 단순하다.

- File Gateway는 객체 스토리지를 파일 인터페이스로 보여주는 하이브리드 패턴이다.
- Volume Gateway는 iSCSI block 인터페이스이며 EC2에 붙는 EBS와 역할이 다르다.
- Tape Gateway는 물리 테이프 인프라를 줄이기 위한 VTL 패턴이다.

## 7. 암기 문장

- 온프레미스 앱은 그대로 두고 AWS 스토리지를 파일/볼륨/테이프로 붙이면 Storage Gateway다.
- 서버 복구는 DRS, 중앙 백업 정책은 AWS Backup, AWS 네이티브 파일 공유는 EFS/FSx와 구분한다.

## 참고 링크

- [AWS Storage Gateway Documentation](https://docs.aws.amazon.com/storagegateway/)
- [What is Tape Gateway?](https://docs.aws.amazon.com/storagegateway/latest/tgw/WhatIsStorageGateway.html)
- [How Volume Gateway works](https://docs.aws.amazon.com/storagegateway/latest/vgw/StorageGatewayConcepts.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
