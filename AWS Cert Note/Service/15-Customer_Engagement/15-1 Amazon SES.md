---
type: aws-service
service_name: "Amazon SES"
category: "Customer Engagement"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["SES", "Simple Email Service"]
tags: [aws, sap-c02, email, messaging]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon SES

> [!summary] 한 줄 요약
> 트랜잭션/마케팅 이메일을 대규모로 발송하는 관리형 이메일 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | email sending, domain verification, bounce/complaint |
| 대표 키워드 | SES, Simple Email Service, email, messaging |
| 자주 비교되는 서비스 | [[Amazon Pinpoint]], [[Amazon SNS]], [[Amazon Connect]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 도메인/이메일 검증 후 API/SMTP로 이메일을 전송한다.
- **왜 쓰는가?**: 주문 확인, 알림, 대량 이메일을 비용 효율적으로 보낸다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 멀티채널 캠페인 여정은 Pinpoint가 더 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Identity/DKIM | 도메인 검증과 인증 | 전달률/보안 |
| Bounce/Complaint | 반송/불만 처리 | 평판 관리 |
| SMTP/API | 앱 연동 | 트랜잭션 메일 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-customer-engagement-selection-map.png]]

이 그림은 15. Customer Engagement 영역에서 `Amazon SES`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Pinpoint]] | 멀티채널 캠페인 | 세그먼트/여정/분석 | SES보다 캠페인 중심 |
| [[Amazon SNS]] | pub/sub 알림 | SMS/푸시 일부 지원 | 이메일 마케팅 플랫폼 아님 |
| [[Amazon Connect]] | 컨택센터 | 음성 상담 | 이메일 발송 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon SES는 `이메일 발송` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 멀티채널 캠페인 여정은 Pinpoint가 더 적합하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon SES`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| email sending, domain verification, bounce/complaint | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon SES]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `이메일 발송`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 대량/트랜잭션 이메일 발송은 SES다.
- 캠페인·세그먼트·멀티채널 참여는 Pinpoint와 구분한다.

## 참고 링크

- [Amazon SES 공식 문서](https://docs.aws.amazon.com/ses/latest/dg/Welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
