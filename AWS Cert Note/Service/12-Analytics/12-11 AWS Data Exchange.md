---
type: aws-service
service_name: "AWS Data Exchange"
category: "Analytics"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선", "4. 마이그레이션/현대화"]
status: complete
priority: low
aliases: ["Data Exchange"]
tags: [aws, sap-c02, data-marketplace]
created: 2026-05-27
updated: 2026-05-27
---

# AWS Data Exchange

> [!summary] 한 줄 요약
> 서드파티 데이터 세트를 AWS에서 구독·교환하는 데이터 마켓플레이스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선, 4. 마이그레이션/현대화 |
| 핵심 의사결정 | third-party data, subscriptions, data products |
| 대표 키워드 | Data Exchange, data-marketplace |
| 자주 비교되는 서비스 | [[AWS Marketplace]], [[AWS Lake Formation]], [[Amazon S3]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 데이터 공급자와 구독자가 데이터 제품을 안전하게 교환한다.
- **왜 쓰는가?**: 외부 데이터 구매/공유를 AWS 네이티브로 처리한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: ETL/쿼리/BI 서비스가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Data products | 파일/API/Redshift 등 데이터 제품 | 외부 데이터 구독 |
| Subscriptions | 라이선스/구독 관리 | 상용 데이터 조달 |
| Entitlements | 권한 부여 | 데이터 공유 통제 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-analytics-selection-map.png]]

이 그림은 12. Analytics 영역에서 `AWS Data Exchange`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Marketplace]] | 소프트웨어/서비스 구매 | 상용 SW 조달 | 데이터 제품 특화 아님 |
| [[AWS Lake Formation]] | 데이터 레이크 권한 | 내부 데이터 거버넌스 | 마켓플레이스 아님 |
| [[Amazon S3]] | 객체 저장 | 데이터 보관 | 구독/라이선스 기능 없음 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS Data Exchange는 `데이터 마켓플레이스` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- ETL/쿼리/BI 서비스가 아니다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS Data Exchange`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| third-party data, subscriptions, data products | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS Data Exchange]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `데이터 마켓플레이스`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 외부/상용 데이터 세트를 AWS에서 구독하면 Data Exchange다.
- 분석 엔진이 아니라 데이터 제품 거래·배포 계층이다.

## 참고 링크

- [AWS Data Exchange 공식 문서](https://docs.aws.amazon.com/data-exchange/latest/userguide/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
