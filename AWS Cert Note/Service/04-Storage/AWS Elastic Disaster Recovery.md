---
type: aws-service
service_name: "AWS Elastic Disaster Recovery"
category: "Storage"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: medium
aliases: ["AWS DRS", "Elastic Disaster Recovery"]
tags: [aws, sap-c02, storage, dr, migration]
created: 2026-05-20
updated: 2026-05-20
---

# AWS Elastic Disaster Recovery

> [!summary] 한 줄 요약
> 온프레미스/클라우드 서버를 AWS로 지속 블록 복제하여 장애 시 복구 인스턴스를 빠르게 실행하는 DR 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 서버 DR, 데이터센터 탈출, 낮은 RPO/RTO, DR drill |
| 핵심 의사결정 | 기존 서버를 거의 그대로 AWS에 복구해야 하면 AWS DRS |
| 대표 키워드 | continuous block-level replication, staging area, recovery instance, drill, failback |
| 자주 비교되는 서비스 | [[AWS Backup]], [[AWS Storage Gateway]], [[Amazon EBS]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 소스 서버에 agent를 설치하고 변경 블록을 AWS staging area로 지속 복제하는 DR 서비스.
- **왜 쓰는가?**: 온프레미스 또는 다른 클라우드 서버를 장애 시 AWS EC2로 빠르게 복구한다.
- **관리형 여부**: 복제/복구 오케스트레이션은 관리형이나 네트워크, launch template, 테스트, runbook은 설계해야 한다.
- **리전/글로벌**: target AWS Region에 초기화하고 staging subnet을 구성한다.
- **핵심 제약**: 파일/객체 백업 서비스가 아니라 서버 단위 복제/복구 서비스다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Agent 기반 복제 | 소스 서버 변경 블록을 복제 | lift-and-shift DR, 물리/가상/클라우드 서버 보호 |
| Staging Area | 복제 서버와 EBS가 있는 저비용 subnet | 운영 복구 인스턴스와 다름 |
| Point-in-Time Snapshot | crash-consistent 복구 지점 | 랜섬웨어/오류 전 시점 복구 |
| Drill | 비파괴 복구 테스트 | DR readiness 증명 |
| Recovery Instance | 장애/테스트 때 target subnet에 launch | 실제 서비스 전환은 DNS/라우팅/앱 검증 필요 |
| Failback | 복구 후 원본/다른 위치로 되돌림 | DR 운영 절차 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Elastic Disaster Recovery]] | 서버 전체 지속 복제와 EC2 복구 | 낮은 RPO/RTO, 기존 서버 DR | 중앙 백업 보존/감사는 AWS Backup |
| [[AWS Backup]] | 백업 정책/보존/복구 중앙화 | 여러 AWS 리소스 백업 관리 | 지속 복제 기반 빠른 failover와 혼동 |
| [[AWS Storage Gateway]] | 온프레미스와 AWS storage 연결 | 하이브리드 파일/볼륨/테이프 통합 | 서버 OS/앱 전체 DR 서비스가 아님 |
| AMI/EBS Snapshot | 수동/스케줄 이미지 백업 | 단순 EC2 복원 | 지속 복제와 자동 복구 orchestration 부족 |

## 4. 아키텍처 / 복구 흐름

![[attachments/aws/aws-elastic-disaster-recovery-architecture.png]]

1. 소스 서버에 DRS agent를 설치한다.
2. 변경 블록이 target Region의 staging area subnet으로 지속 복제된다.
3. 장애 또는 drill 시 point-in-time을 선택해 recovery instance를 launch한다.
4. DNS/라우팅/보안 그룹/애플리케이션 검증 후 트래픽을 전환한다.

## 5. 설계 시 고려사항

- **네트워크**: staging subnet CIDR, replication traffic, recovery subnet, 보안 그룹, VPN/DX 연결을 미리 설계한다.
- **복구 자동화**: launch settings, post-launch script, Route 53 전환, ALB target 등록을 runbook화한다.
- **테스트**: drill을 정기 실행해 RTO/RPO와 의존성 복구 순서를 검증한다.
- **규모**: 대량 서버는 계정/리전/할당량/에이전트 배포 자동화가 중요하다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Staging area는 운영 환경이 아니라 복제를 위한 저비용 준비 영역이다. 사용자는 복구 시 recovery instance를 별도로 launch한다.

- AWS DRS는 백업 보존 정책 중심 서비스가 아니다.
- 애플리케이션 정합성은 crash-consistent만으로 충분한지, application-consistent 절차가 필요한지 판단한다.
- DB managed service로 현대화하는 문제가 나오면 DRS보다 DMS/RDS migration이 정답일 수 있다.

## 7. 암기 문장

- “서버를 AWS로 계속 복제하다 장애 시 EC2로 띄운다”는 지문은 AWS DRS다.
- 백업 중앙관리는 AWS Backup, 하이브리드 스토리지 접속은 Storage Gateway와 구분한다.

## 참고 링크

- [AWS Elastic Disaster Recovery User Guide](https://docs.aws.amazon.com/drs/latest/userguide/what-is-drs.html)
- [Getting started with AWS Elastic Disaster Recovery](https://docs.aws.amazon.com/drs/latest/userguide/getting-started.html)
- [Elastic Disaster Recovery concepts](https://docs.aws.amazon.com/drs/latest/userguide/CloudEndure-Concepts.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
