---
type: aws-service
service_name: "AWS Config"
category: "Management & Governance"
exam: SAP-C02
exam_domains: ["1. 조직 복잡성", "2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Config", "AWS Config Rules", "Conformance Packs"]
tags: [aws, sap-c02, compliance, governance]
created: 2026-05-26
updated: 2026-05-26
---

# AWS Config

> [!summary] 한 줄 요약
> AWS 리소스 구성 변경 이력과 규정 준수 상태를 기록·평가하는 구성 관리/컴플라이언스 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 구성 변경 추적, compliance evaluation, drift/규정 위반 탐지, conformance pack |
| 핵심 의사결정 | 리소스의 과거/현재 구성과 규칙 준수 여부를 지속 평가해야 하면 AWS Config |
| 대표 키워드 | configuration item, configuration recorder, Config Rules, remediation, conformance packs |
| 자주 비교되는 서비스 | [[AWS CloudTrail]], [[Amazon CloudWatch]], [[AWS Systems Manager]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 리소스 구성 스냅샷과 변경 이력을 기록하고 규칙으로 준수 여부를 평가한다.
- **왜 쓰는가?**: 보안 그룹 공개, S3 암호화 누락, IAM 정책 위반 같은 정책 위반을 찾는다.
- **핵심 제약**: API 호출 감사 로그 원천은 CloudTrail이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Configuration recorder | 리소스 구성 기록 | 변경 이력과 타임라인 |
| Config Rules | 관리형/사용자 지정 규칙 평가 | 컴플라이언스 자동 점검 |
| Remediation | SSM Automation 등으로 수정 | 위반 자동 조치 |
| Conformance Packs | 규칙 묶음 배포 | 조직 표준/규제 기준 적용 |
| Aggregator | 멀티계정/리전 집계 | 중앙 governance |

## 3. 아키텍처 / 동작 흐름

![[attachments/aws/aws-observability-audit-compliance-map.png]]

## 4. 비교 / 선택 기준

| 요구사항 | 선택 | 오답 함정 |
|---|---|---|
| 구성 준수 평가 | AWS Config | CloudTrail은 누가 변경했는지 기록 |
| 성능 알람 | CloudWatch | Config는 운영 성능 지표가 아님 |
| 리소스 수정 자동화 | Config + SSM Automation | Config 단독은 탐지/평가 중심 |

## 5. 헷갈리는 포인트

> [!warning] 주의
> Config는 “리소스 구성 상태와 규정 준수”를 본다. API 감사나 실시간 성능 알람과 혼동하지 않는다.

- 모든 리소스를 기록하면 비용이 커질 수 있어 범위를 설계한다.
- Organizations 환경은 aggregator와 conformance pack을 함께 본다.
- 위반 자동 수정은 SSM Automation 연계가 자주 출제된다.

## 6. 암기 문장

- 구성 변경 이력과 규정 준수는 Config다.
- 누가 바꿨는지는 CloudTrail, 바뀐 결과가 정책 위반인지는 Config다.

## 참고 링크

- [How AWS Config Works](https://docs.aws.amazon.com/config/latest/developerguide/how-does-config-work.html)
- [AWS Config Developer Guide](https://docs.aws.amazon.com/config/latest/developerguide/)
