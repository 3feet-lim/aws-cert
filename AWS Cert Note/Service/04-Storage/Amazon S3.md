---
type: aws-service
service_name: "Amazon S3"
category: "Storage"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["S3", "Simple Storage Service"]
tags: [aws, sap-c02, storage, object-storage]
created: 2026-05-20
updated: 2026-05-20
---

# Amazon S3

> [!summary] 한 줄 요약
> 인터넷 규모의 객체 스토리지로, 정적 콘텐츠·데이터 레이크·백업·아카이브·이벤트 기반 통합의 기본 정답 후보이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 신규 설계, 비용 최적화, DR, 데이터 레이크, 보안/거버넌스 |
| 핵심 의사결정 | 객체 단위 저장, 높은 내구성, 수평 확장, lifecycle/replication/policy가 필요하면 S3 |
| 대표 키워드 | object storage, static website, data lake, lifecycle, CRR/SRR, Object Lock, presigned URL |
| 자주 비교되는 서비스 | [[Amazon EBS]], [[Amazon EFS]], [[Amazon S3 Glacier]], [[AWS Storage Gateway]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 버킷에 객체를 저장하는 관리형 객체 스토리지. 파일 시스템처럼 mount하는 서비스가 아니라 API/HTTP 기반 객체 저장소다.
- **왜 쓰는가?**: 내구성, 확장성, 비용 계층화, 이벤트 연동, cross-Region 복제를 한 서비스에서 해결한다.
- **관리형 여부**: 완전 관리형. 사용자는 버킷 정책, 암호화, lifecycle, replication, access logging 등을 설계한다.
- **리전/글로벌**: 버킷은 리전 리소스이며, 이름은 전역적으로 고유하다. CloudFront와 조합하면 글로벌 배포가 된다.
- **핵심 제약**: 블록 스토리지/공유 POSIX 파일 시스템이 아니다. Glacier 계열 아카이브 객체는 복원 후 접근해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Storage Class | Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier 계열, Express One Zone | 접근 패턴/복원 시간/최소 보관 기간/가용성 요구사항으로 선택 |
| Lifecycle | 객체를 시간·prefix·tag 기준으로 전환/만료 | 비용 최적화의 대표 단서 |
| Versioning | 삭제/덮어쓰기 복구를 위해 버전을 유지 | 실수 삭제 대응, replication/Object Lock 전제와 함께 출제 |
| Replication | 같은 리전(SRR) 또는 다른 리전(CRR)으로 객체 복제 | DR, 지연시간, 컴플라이언스, 계정 분리 요구사항 |
| Object Lock | WORM 보존, retention/legal hold | 규정 준수·랜섬웨어 방어. Versioning 필요 |
| Event Notification | S3 이벤트를 Lambda/SQS/SNS/EventBridge로 전달 | 업로드 후 처리 파이프라인 |
| Access Control | Block Public Access, bucket policy, IAM, access point, presigned URL | 퍼블릭 노출 방지와 임시 접근 제어 |
| Encryption | SSE-S3, SSE-KMS, DSSE-KMS, SSE-C, client-side | KMS 키 정책·cross-account 복제·감사 요구사항 |

## 3. 스토리지 클래스 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 자주 접근, 밀리초 지연 | S3 Standard | 비용만 보고 IA를 고르면 retrieval fee/최소 보관 기간 함정 |
| 접근 패턴 알 수 없음 | S3 Intelligent-Tiering | 작은 객체/모니터링 비용 고려 필요 |
| 드물게 접근하지만 즉시 필요 | S3 Standard-IA 또는 Glacier Instant Retrieval | Flexible Retrieval은 즉시 접근 불가 |
| 한 AZ 손실 허용, 재생성 가능 | S3 One Zone-IA 또는 S3 Express One Zone | 중요 데이터 DR에는 부적합 |
| 장기 보관, 분~시간 복원 가능 | S3 Glacier Flexible Retrieval | 앱이 즉시 읽어야 하면 오답 |
| 거의 접근하지 않는 장기 보관 | S3 Glacier Deep Archive | 복원 시간이 길고 최소 보관 기간이 길다 |
| 가장 낮은 지연의 객체 접근 | S3 Express One Zone | 단일 AZ 특성 때문에 Multi-AZ 내구성 요구와 충돌 가능 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/amazon-s3-architecture.png]]

1. 애플리케이션은 S3 API로 객체를 PUT/GET한다.
2. Lifecycle가 접근 패턴에 맞춰 IA/Glacier 계층으로 전환한다.
3. Replication은 DR·컴플라이언스·지연시간 요구에 따라 다른 버킷/리전/계정으로 복제한다.
4. Event Notification은 업로드 후 처리 파이프라인을 시작한다.

## 5. 보안 / 거버넌스

- 기본값은 **Block Public Access**를 유지하고, 필요한 공개는 CloudFront OAC/OAI 또는 제한된 bucket policy로 설계한다.
- cross-account 접근은 IAM만이 아니라 bucket policy, KMS key policy, object ownership까지 함께 확인한다.
- Object Lock은 WORM 요구사항의 핵심이며 versioning과 함께 설계한다.
- CloudTrail data events, S3 server access logs, Storage Lens, Macie를 감사/분석에 사용한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> S3는 EBS처럼 인스턴스에 붙이는 디스크가 아니고, EFS처럼 여러 인스턴스가 POSIX로 공유 mount하는 파일 시스템도 아니다.

- `S3 Glacier`는 별도 백업 서비스가 아니라 S3 storage class 계열로 이해한다.
- Versioning은 삭제 marker를 만들 수 있으므로 lifecycle로 noncurrent version 비용을 관리한다.
- CRR은 기존 객체까지 자동 소급 복제하는 기능이 아니라, 설정 이후 객체가 기본 대상이다.
- KMS 암호화 객체의 replication/cross-account 접근은 KMS 권한까지 맞아야 한다.

## 7. 암기 문장

- 객체·정적 콘텐츠·데이터 레이크·장기 보관·이벤트 처리는 우선 S3를 떠올린다.
- 즉시 공유 파일 시스템은 EFS/FSx, 블록 디스크는 EBS, 아카이브 복원 시간은 Glacier 계층으로 구분한다.

## 참고 링크

- [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [Understanding and managing Amazon S3 storage classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
- [S3 Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)
- [S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock-overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
