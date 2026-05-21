---
type: aws-service
service_name: "Amazon FSx"
category: "Storage"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["FSx", "Amazon FSx for Windows", "Amazon FSx for Lustre", "FSx for ONTAP", "FSx for OpenZFS"]
tags: [aws, sap-c02, storage, file-storage, windows, hpc]
created: 2026-05-20
updated: 2026-05-20
---

# Amazon FSx

> [!summary] 한 줄 요약
> Windows SMB, Lustre HPC, NetApp ONTAP, OpenZFS처럼 특정 파일 시스템 엔진이 필요할 때 선택하는 관리형 파일 스토리지 패밀리다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 엔터프라이즈 파일 공유, Windows/AD, HPC/ML, 온프레미스 파일 시스템 마이그레이션 |
| 핵심 의사결정 | “어떤 파일 시스템 프로토콜/엔진이 필요한가?”로 FSx 종류를 고른다 |
| 대표 키워드 | SMB, Windows File Server, Active Directory, Lustre, S3 dataset, ONTAP, OpenZFS |
| 자주 비교되는 서비스 | [[Amazon EFS]], [[Amazon EBS]], [[Amazon S3]], [[AWS Storage Gateway]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: AWS가 운영하는 여러 파일 시스템 엔진의 관리형 서비스 묶음.
- **왜 쓰는가?**: 기존 애플리케이션이 특정 파일 프로토콜/기능을 요구하거나, EFS보다 특화된 성능/Windows/NetApp 기능이 필요할 때 사용한다.
- **관리형 여부**: 파일 서버/스토리지 인프라는 AWS가 관리. AD, 네트워크, 백업, 성능 모드는 설계해야 한다.
- **리전/글로벌**: 파일 시스템은 VPC/서브넷에 배치되는 리전 서비스. 엔진별 Multi-AZ/Single-AZ 옵션이 다르다.
- **핵심 제약**: FSx는 단일 제품이 아니라 엔진별 정답이 다르다. 시험에서는 키워드가 엔진을 거의 지정한다.

## 2. FSx 종류와 시험 포인트

| FSx 종류 | 핵심 용도 | 선택 단서 | 오답 함정 |
|---|---|---|---|
| FSx for Windows File Server | SMB, Windows ACL, AD 통합 | Windows 애플리케이션, 홈 디렉터리, SMB share | Linux NFS 범용 공유면 EFS가 단순 |
| FSx for Lustre | HPC/ML/EDA, 초고성능 POSIX, S3 연동 | S3 데이터셋을 고속 병렬 처리 | 일반 영구 파일 공유/Windows SMB 요구에는 부적합 |
| FSx for NetApp ONTAP | NFS/SMB/iSCSI, SnapMirror, NetApp 기능 | 온프레미스 NetApp 마이그레이션/하이브리드 | 단순 AWS 네이티브 공유에는 과할 수 있음 |
| FSx for OpenZFS | OpenZFS 기능, NFS, snapshot/clone | ZFS 기반 앱 lift-and-shift | Windows SMB/AD 요구와 혼동 금지 |

## 3. 비교 / 선택 기준

| 요구사항 | 정답 후보 | 이유 |
|---|---|---|
| Windows 서버 앱이 SMB와 AD 권한 필요 | FSx for Windows File Server | 네이티브 Windows 파일 서버 기능 |
| S3에 있는 대규모 데이터셋을 HPC로 처리 | FSx for Lustre | S3 data repository와 고성능 POSIX 파일 시스템 |
| 기존 NetApp ONTAP 기능/복제 유지 | FSx for NetApp ONTAP | SnapMirror/ONTAP 호환성 |
| 여러 Linux 워크로드의 단순 NFS 공유 | [[Amazon EFS]] | 서버리스 범용 NFS가 더 단순 |
| EC2 단일 인스턴스 블록 볼륨 | [[Amazon EBS]] | 파일 서버가 아니라 block storage |

## 4. 아키텍처 / 선택 맵

![[attachments/aws/amazon-fsx-comparison.png]]

1. 프로토콜이 Windows SMB/AD면 FSx for Windows를 선택한다.
2. 고성능 병렬 처리와 S3 dataset 연동이면 FSx for Lustre를 선택한다.
3. NetApp 또는 OpenZFS 호환성이 지문에 있으면 해당 FSx 엔진을 선택한다.
4. 별도 엔진 요구가 없고 Linux 공유 파일만 필요하면 EFS와 비교한다.

## 5. 설계 시 고려사항

- **AD 통합**: FSx for Windows는 AWS Managed Microsoft AD 또는 self-managed AD 연동 요구가 자주 나온다.
- **S3 연동**: FSx for Lustre는 S3 data repository와 import/export 흐름이 핵심이다.
- **가용성**: 엔진별 Multi-AZ/Single-AZ 옵션과 백업/복제 지원 차이를 확인한다.
- **네트워크**: VPC 내부 파일 시스템이므로 라우팅, SG, DNS, 온프레미스 연결(DX/VPN)이 중요하다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> “파일 공유”라는 말만 보고 EFS를 고르면 안 된다. Windows SMB/AD, Lustre/HPC, NetApp 같은 키워드는 FSx로 간다.

- FSx for Lustre는 S3를 대체하는 장기 보관소가 아니라 고성능 처리 파일 시스템으로 보는 것이 자연스럽다.
- FSx for Windows는 Linux NFS 공유의 기본 정답이 아니다.
- ONTAP/OpenZFS는 기존 플랫폼 호환성이 강한 단서일 때 선택한다.

## 7. 암기 문장

- FSx는 “특정 파일 시스템 엔진이 문제에 박혀 있을 때” 고르는 서비스다.
- Windows/SMB/AD는 FSx for Windows, S3+HPC는 FSx for Lustre, 범용 Linux NFS는 EFS다.

## 참고 링크

- [Amazon FSx Documentation](https://docs.aws.amazon.com/fsx/)
- [FSx for Windows File Server User Guide](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)
- [Using data repositories with FSx for Lustre](https://docs.aws.amazon.com/fsx/latest/LustreGuide/fsx-data-repositories.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
