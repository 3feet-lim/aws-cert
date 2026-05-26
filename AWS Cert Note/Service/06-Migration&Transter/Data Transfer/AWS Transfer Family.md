---
type: aws-service
service_name: "AWS Transfer Family"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["Transfer Family", "AWS SFTP", "SFTP on AWS", "AS2"]
tags: [aws, sap-c02, migration, data-transfer, sftp]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Transfer Family

> [!summary] 한 줄 요약
> SFTP, FTPS, FTP, AS2 같은 기존 파일 전송 프로토콜을 유지하면서 백엔드는 Amazon S3 또는 Amazon EFS로 사용하는 완전관리형 파일 전송 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | B2B 파일 교환, 레거시 SFTP/FTP 유지, 파트너 통합, S3/EFS 기반 수신 |
| 핵심 의사결정 | 고객/파트너 클라이언트와 프로토콜 설정을 바꾸지 않고 AWS storage로 파일을 주고받아야 하면 Transfer Family |
| 대표 키워드 | SFTP, FTPS, FTP, AS2, managed endpoint, partner file exchange, S3 backend, EFS backend |
| 자주 비교되는 서비스 | [[AWS DataSync]], [[AWS Storage Gateway]], [[Amazon S3]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 파일 전송 프로토콜 서버를 직접 운영하지 않고 AWS managed endpoint로 제공하는 서비스.
- **왜 쓰는가?**: 파트너·고객·내부 시스템의 SFTP/FTPS/FTP/AS2 클라이언트 설정을 유지하면서 데이터를 S3/EFS에 저장한다.
- **관리형 여부**: 서버 인프라, 확장, 패치 운영을 AWS가 관리한다.
- **리전/글로벌**: 리전 서비스이며 endpoint 유형, VPC 접근, custom hostname, identity provider를 설계한다.
- **핵심 제약**: 대량 마이그레이션 복사 엔진이 아니라 프로토콜 endpoint다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Protocol support | SFTP, FTPS, FTP, AS2, web app | 기존 B2B 파일 교환 유지 |
| Storage backend | Amazon S3 또는 Amazon EFS | 객체/파일 기반 후속 처리 선택 |
| Identity provider | Service managed, AD/LDAP/custom, IAM 등 | 기존 사용자 인증 통합 |
| Endpoint type | Public 또는 VPC-hosted endpoint | 보안/네트워크 접근 제어 |
| Workflows | 업로드 후 처리 자동화 | 파일 수신 후 Lambda/검사/이동 패턴 |
| Logging | CloudWatch logs | 감사와 운영 모니터링 |

## 3. 선택 맵

![[attachments/aws/aws-data-transfer-selection-map.png]]

1. 외부 파트너나 레거시 앱이 SFTP/FTPS/FTP/AS2로 접속한다.
2. Transfer Family endpoint가 인증·권한을 처리하고 파일을 S3 또는 EFS에 저장한다.
3. 저장된 파일은 Lambda, Step Functions, Glue, S3 event 등으로 후속 처리한다.
4. CloudWatch/CloudTrail/S3 logging으로 감사와 모니터링을 구성한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 파트너가 SFTP 계정으로 파일 업로드 | Transfer Family | DataSync는 SFTP server endpoint가 아님 |
| NFS/SMB 파일 서버에서 S3/EFS로 대량 복사 | DataSync | Transfer Family는 복사 작업 자동화 목적이 아님 |
| 온프레미스 앱이 NFS/SMB/iSCSI 인터페이스 필요 | Storage Gateway | Transfer Family는 파일 전송 프로토콜 endpoint |
| 애플리케이션이 S3 API 직접 사용 가능 | Amazon S3 | SFTP 호환 요구 없으면 Transfer Family 불필요 |

## 5. 설계 시 고려사항

- **인증/권한**: 사용자별 home directory, IAM role, logical directory mapping, custom IdP를 설계한다.
- **네트워크**: public endpoint, VPC endpoint, security group, allow list, custom hostname을 검토한다.
- **보안**: SFTP/FTPS/AS2 요구, 암호화, partner key/certificate 관리, CloudWatch logging을 구성한다.
- **운영 자동화**: 업로드 후 malware scan, format validation, S3 prefix 이동, 알림 workflow를 붙인다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Transfer Family는 “프로토콜 호환 endpoint”가 핵심이다. “대량 데이터를 빠르게 복사”가 핵심이면 DataSync/Snow가 더 자주 정답이다.

- FTP는 암호화가 없으므로 보안 요구가 있으면 SFTP/FTPS/AS2를 검토한다.
- S3 backend를 쓰면 객체 이벤트 기반 처리와 lifecycle/archive를 쉽게 붙일 수 있다.
- EFS backend는 파일 시스템 semantics가 필요한 워크로드에 더 자연스럽다.

## 7. 암기 문장

- SFTP/FTPS/FTP/AS2를 유지하고 저장소만 S3/EFS로 바꾸면 Transfer Family다.
- DataSync는 복사 작업, Transfer Family는 사용자/파트너가 접속하는 managed endpoint다.

## 참고 링크

- [What is AWS Transfer Family?](https://docs.aws.amazon.com/transfer/latest/userguide/what-is-aws-transfer-family.html)
- [Transferring files over a server endpoint using a client](https://docs.aws.amazon.com/transfer/latest/userguide/transfer-file.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
