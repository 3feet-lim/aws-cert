---
type: aws-service
service_name: "AWS Migration Hub"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Migration Hub", "AWS Migration Hub Home Region"]
tags: [aws, sap-c02, migration, governance, tracking]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Migration Hub

> [!summary] 한 줄 요약
> 여러 마이그레이션 도구의 발견 데이터, 애플리케이션 그룹, 진행 상태를 한 곳에서 추적하는 마이그레이션 포트폴리오 관리 콘솔이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 대규모 마이그레이션 계획, 애플리케이션 포트폴리오 가시화, 여러 도구의 진행률 통합 |
| 핵심 의사결정 | 서버/DB를 애플리케이션 단위로 묶고 MGN/DMS/Partner 도구 진행 상태를 중앙에서 추적해야 하면 Migration Hub |
| 대표 키워드 | migration portfolio, application grouping, migration status tracking, Home Region, discovery data |
| 자주 비교되는 서비스 | [[AWS Application Discovery Service]], [[AWS Application Migration Service (MGN)]], [[AWS Database Migration Service (DMS)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 기존 서버를 발견하고 애플리케이션으로 그룹화하며 마이그레이션 상태를 추적하는 관리형 허브.
- **왜 쓰는가?**: 조직 단위의 wave 계획, 의존성 파악, 서버/DB/앱 진행률 보고를 한 콘솔에서 관리한다.
- **관리형 여부**: 관리형 콘솔/서비스. 실제 복제·cutover는 MGN, DMS, Partner 도구가 수행한다.
- **리전/글로벌**: Migration Hub Home Region을 설정하고 발견/계획 데이터를 그 리전에 저장한다.
- **핵심 제약**: Migration Hub 자체는 마이그레이션 엔진이 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Home Region | 발견 데이터와 추적 정보를 저장하는 기준 리전 | 대규모 마이그레이션 전 먼저 설정해야 하는 단서 |
| Application grouping | 발견된 서버를 애플리케이션 단위로 묶음 | wave 계획과 의존성 추적 |
| Status tracking | MGN, DMS 등 도구의 상태를 통합 표시 | 여러 마이그레이션 도구를 동시에 쓰는 조직 문제 |
| Discovery 통합 | Application Discovery Service, import, partner 도구 데이터 활용 | 사전 평가/계획 단계와 연결 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-migration-hub-discovery-flow.png]]

1. Application Discovery Service 또는 CSV/Partner 도구로 온프레미스 인벤토리와 사용률을 수집한다.
2. 발견 데이터는 Migration Hub Home Region에 저장된다.
3. 서버를 애플리케이션으로 그룹화하고 migration wave를 계획한다.
4. 실제 마이그레이션은 MGN/DMS/Partner 도구로 수행하고 Migration Hub에서 상태를 추적한다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Migration Hub]] | 계획/추적/포트폴리오 가시화 | 여러 앱과 도구의 진행률 통합 | 직접 서버나 DB를 복제하지 않음 |
| [[AWS Application Discovery Service]] | 온프레미스 서버/DB 정보 수집 | 평가·권장 사이징·의존성 파악 | 추적 허브가 아니라 데이터 수집 도구 |
| [[AWS Application Migration Service (MGN)]] | 서버 rehost 복제/전환 | VM/물리 서버를 EC2로 lift-and-shift | 포트폴리오 관리 기능과 혼동 |
| [[AWS Database Migration Service (DMS)]] | DB 데이터 복제/CDC | DB 마이그레이션 최소 다운타임 | 애플리케이션 전체 추적 도구가 아님 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Migration Hub는 “마이그레이션을 실행하는 서비스”가 아니라 “마이그레이션을 계획하고 추적하는 서비스”다.

- Home Region을 설정하지 않으면 발견 데이터 저장과 추적 흐름에서 문제가 된다.
- 서버/DB 의존성 수집은 Application Discovery Service가 담당하고, Migration Hub는 그 데이터를 보여주고 묶는다.
- 실제 cutover는 MGN, DMS, DNS/라우팅 변경, 애플리케이션 검증 runbook으로 수행한다.

## 6. SAP-C02 시나리오 패턴

- **문제 상황**: 수백 개 서버와 여러 데이터베이스를 wave 단위로 AWS로 이전해야 한다.
- **요구사항**: 앱별 그룹화, 진행률 대시보드, 여러 마이그레이션 도구 통합 추적.
- **정답 단서**: Migration Hub + Application Discovery Service + MGN/DMS.
- **오답 함정**: MGN만 선택하면 포트폴리오 추적 요구사항을 놓친다.

## 7. 암기 문장

- 마이그레이션 포트폴리오를 “발견·그룹화·추적”하면 Migration Hub다.
- Migration Hub는 허브이고, 실제 이동은 MGN/DMS/DataSync/Snow 같은 실행 도구가 한다.

## 참고 링크

- [What Is AWS Migration Hub?](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)
- [AWS Application Discovery Service User Guide](https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
