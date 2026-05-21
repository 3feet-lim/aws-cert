---
type: aws-service
service_name: "Amazon S3 Glacier"
category: "Storage"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["S3 Glacier", "Glacier Flexible Retrieval", "Glacier Deep Archive"]
tags: [aws, sap-c02, storage, archive, compliance]
created: 2026-05-20
updated: 2026-05-20
---

# Amazon S3 Glacier

> [!summary] 한 줄 요약
> 장기 보관·감사·백업 데이터를 낮은 비용으로 저장하는 S3 아카이브 스토리지 클래스 계열이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 비용 최적화, 장기 보관, 규정 준수, 백업/아카이브 |
| 핵심 의사결정 | 접근 빈도와 복원 시간 요구에 따라 Glacier Instant/Flexible/Deep Archive를 고른다 |
| 대표 키워드 | archive, long-term retention, retrieval time, compliance, WORM, vault lock |
| 자주 비교되는 서비스 | [[Amazon S3]], [[AWS Backup]], [[AWS Storage Gateway]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 현대 시험에서는 주로 S3 storage class로 다룬다. 객체는 S3에 남아 있고 아카이브 계층에 저장된다.
- **왜 쓰는가?**: 접근이 드문 데이터를 저비용으로 장기간 보관한다.
- **관리형 여부**: 완전 관리형. lifecycle, retention, 복원 절차, 비용 모델을 설계한다.
- **리전/글로벌**: S3 버킷 리전에 종속. CRR로 다른 리전/계정 아카이브 전략 가능.
- **핵심 제약**: Flexible Retrieval/Deep Archive 객체는 직접 즉시 읽을 수 없고 RestoreObject로 복원 후 접근한다.

## 2. Glacier 계층 선택 기준

| 계층 | 접근 특성 | SAP-C02 선택 단서 | 오답 함정 |
|---|---|---|---|
| S3 Glacier Instant Retrieval | 드물게 접근하지만 밀리초 접근 필요 | 의료 이미지, 장기 보관이지만 즉시 조회 | 복원 지연을 허용한다고 쓰면 비용 최적화 부족 가능 |
| S3 Glacier Flexible Retrieval | 분~시간 복원 허용 | 백업, 아카이브, 가끔 복구 | 즉시 애플리케이션 읽기에는 부적합 |
| S3 Glacier Deep Archive | 거의 접근하지 않고 시간 단위 복원 허용 | 7~10년 보관, 규정/감사, 최저 비용 | 빠른 RTO 요구와 충돌 |
| S3 Intelligent-Tiering Archive tiers | 접근 패턴이 바뀌고 자동 계층화 필요 | 운영 부담 최소화 | archive tier는 복원 필요 |

## 3. 아키텍처 / 복원 흐름

![[attachments/aws/amazon-s3-glacier-flow.png]]

1. 객체를 S3 Standard/IA에 저장한다.
2. Lifecycle rule이 보관 기간에 따라 Glacier 계층으로 이동한다.
3. 복구 시 retrieval option을 선택해 restore 요청을 수행한다.
4. 임시 복원 사본을 읽거나 필요한 경우 다른 storage class로 copy한다.

## 4. 보안 / 거버넌스

- S3 Object Lock을 사용하면 WORM 보관 요구를 S3 객체 버전 단위로 적용할 수 있다.
- 과거 Amazon Glacier Vault Lock 개념도 있지만, SAP-C02에서는 S3 Object Lock, AWS Backup Vault Lock과 구분한다.
- 암호화, bucket policy, KMS key policy, CloudTrail data events를 함께 설계한다.

## 5. 비용 / 운영 포인트

- 저장 비용은 낮지만 retrieval fee, 요청 비용, 최소 보관 기간, metadata overhead가 시험 함정이다.
- lifecycle로 자동 전환하되 너무 작은/짧은 생명주기 객체를 과도하게 아카이브하면 비용 이점이 줄 수 있다.
- RTO가 짧은 시스템의 primary 복구 데이터는 Deep Archive가 아니라 Standard/IA/Instant Retrieval/복제본을 검토한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> “저렴한 장기 보관”만 보고 Deep Archive를 고르면 안 된다. 복원 시간과 RTO가 지문에 있으면 계층이 달라진다.

- S3 Glacier Flexible Retrieval과 Deep Archive는 객체 restore가 필요하다.
- 백업을 중앙 정책으로 보호하고 리소스별 복구를 관리하려면 [[AWS Backup]]이 더 직접적인 답일 수 있다.
- 온프레미스 테이프 백업 소프트웨어를 유지하려면 [[AWS Storage Gateway]] Tape Gateway가 단서다.

## 7. 암기 문장

- Glacier는 장기 보관 정답이지만, 시험의 핵심은 “얼마나 빨리 복원해야 하는가”이다.
- 즉시 접근은 Instant Retrieval, 분~시간은 Flexible Retrieval, 가장 긴 장기 최저 비용은 Deep Archive다.

## 참고 링크

- [Understanding Amazon S3 storage classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
- [Understanding archive retrieval options](https://docs.aws.amazon.com/AmazonS3/latest/userguide/restoring-objects-retrieval-options.html)
- [S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock-overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
