---
type: aws-service
service_name: "AWS Application Migration Service (MGN)"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["AWS MGN", "Application Migration Service", "CloudEndure Migration replacement"]
tags: [aws, sap-c02, migration, rehost, lift-and-shift]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Application Migration Service (MGN)

> [!summary] 한 줄 요약
> 온프레미스/다른 클라우드 서버를 블록 레벨로 지속 복제해 AWS EC2로 빠르게 rehost(lift-and-shift)하는 서버 마이그레이션 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 데이터센터 탈출, 서버 rehost, 최소 다운타임 cutover, wave 단위 대량 이전 |
| 핵심 의사결정 | 앱 구조 변경 없이 기존 서버를 EC2로 빠르게 이전해야 하면 MGN |
| 대표 키워드 | lift-and-shift, rehost, block-level replication, staging area, test launch, cutover |
| 자주 비교되는 서비스 | [[AWS Elastic Disaster Recovery]], [[AWS Database Migration Service (DMS)]], [[AWS Migration Hub]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 소스 서버 디스크 변경 블록을 AWS staging area로 지속 복제하고, 테스트/전환 시 EC2 인스턴스를 실행하는 서비스.
- **왜 쓰는가?**: 애플리케이션을 크게 수정하지 않고 빠르게 AWS로 이전한다.
- **관리형 여부**: 복제/전환 오케스트레이션은 관리형이지만 agent 배포, 네트워크, launch template, 검증 runbook은 설계해야 한다.
- **리전/글로벌**: 대상 리전에 staging subnet과 복제 인프라를 구성한다.
- **핵심 제약**: rehost 중심이다. DB 엔진 변경, 앱 리팩터링, 스키마 변환은 별도 도구가 필요하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Replication agent / agentless | 소스 서버 변경 블록 복제 | 물리/가상/클라우드 서버 lift-and-shift |
| Staging area | 복제 서버와 staging EBS가 있는 저비용 영역 | 운영 인스턴스가 아니라 준비 영역 |
| Test launch | 실제 cutover 전 테스트 인스턴스 실행 | 비파괴 검증, migration readiness |
| Cutover launch | 운영 전환용 EC2 실행 | DNS/라우팅/검증 절차와 함께 수행 |
| Wave/Application 관리 | 서버를 그룹화해 순차 이전 | 대규모 이전 계획과 Migration Hub 연계 |
| Post-launch actions | 에이전트 제거, SSM, 현대화 스크립트 등 | 이전 후 운영 표준화 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-application-migration-service-mgn-flow.png]]

1. 소스 서버에 MGN agent를 설치하거나 지원되는 VMware agentless 방식을 사용한다.
2. 변경 블록이 Target AWS Region의 staging area subnet으로 지속 복제된다.
3. test launch로 앱 동작, 네트워크, 보안 그룹, 성능을 검증한다.
4. cutover launch 후 DNS/라우팅을 전환하고 post-launch action으로 운영 표준을 적용한다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Application Migration Service (MGN)]] | 서버 전체 rehost 마이그레이션 | 최소 변경, 빠른 데이터센터 탈출 | 앱 구조 현대화는 아님 |
| [[AWS Elastic Disaster Recovery]] | 동일한 복제 기술 계열이지만 목적은 DR | 장애 복구/DR drill/RPO-RTO | 마이그레이션 프로젝트면 MGN |
| [[AWS Database Migration Service (DMS)]] | DB 데이터 복제와 CDC | DB만 이전하거나 엔진 변경 | OS/앱 서버 전체 복제는 MGN |
| [[AWS Migration Hub]] | 포트폴리오 추적 | 여러 앱 진행률 관리 | 실제 복제는 하지 않음 |

## 5. 설계 시 고려사항

- **네트워크**: 소스→AWS 복제 트래픽, staging subnet, cutover subnet, 보안 그룹, VPN/DX를 설계한다.
- **Launch 설정**: 인스턴스 타입, subnet, IAM role, EBS, tags, post-launch actions를 사전에 정의한다.
- **검증**: test launch, 앱 smoke test, 데이터 정합성, DNS TTL, rollback 절차를 준비한다.
- **현대화**: rehost 후 RDS/Aurora, Auto Scaling, ALB, managed service로 단계적 개선한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> MGN은 “일단 EC2로 가져오는” rehost 서비스다. 문제에서 DB 엔진 변경, 스키마 변환, SQL 호환성까지 요구하면 DMS/SCT가 필요하다.

- staging area는 복제용이며 사용자가 접속하는 운영 환경이 아니다.
- cutover는 MGN launch만으로 끝나지 않고 DNS, 라우팅, 보안, 앱 검증이 필요하다.
- “재해 복구” 요구사항이면 AWS DRS와 비교한다.

## 7. 암기 문장

- 서버를 거의 그대로 EC2로 옮기는 lift-and-shift는 MGN이다.
- MGN은 rehost, DMS/SCT는 DB 마이그레이션/스키마 변환, Migration Hub는 추적이다.

## 참고 링크

- [What Is AWS Application Migration Service?](https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html)
- [AWS Migration Hub User Guide](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
