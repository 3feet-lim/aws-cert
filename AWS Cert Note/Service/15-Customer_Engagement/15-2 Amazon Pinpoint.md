---
type: aws-service
service_name: "Amazon Pinpoint"
category: "Customer Engagement"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Pinpoint"]
tags: [aws, sap-c02, campaign, engagement]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Pinpoint

> [!summary] 한 줄 요약
> 사용자 세그먼트, 캠페인, 여정을 통해 이메일·SMS·푸시 등 멀티채널 고객 참여를 관리한다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | campaigns, journeys, segmentation, multi-channel messaging |
| 대표 키워드 | Pinpoint, campaign, engagement |
| 자주 비교되는 서비스 | [[Amazon SES]], [[Amazon SNS]], [[Amazon Personalize]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 이벤트/세그먼트를 기반으로 채널별 메시지와 분석을 제공한다.
- **왜 쓰는가?**: 마케팅 캠페인과 사용자 참여 최적화에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 단순 트랜잭션 이메일은 SES가 단순하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Segments | 대상 그룹 | 타겟팅 |
| Campaign/Journey | 메시지 흐름 | 고객 여정 |
| Channels/Analytics | 이메일/SMS/푸시/분석 | 참여 측정 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-customer-engagement-selection-map.png]]

이 그림은 15. Customer Engagement 영역에서 `Amazon Pinpoint`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon SES]] | 이메일 발송 | 트랜잭션/대량 메일 | 캠페인 플랫폼 아님 |
| [[Amazon SNS]] | 알림 pub/sub | 시스템 알림 | 고객 여정 관리 부족 |
| [[Amazon Personalize]] | 추천 | 개인화 추천 | 메시징 캠페인 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Pinpoint는 `고객 참여 캠페인` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 단순 트랜잭션 이메일은 SES가 단순하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Pinpoint`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| campaigns, journeys, segmentation, multi-channel messaging | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Pinpoint]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `고객 참여 캠페인`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 멀티채널 고객 캠페인과 세그먼트는 Pinpoint다.
- 단순 이메일 전송은 SES가 시험 정답인 경우가 많다.

## 참고 링크

- [Amazon Pinpoint 공식 문서](https://docs.aws.amazon.com/pinpoint/latest/userguide/welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
