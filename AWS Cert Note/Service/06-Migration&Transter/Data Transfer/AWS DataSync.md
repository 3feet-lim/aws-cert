---
type: aws-service
service_name: "AWS DataSync"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["DataSync"]
tags: [aws, sap-c02, migration, data-transfer, storage]
created: 2026-05-26
updated: 2026-05-26
---

# AWS DataSync

> [!summary] 한 줄 요약
> 온프레미스, 다른 클라우드, AWS 스토리지 사이에서 파일/객체 데이터를 빠르고 안전하게 온라인 전송·동기화하는 관리형 데이터 이동 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 온라인 데이터 마이그레이션, 반복 복사, 검증, S3/EFS/FSx 이전 |
| 핵심 의사결정 | 네트워크로 전송 가능하고 NFS/SMB/HDFS/Object 데이터를 S3/EFS/FSx로 빠르게 복사해야 하면 DataSync |
| 대표 키워드 | online transfer, NFS, SMB, HDFS, object storage, scheduled task, data validation |
| 자주 비교되는 서비스 | [[AWS Snow Family]], [[AWS Transfer Family]], [[AWS Storage Gateway]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 파일/객체 데이터를 소스 location에서 대상 location으로 전송하는 관리형 데이터 이동 서비스.
- **왜 쓰는가?**: 수동 스크립트/rsync 운영 부담 없이 고속 전송, 스케줄링, 암호화, 무결성 검증을 사용한다.
- **관리형 여부**: AWS가 전송 작업을 관리하고, 온프레미스 소스에는 DataSync agent를 배포할 수 있다.
- **리전/글로벌**: 대상 AWS 스토리지 리전과 네트워크 경로를 고려한다.
- **핵심 제약**: SFTP/FTPS/FTP 서비스 엔드포인트가 아니며, 네트워크가 부족한 PB급 오프라인 이동은 Snow Family를 고려한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Location | NFS/SMB/HDFS/Object/S3/EFS/FSx 등 소스·타깃 | 지원 스토리지 확인 |
| Task | 전송 설정, 필터, 스케줄, 검증 | 반복 동기화/마이그레이션 자동화 |
| Agent | 온프레미스/다른 클라우드 접근용 VM | 하이브리드 전송 구성 |
| Data validation | 전송 후 무결성 검증 | 마이그레이션 신뢰성 |
| VPC endpoint 지원 | AWS 내부 경로로 접근 가능 | 보안/프라이빗 전송 요구 |

## 3. 선택 맵

![[attachments/aws/aws-data-transfer-selection-map.png]]

1. 온라인 전송이 가능하고 파일/객체 데이터를 빠르게 복사해야 하면 DataSync를 선택한다.
2. 네트워크가 부족하거나 수백 TB~PB를 물리적으로 가져와야 하면 Snow Family를 고려한다.
3. 파트너가 SFTP/FTPS/FTP/AS2 프로토콜로 계속 접속해야 하면 Transfer Family를 선택한다.
4. 온프레미스 앱이 기존 NFS/SMB/iSCSI/VTL 인터페이스를 계속 써야 하면 Storage Gateway가 맞다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS DataSync]] | 온라인 파일/객체 복사 작업 | NFS/SMB/HDFS/Object → S3/EFS/FSx | 프로토콜 서버가 아님 |
| [[AWS Snow Family]] | 물리 장비 배송, 오프라인/엣지 | 네트워크 부족, 대용량 일회성 이전 | 반복 온라인 동기화 기본 답 아님 |
| [[AWS Transfer Family]] | SFTP/FTPS/FTP/AS2 managed endpoint | 외부 파트너 파일 교환 유지 | 대량 마이그레이션 복사 엔진과 다름 |
| [[AWS Storage Gateway]] | 온프레미스 앱용 파일/볼륨/테이프 인터페이스 | 기존 앱 프로토콜 유지 | 단순 복사 작업이면 DataSync |

## 5. 헷갈리는 포인트

> [!warning] 주의
> DataSync는 “복사 작업” 서비스다. 사용자가 SFTP 서버처럼 접속해야 하는 요구사항은 Transfer Family가 더 직접적이다.

- DataSync는 데이터베이스 트랜잭션 복제 서비스가 아니다. DB 최소 다운타임 이전은 DMS를 본다.
- DataSync는 네트워크 기반이므로 대역폭, 변경률, 전송 창을 계산해야 한다.
- S3 replication은 S3 버킷 간 객체 복제 정책이고, DataSync는 다양한 파일/객체 소스 간 작업이다.

## 6. 암기 문장

- 온라인으로 파일/객체를 S3/EFS/FSx에 빠르게 옮기면 DataSync다.
- 오프라인 대용량은 Snow, 파일 전송 프로토콜 엔드포인트는 Transfer Family다.

## 참고 링크

- [What is AWS DataSync?](https://docs.aws.amazon.com/datasync/latest/userguide/what-is-datasync.html)
- [How AWS DataSync works](https://docs.aws.amazon.com/datasync/latest/userguide/how-datasync-works.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
