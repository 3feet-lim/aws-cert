---
type: aws-service
service_name: "AWS Backup"
category: "Storage"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Backup"]
tags: [aws, sap-c02, storage, backup, governance, dr]
created: 2026-05-20
updated: 2026-05-20
---

# AWS Backup

> [!summary] 한 줄 요약
> 여러 AWS 리소스의 백업 정책·보존·cross-account/cross-Region 복사·감사를 중앙에서 관리하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 조직 단위 백업 거버넌스, 랜섬웨어 대비, DR, 감사/규정 준수 |
| 핵심 의사결정 | 여러 서비스의 백업을 중앙 정책으로 표준화해야 하면 AWS Backup |
| 대표 키워드 | centralized backup, backup plan, vault, Vault Lock, cross-account backup, Audit Manager |
| 자주 비교되는 서비스 | [[Amazon EBS]], [[Amazon S3 Glacier]], [[AWS Elastic Disaster Recovery]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: EBS, EFS, RDS, DynamoDB, S3 등 지원 리소스의 백업/복원을 정책화하는 중앙 서비스.
- **왜 쓰는가?**: 계정·리전·서비스별로 흩어진 백업을 backup plan과 vault로 표준화하고 감사한다.
- **관리형 여부**: 관리형 오케스트레이션. 실제 백업 저장/암호화 방식은 리소스 유형에 따라 다를 수 있다.
- **리전/글로벌**: 리전 서비스이며 Organizations 정책, cross-account/cross-Region copy로 확장한다.
- **핵심 제약**: 애플리케이션 실시간 failover 서비스가 아니다. 낮은 RTO/RPO 서버 DR은 AWS DRS와 비교한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Backup Plan | 일정, lifecycle, copy rule, resource assignment 정의 | 조직 표준 백업 정책 |
| Backup Vault | recovery point 저장 컨테이너 | vault policy/KMS/Vault Lock 설계 |
| Cross-Region Copy | 다른 리전에 복구 지점 복사 | 리전 재해 대비 |
| Cross-Account Copy | 다른 계정 vault로 복사 | 랜섬웨어/권한 분리/조직 백업 계정 |
| Vault Lock | governance/compliance mode WORM 보호 | 삭제/보존 변경 방지 |
| Logically air-gapped vault | 추가 보호·공유 복구를 위한 특수 vault | 침해 계정과 분리된 복구 전략 |
| Audit Manager | 백업 준수 상태 평가 | 규정 준수 보고/감사 단서 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Backup]] | 정책 기반 백업/복구 중앙 관리 | 여러 리소스/계정/리전 백업 표준화 | 애플리케이션을 즉시 failover하는 서비스로 착각 |
| [[AWS Elastic Disaster Recovery]] | 서버 단위 지속 복제/복구 인스턴스 launch | 온프레미스/EC2 서버의 낮은 RPO/RTO DR | 일반 백업 보존/감사 목적에는 과함 |
| EBS Snapshot/DLM | EBS 중심 snapshot 자동화 | 단일 EC2/EBS lifecycle | 다중 서비스 중앙 거버넌스에는 부족 |
| [[Amazon S3 Glacier]] | 장기 객체 아카이브 계층 | 저비용 장기 보관 | 백업 정책/복원 작업 중앙관리는 AWS Backup |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-backup-architecture.png]]

1. Organizations 또는 계정별 backup plan이 리소스를 선택한다.
2. 백업은 지정 vault에 recovery point로 저장된다.
3. copy rule로 보안 계정/다른 리전/logically air-gapped vault에 복사한다.
4. Audit Manager와 CloudTrail로 준수 상태를 검증한다.

## 5. 보안 / 거버넌스

- 백업 전용 계정과 cross-account copy를 사용하면 운영 계정 침해 시에도 복구 가능성이 높아진다.
- Vault Lock compliance mode는 grace time 이후 보존 정책 변경/삭제가 제한되므로 설정 전 retention을 신중히 정한다.
- KMS 키 정책과 vault access policy가 cross-account copy/restore의 핵심 장애 지점이다.
- Organizations backup policy로 계정별 누락을 줄인다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> AWS Backup은 “백업 거버넌스” 서비스이지, active-active 애플리케이션 DR을 자동 구성하는 서비스가 아니다.

- RTO가 수분 이내이고 서버 전체를 빠르게 올려야 하면 AWS DRS가 더 직접적일 수 있다.
- cross-Region copy는 리전 장애 대비, cross-account copy는 권한/랜섬웨어 분리 관점이다.
- 모든 리소스의 백업 암호화/복사 제한이 동일하지 않으므로 리소스별 지원 범위를 확인한다.

## 7. 암기 문장

- 여러 AWS 리소스 백업을 조직 차원에서 표준화·감사·보호하면 AWS Backup이다.
- 낮은 RPO/RTO 서버 DR은 AWS DRS, 장기 객체 아카이브는 S3 Glacier와 비교한다.

## 참고 링크

- [AWS Backup Developer Guide](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html)
- [Backup vaults](https://docs.aws.amazon.com/aws-backup/latest/devguide/vaults.html)
- [AWS Backup Vault Lock](https://docs.aws.amazon.com/aws-backup/latest/devguide/vault-lock.html)
- [Logically air-gapped vault](https://docs.aws.amazon.com/aws-backup/latest/devguide/logicallyairgappedvault.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
