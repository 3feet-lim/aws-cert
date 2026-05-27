---
type: aws-service
service_name: "AWS Device Farm"
category: "Frontend Web & Mobile"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Device Farm"]
tags: [aws, sap-c02, testing, mobile]
created: 2026-05-27
updated: 2026-05-27
---

# AWS Device Farm

> [!summary] 한 줄 요약
> 실제 모바일 디바이스와 브라우저에서 앱 테스트를 실행하는 관리형 테스트 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | real devices, mobile testing, browser testing |
| 대표 키워드 | Device Farm, testing, mobile |
| 자주 비교되는 서비스 | [[AWS Amplify]], [[AWS CodeBuild]], [[Amazon CloudWatch]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 자동화 테스트와 원격 접근으로 호환성 문제를 검증한다.
- **왜 쓰는가?**: 다양한 기기/OS 조합 테스트를 직접 보유하지 않고 수행한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 앱 배포/호스팅 서비스가 아니다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Real devices | 실제 디바이스 테스트 | 호환성 검증 |
| Automated tests | 테스트 스위트 실행 | 품질 자동화 |
| Remote access/reports | 수동 디버깅과 결과 보고 | 문제 분석 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-frontend-mobile-selection-map.png]]

이 그림은 14. Frontend Web & Mobile 영역에서 `AWS Device Farm`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Amplify]] | 앱 개발/호스팅 | 배포와 백엔드 연결 | 테스트 서비스 아님 |
| [[AWS CodeBuild]] | 빌드/테스트 실행 | 일반 CI | 실디바이스 랩 아님 |
| [[Amazon CloudWatch]] | 모니터링 | 운영 관측 | 테스트 실행 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS Device Farm는 `실디바이스 테스트` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 앱 배포/호스팅 서비스가 아니다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS Device Farm`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| real devices, mobile testing, browser testing | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS Device Farm]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `실디바이스 테스트`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 실제 디바이스 호환성 테스트는 Device Farm이다.
- Device Farm은 앱을 운영 배포하는 서비스가 아니다.

## 참고 링크

- [AWS Device Farm 공식 문서](https://docs.aws.amazon.com/devicefarm/latest/developerguide/welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
