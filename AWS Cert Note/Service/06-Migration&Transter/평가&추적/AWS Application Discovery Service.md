---
type: aws-service
service_name: "AWS Application Discovery Service"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["Application Discovery Service", "Discovery Agent", "Agentless Collector"]
tags: [aws, sap-c02, migration, discovery, assessment]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Application Discovery Service

> [!summary] 한 줄 요약
> 온프레미스 서버와 데이터베이스의 구성, 사용률, 프로세스, 네트워크 의존성을 수집해 마이그레이션 계획을 돕는 discovery 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 마이그레이션 사전 평가, 서버 인벤토리, 의존성 매핑, right-sizing |
| 핵심 의사결정 | 기존 데이터센터의 서버/DB 정보를 수집해 Migration Hub에서 애플리케이션 그룹과 wave를 만들려면 Application Discovery Service |
| 대표 키워드 | agentless collector, discovery agent, server utilization, network dependencies, Migration Hub Home Region |
| 자주 비교되는 서비스 | [[AWS Migration Hub]], [[AWS Database Migration Service (DMS)]], [[AWS Application Migration Service (MGN)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 온프레미스 서버/VM/DB에 대한 구성·성능·의존성 데이터를 수집하는 마이그레이션 평가 서비스.
- **왜 쓰는가?**: EC2 사이징, 서버 그룹화, 애플리케이션 의존성, DB 마이그레이션 후보를 파악한다.
- **관리형 여부**: 수집 도구는 agent/collector 형태로 배포하고, 데이터는 AWS 서비스에 저장·조회한다.
- **리전/글로벌**: 데이터는 Migration Hub Home Region에 저장된다.
- **핵심 제약**: 발견/평가용이다. 서버 복제나 DB 데이터 이동은 하지 않는다.

## 2. 수집 방식과 시험 포인트

| 방식 | 수집 대상 | 강점 | 시험 포인트 |
|---|---|---|---|
| Agentless Collector | VMware vCenter, DB/Analytics 서버 | VM 단위 배포 부담이 낮음 | VMware 환경 인벤토리/사용률 수집 |
| Discovery Agent | Linux/Windows 서버 | 프로세스, 네트워크 연결, 시계열 성능 | 물리/가상 서버의 상세 의존성 분석 |
| File import | CSV 등 기존 인벤토리 | 빠른 시작 | 도구 설치 없이 기존 CMDB 데이터 활용 |
| Partner tools | APN migration tool | 기존 도구 연계 | Migration Hub로 결과 통합 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-migration-hub-discovery-flow.png]]

1. Agentless Collector, Discovery Agent, CSV import 중 환경에 맞는 방식을 선택한다.
2. 수집 데이터는 Migration Hub Home Region에 저장된다.
3. Migration Hub에서 서버를 애플리케이션으로 그룹화하고 wave를 설계한다.
4. MGN/DMS 같은 실행 도구로 마이그레이션하면서 진행률을 추적한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 온프레미스 서버 인벤토리와 사용률 수집 | Application Discovery Service | Migration Hub만으로는 데이터 수집이 충분하지 않음 |
| 마이그레이션 전체 진행률 추적 | Migration Hub | Discovery Service는 추적 허브가 아님 |
| 서버를 AWS로 rehost | MGN | Discovery는 복제 엔진이 아님 |
| DB 데이터 최소 다운타임 이동 | DMS | Discovery는 DB 데이터 복제 서비스가 아님 |

## 5. 설계 시 고려사항

- **Home Region**: discovery 시작 전 Migration Hub Home Region을 정한다.
- **수집 깊이**: agentless는 배포 부담이 낮고, agent 기반은 네트워크/프로세스 의존성 분석이 강하다.
- **보안**: 수집 권한, 에이전트 설치 범위, 데이터 보존/접근 권한을 검토한다.
- **분석 활용**: Athena/QuickSight 또는 export로 비용 모델과 wave 계획을 보강할 수 있다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> “애플리케이션 의존성 확인 후 마이그레이션 계획”은 Discovery Service + Migration Hub이고, “서버 복제 후 cutover”는 MGN이다.

- Discovery Agent는 모든 서버에 설치해야 하므로 배포/권한 부담이 있다.
- Agentless Collector는 VMware 중심 시나리오에서 자주 등장한다.
- DB 마이그레이션 평가는 DMS Fleet Advisor/Schema Conversion과 함께 출제될 수 있다.

## 7. 암기 문장

- 마이그레이션 전에 “무엇이 어디서 얼마나 쓰이는지” 찾는 서비스는 Application Discovery Service다.
- 발견 데이터는 Migration Hub Home Region으로 모이고, 실행은 MGN/DMS가 한다.

## 참고 링크

- [What is AWS Application Discovery Service?](https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html)
- [What Is AWS Migration Hub?](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
