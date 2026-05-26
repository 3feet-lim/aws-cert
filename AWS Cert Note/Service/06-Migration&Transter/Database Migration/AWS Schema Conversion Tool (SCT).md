---
type: aws-service
service_name: "AWS Schema Conversion Tool (SCT)"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["AWS SCT", "Schema Conversion Tool", "DMS Schema Conversion"]
tags: [aws, sap-c02, migration, database, schema-conversion]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Schema Conversion Tool (SCT)

> [!summary] 한 줄 요약
> 이기종 데이터베이스 마이그레이션에서 소스 스키마와 코드 객체를 평가·변환해 타깃 엔진으로 이동할 수 있게 돕는 도구다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | DB 현대화, Oracle/SQL Server → Aurora/RDS/PostgreSQL/MySQL, 스키마 호환성 평가 |
| 핵심 의사결정 | DB 엔진을 바꾸는 이기종 마이그레이션에서 스키마/프로시저/뷰 변환이 필요하면 SCT |
| 대표 키워드 | heterogeneous migration, assessment report, schema conversion, manual action items |
| 자주 비교되는 서비스 | [[AWS Database Migration Service (DMS)]], [[Amazon Aurora]], [[AWS Application Migration Service (MGN)]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 소스 DB 스키마, 저장 프로시저, 함수, 뷰 등을 분석하고 타깃 엔진 호환 형태로 변환을 지원하는 도구.
- **왜 쓰는가?**: 상용 DB에서 오픈소스/관리형 DB로 현대화할 때 변환 난이도와 수동 수정 항목을 파악한다.
- **관리형 여부**: 전통적 SCT는 로컬 설치형 도구이며, DMS Schema Conversion 기능과 함께 출제될 수 있다.
- **리전/글로벌**: 도구 자체보다 소스/타깃 DB 연결과 보안 접근이 중요하다.
- **핵심 제약**: 자동 변환이 불가능한 객체는 manual action이 필요하며 애플리케이션 코드 변경도 별도다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Assessment report | 변환 가능성, effort, 호환성 이슈 분석 | 현대화 의사결정 근거 |
| Schema conversion | 테이블/인덱스/뷰/프로시저 등 변환 | 이기종 DB 이전 필수 단서 |
| Manual action items | 자동 변환 불가 항목 표시 | “완전 자동 아님” 오답 방지 |
| Apply target schema | 변환 스키마를 target DB에 적용 | 이후 DMS 데이터 복제 준비 |
| Data warehouse migration 지원 | 일부 DW → Redshift 평가/변환 | 분석 플랫폼 현대화 시나리오 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-dms-sct-migration-flow.png]]

1. SCT가 소스 DB와 타깃 DB에 연결해 assessment report를 생성한다.
2. 변환 가능한 스키마 객체를 타깃 엔진에 맞게 변환한다.
3. manual action이 필요한 객체는 DBA/개발자가 수정한다.
4. 변환 스키마를 타깃에 적용한 뒤 DMS로 데이터를 full load + CDC한다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Schema Conversion Tool (SCT)]] | 스키마/코드 객체 평가·변환 | Oracle → Aurora PostgreSQL 같은 엔진 변경 | 데이터 복제 자체는 DMS |
| [[AWS Database Migration Service (DMS)]] | 데이터 full load/CDC | 최소 다운타임 데이터 이동 | 복잡한 스키마 변환 자동 해결 아님 |
| Native dump/restore | 엔진 자체 백업/복원 | 동종 엔진, 다운타임 허용 | 엔진 변경/CDC 요구엔 부족 |
| [[AWS Application Migration Service (MGN)]] | 서버 rehost | DB 서버 OS까지 EC2로 그대로 이동 | DB 현대화 요구와 다름 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> “DMS가 이기종 DB를 지원한다”는 말은 데이터 복제 관점이다. 스키마와 DB 코드 변환 평가는 SCT/Schema Conversion을 함께 고려해야 한다.

- SCT는 자동 변환률을 보여주지만 100% 자동 전환을 보장하지 않는다.
- 저장 프로시저, 함수, 트리거, proprietary SQL은 수동 수정 단서가 된다.
- 앱의 SQL 쿼리와 ORM 설정 변경은 별도 애플리케이션 마이그레이션 작업이다.

## 6. 암기 문장

- DB 엔진을 바꾸면 SCT로 스키마를 먼저 평가·변환하고 DMS로 데이터를 옮긴다.
- SCT는 변환 도구이지, 운영 중 변경 데이터 복제 도구가 아니다.

## 참고 링크

- [Getting started with AWS Schema Conversion Tool](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_GettingStarted.html)
- [Converting schemas using AWS SCT](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Converting.Convert.html)
- [What is AWS Database Migration Service?](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
