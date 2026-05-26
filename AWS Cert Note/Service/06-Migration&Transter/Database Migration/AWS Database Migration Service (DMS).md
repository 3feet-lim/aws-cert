---
type: aws-service
service_name: "AWS Database Migration Service (DMS)"
category: "Migration & Transfer"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: high
aliases: ["AWS DMS", "Database Migration Service", "DMS CDC"]
tags: [aws, sap-c02, migration, database, cdc]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Database Migration Service (DMS)

> [!summary] 한 줄 요약
> 소스 DB를 계속 운영하면서 full load와 CDC로 데이터를 AWS 또는 다른 데이터 저장소로 이전·복제하는 데이터베이스 마이그레이션 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | DB 마이그레이션, 최소 다운타임, 동종/이기종 엔진, CDC, 데이터 검증 |
| 핵심 의사결정 | 운영 DB를 멈추지 않고 데이터만 지속 복제해 cutover하려면 DMS |
| 대표 키워드 | full load, change data capture, replication instance, source/target endpoint, homogeneous/heterogeneous |
| 자주 비교되는 서비스 | [[AWS Schema Conversion Tool (SCT)]], [[AWS Application Migration Service (MGN)]], [[AWS DataSync]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: source endpoint와 target endpoint 사이에서 데이터를 로드하고 변경분을 복제하는 관리형 마이그레이션 서비스.
- **왜 쓰는가?**: DB 다운타임을 줄이고 RDS/Aurora/Redshift/S3/DynamoDB 등으로 이전하거나 복제한다.
- **관리형 여부**: replication instance 또는 DMS Serverless로 복제 인프라를 관리한다.
- **리전/글로벌**: 리전 서비스이며 소스/타깃 네트워크 연결과 보안 그룹 구성이 중요하다.
- **핵심 제약**: 스키마/코드/SQL 호환성을 완전히 자동 해결하지 않는다. 이기종 엔진은 SCT/Schema Conversion을 함께 본다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Full load | 기존 데이터를 한 번 적재 | 초기 대량 이전 |
| CDC | 변경 데이터를 지속 복제 | 최소 다운타임 cutover 핵심 |
| Replication instance / Serverless | DMS 작업 실행 인프라 | 성능, 비용, HA, 스케일 고려 |
| Source/Target endpoint | DB/S3/Redshift 등 연결 정의 | 네트워크·권한·SSL 설정 |
| Data validation | 소스/타깃 데이터 비교 | cutover 전 검증 |
| DMS Fleet Advisor / Schema Conversion | 평가와 스키마 변환 지원 | 현대화/이기종 마이그레이션 단서 |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-dms-sct-migration-flow.png]]

1. 동종 엔진이면 DMS로 full load + CDC를 구성한다.
2. 이기종 엔진이면 SCT 또는 DMS Schema Conversion으로 스키마/코드 변환 가능성을 평가한다.
3. DMS replication task가 source에서 데이터를 읽어 target에 적재하고 변경분을 계속 반영한다.
4. CDC lag와 validation을 확인한 뒤 애플리케이션 cutover를 수행한다.

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| Oracle on-prem → Amazon RDS Oracle, 최소 다운타임 | DMS | 단순 dump/restore는 다운타임이 길 수 있음 |
| Oracle → Aurora PostgreSQL | SCT/Schema Conversion + DMS | DMS만으로 앱 SQL/프로시저 호환성 해결 불가 |
| 서버 전체를 EC2로 이전 | MGN | DMS는 DB 데이터 이동 도구 |
| 파일/객체 대량 복사 | DataSync/Snow | DMS는 DB/데이터 저장소 마이그레이션 중심 |
| 데이터 웨어하우스/분석 타깃 | DMS → Redshift/S3 등 | ETL 변환 요구가 크면 Glue/EMR과 구분 |

## 5. 설계 시 고려사항

- **네트워크**: replication instance가 source와 target 모두에 접근해야 한다.
- **성능**: LOB 처리, 병렬 로드, task 설정, 인덱스/제약조건, CDC 로그 보존을 검토한다.
- **정합성**: validation, CDC latency, cutover window, rollback 계획이 필요하다.
- **보안**: KMS at-rest 암호화, SSL in-transit, Secrets Manager/IAM 권한을 고려한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> DMS는 데이터 이동/복제 서비스다. 이기종 엔진의 스키마·프로시저·애플리케이션 SQL 변경은 별도 평가와 수정이 필요하다.

- DMS는 마이그레이션 중 소스 DB가 계속 운영되도록 CDC를 사용할 수 있다.
- 스키마 생성은 제한적으로 가능하지만 복잡한 이기종 변환은 SCT/Schema Conversion이 핵심이다.
- DB가 아니라 파일 시스템이나 객체 저장소 이동이면 DataSync/Snow를 먼저 본다.

## 7. 암기 문장

- DB를 켜둔 채 full load + CDC로 옮기면 DMS다.
- 이기종 DB는 “SCT로 스키마, DMS로 데이터”라고 외운다.

## 참고 링크

- [What is AWS Database Migration Service?](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html)
- [AWS Schema Conversion Tool User Guide](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_GettingStarted.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
