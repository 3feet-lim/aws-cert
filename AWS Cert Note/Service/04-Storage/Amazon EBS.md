---
type: aws-service
service_name: "Amazon EBS"
category: "Storage"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["EBS", "Elastic Block Store"]
tags: [aws, sap-c02, storage, block-storage, ec2]
created: 2026-05-20
updated: 2026-05-20
---

# Amazon EBS

> [!summary] 한 줄 요약
> EC2 인스턴스에 연결하는 AZ 단위 블록 스토리지로, 데이터베이스·부트 볼륨·저지연 랜덤 I/O에 사용한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | EC2 기반 워크로드, 성능 튜닝, 스냅샷/DR, 암호화 |
| 핵심 의사결정 | 인스턴스에 attach되는 block device가 필요하면 EBS |
| 대표 키워드 | block storage, EC2 volume, gp3/io2, snapshot, Multi-Attach, AZ |
| 자주 비교되는 서비스 | [[Amazon S3]], [[Amazon EFS]], [[Amazon FSx]], Instance Store |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: EC2에 연결하는 영구 블록 스토리지. OS에서는 디스크처럼 보인다.
- **왜 쓰는가?**: 부트 볼륨, 데이터베이스, 파일 시스템 구성, 낮은 지연의 블록 I/O가 필요할 때 사용한다.
- **관리형 여부**: AWS가 물리 저장소를 관리하지만 파일 시스템, 백업 주기, 암호화 정책은 사용자가 설계한다.
- **리전/글로벌**: 볼륨은 특정 AZ에 존재하며 같은 AZ의 인스턴스에 연결한다. Snapshot은 리전 단위로 관리되고 복사 가능하다.
- **핵심 제약**: 기본적으로 단일 인스턴스 attach. Multi-Attach는 제한된 io1/io2 용도이며 클러스터 파일 시스템이 필요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| gp3/gp2 | 범용 SSD. gp3는 크기와 별개로 IOPS/throughput 조정 | 일반 워크로드 기본 선택 |
| io2/io1 | Provisioned IOPS SSD | 고성능 DB, 지연시간/IOPS 보장 |
| st1/sc1 | 처리량 최적화/Cold HDD | 순차 처리 대용량, 부트 볼륨 불가 |
| Snapshot | S3에 저장되는 증분 point-in-time 백업 | 백업/복제/AMI/DR 핵심 |
| Fast Snapshot Restore | snapshot으로 만든 볼륨 초기 지연 감소 | 대규모 빠른 복구 요구 |
| Encryption | KMS 기반, volume/snapshot/복원 volume에 전파 | 규정 준수, cross-account 공유 시 KMS 권한 |
| Elastic Volumes | 실행 중 크기/성능/타입 변경 | 다운타임 최소화 성능 개선 |
| Multi-Attach | 지원 볼륨을 같은 AZ 여러 인스턴스에 attach | 일반 공유 파일 시스템 대체가 아님 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon EBS]] | EC2에 attach하는 block storage | DB, OS disk, 낮은 지연 랜덤 I/O | 여러 AZ에서 동시에 공유하려고 선택하면 오답 |
| [[Amazon EFS]] | NFS 공유 파일 시스템 | 여러 EC2/Lambda/ECS가 파일을 공유 | 단일 DB 디스크 성능 목적이면 부적합 |
| [[Amazon S3]] | 객체 스토리지 | 데이터 레이크, 정적 파일, 백업 저장 | POSIX 파일/블록 수정 워크로드에 부적합 |
| Instance Store | 호스트 로컬 임시 디스크 | 임시 캐시, 초저지연 임시 데이터 | 인스턴스 중지/종료 시 데이터 지속성 기대하면 오답 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/amazon-ebs-flow.png]]

1. 같은 AZ의 EC2 인스턴스에 EBS 볼륨을 attach한다.
2. Snapshot은 point-in-time으로 생성되고 증분 방식으로 저장된다.
3. Snapshot copy로 다른 리전/계정 DR을 구성한다.
4. 복구 시 snapshot에서 새 볼륨을 만들고 대상 AZ의 EC2에 attach한다.

## 5. 가용성 / 확장성 / 복원력

- EBS 볼륨은 AZ 리소스이므로 AZ 장애에 대비하려면 snapshot, AMI, Multi-AZ 애플리케이션 아키텍처가 필요하다.
- Snapshot은 애플리케이션 캐시를 자동 flush하지 않는다. 일관성이 중요하면 정지, flush, filesystem freeze, application-aware backup을 고려한다.
- AWS Backup 또는 Data Lifecycle Manager로 snapshot 스케줄과 retention을 자동화한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> EBS Snapshot은 S3에 저장되지만 사용자가 S3 버킷에서 직접 접근하는 객체가 아니다.

- EBS 볼륨은 같은 AZ 인스턴스에 붙인다. 리전 간 이동은 snapshot copy 후 새 볼륨 생성으로 한다.
- Multi-Attach는 공유 파일 시스템 기능을 제공하지 않는다. 동시 쓰기 정합성은 클러스터 파일 시스템/애플리케이션 책임이다.
- 암호화된 snapshot/volume은 암호화를 제거할 수 없다. 다른 KMS 키를 쓰려면 snapshot copy에서 재암호화한다.

## 7. 암기 문장

- EC2에 디스크처럼 붙고 낮은 지연 블록 I/O가 필요하면 EBS다.
- AZ 경계를 넘는 EBS 고가용성은 volume 자체가 아니라 snapshot/복제/애플리케이션 아키텍처로 해결한다.

## 참고 링크

- [Amazon EBS volumes](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volumes.html)
- [Amazon EBS snapshots](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-snapshots.html)
- [Amazon EBS encryption](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-encryption.html)
- [EBS Multi-Attach](https://docs.aws.amazon.com/ebs/latest/userguide/working-with-multi-attach.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
