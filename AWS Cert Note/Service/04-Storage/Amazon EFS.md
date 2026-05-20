---
type: aws-service
service_name: "Amazon EFS"
category: "Storage"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["EFS", "Elastic File System"]
tags: [aws, sap-c02, storage, file-storage, nfs]
created: 2026-05-20
updated: 2026-05-20
---

# Amazon EFS

> [!summary] 한 줄 요약
> 여러 compute가 동시에 mount하는 Linux/NFS 기반 서버리스 공유 파일 시스템이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 공유 파일, 서버리스/컨테이너/EC2 통합, Multi-AZ 가용성, 비용 계층화 |
| 핵심 의사결정 | 여러 Linux 클라이언트가 같은 파일을 동시에 읽고 써야 하면 EFS |
| 대표 키워드 | NFS, shared file system, Lambda mount, ECS/EKS shared storage, Access Point |
| 자주 비교되는 서비스 | [[Amazon EBS]], [[Amazon FSx]], [[Amazon S3]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: NFSv4 기반 탄력적 파일 스토리지. EC2, ECS, EKS, Lambda에서 mount 가능하다.
- **왜 쓰는가?**: 여러 인스턴스/AZ에서 같은 파일 세트를 공유하고 자동 확장 파일 시스템이 필요할 때 사용한다.
- **관리형 여부**: 서버리스 관리형. 파일 시스템 용량은 자동 증가/감소한다.
- **리전/글로벌**: Regional file system은 여러 AZ mount target을 통해 고가용성을 제공한다. One Zone은 비용 절감 대신 단일 AZ다.
- **핵심 제약**: Windows SMB 공유는 FSx for Windows가 자연스럽다. 초고성능 HPC는 FSx for Lustre가 더 적합할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Mount Target | 각 AZ 서브넷에 ENI 형태로 배치 | 클라이언트와 같은 AZ mount target 권장 |
| Access Point | 애플리케이션별 root path/UID/GID 강제 | 컨테이너/Lambda 멀티테넌시 권한 분리 |
| Regional vs One Zone | Multi-AZ 내구성/가용성 vs 저비용 단일 AZ | 중요 데이터는 Regional, 재생성 가능하면 One Zone 검토 |
| Storage Class | Standard, IA, Archive 계층 | lifecycle로 파일 접근 패턴 비용 최적화 |
| Throughput Mode | Elastic, Provisioned, Bursting | 예측 어려우면 Elastic, 보장 필요하면 Provisioned |
| Backup/Replication | AWS Backup, EFS Replication | DR/RPO와 리전 복구 요구사항 |
| Security | SG, IAM authorization, POSIX permission, TLS | 네트워크·IAM·파일 권한을 함께 확인 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EFS]] | Linux NFS 공유 파일 시스템 | 다수 EC2/ECS/EKS/Lambda가 공유 파일 접근 | Windows SMB/AD 요구를 무시하면 오답 |
| [[Amazon EBS]] | 단일 AZ 블록 스토리지 | 단일 EC2 DB/OS disk 고성능 | 다중 AZ 동시 공유 요구에는 부적합 |
| [[Amazon FSx]] | 특정 파일 시스템 엔진 관리형 | Windows SMB, Lustre HPC, NetApp ONTAP, OpenZFS | Linux 범용 NFS 공유는 EFS가 단순 |
| [[Amazon S3]] | 객체 스토리지 | 데이터 레이크/정적 객체/API 접근 | POSIX rename/lock/file semantics가 필요하면 부적합 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/amazon-efs-architecture.png]]

1. 각 AZ의 private subnet에 EFS mount target을 둔다.
2. EC2/ECS/EKS/Lambda는 보안 그룹과 NFS/TLS 조건을 만족해야 mount한다.
3. Lifecycle policy가 오래 접근하지 않은 파일을 IA/Archive로 이동한다.
4. AWS Backup 또는 EFS Replication으로 복구 전략을 구성한다.

## 5. 설계 시 고려사항

- **네트워크**: mount target 보안 그룹에서 NFS 2049를 허용해야 한다.
- **성능**: General Purpose는 낮은 지연 기본값, Max I/O는 대규모 병렬 처리용이지만 지연이 증가할 수 있다.
- **비용**: IA/Archive는 저장 비용을 낮추지만 접근 비용/지연 특성을 확인한다.
- **DR**: Regional 자체는 Multi-AZ지만 리전 재해 대비는 EFS Replication 또는 AWS Backup cross-Region 전략이 필요하다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> EFS는 “공유 디스크”가 아니라 NFS 파일 시스템이다. 블록 레벨 DB 성능을 기대하면 EBS/io2가 더 맞을 수 있다.

- One Zone EFS는 Regional EFS와 가용성 특성이 다르다.
- EFS는 Windows SMB 공유의 정답이 아니다. Windows/AD 네이티브 요구는 FSx for Windows를 검토한다.
- 보안은 IAM만으로 끝나지 않고 보안 그룹, POSIX permission, Access Point가 함께 작동한다.

## 7. 암기 문장

- Linux 기반 여러 compute가 동시에 파일을 공유하면 EFS다.
- Windows SMB는 FSx for Windows, HPC/S3 dataset 고속 처리는 FSx for Lustre와 비교한다.

## 참고 링크

- [Amazon EFS User Guide](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)
- [Amazon EFS performance specifications](https://docs.aws.amazon.com/efs/latest/ug/throughput-modes.html)
- [Managing storage lifecycle](https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
