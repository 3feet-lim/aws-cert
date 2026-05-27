---
type: aws-service
service_name: "AWS Amplify"
category: "Frontend Web & Mobile"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["Amplify"]
tags: [aws, sap-c02, frontend, mobile, hosting]
created: 2026-05-27
updated: 2026-05-27
---

# AWS Amplify

> [!summary] 한 줄 요약
> 프론트엔드/모바일 앱의 호스팅, CI/CD, 인증·API·스토리지 연결을 단순화하는 개발 플랫폼이다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | web/mobile app, hosting, CI/CD, backend integration |
| 대표 키워드 | Amplify, frontend, mobile, hosting |
| 자주 비교되는 서비스 | [[Amazon CloudFront]], [[AWS CodePipeline]], [[AWS Device Farm]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: Git 기반 배포와 Cognito/AppSync/Lambda/S3 연동을 단순화한다.
- **왜 쓰는가?**: 빠른 앱 출시와 프론트엔드 중심 개발에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 세밀한 엔터프라이즈 IaC/배포 통제는 개별 서비스 조합이 적합할 수 있다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Amplify Hosting | 정적/SSR 앱 배포 | CloudFront 기반 배포 |
| Backend integration | Auth/API/Storage 연결 | 개발 생산성 |
| CI/CD | Git push 기반 빌드/배포 | 운영 단순화 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-frontend-mobile-selection-map.png]]

이 그림은 14. Frontend Web & Mobile 영역에서 `AWS Amplify`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon CloudFront]] | CDN | 정적/동적 콘텐츠 전송 | 앱 개발 플랫폼 아님 |
| [[AWS CodePipeline]] | 범용 CI/CD | 복잡한 파이프라인 | 프론트엔드 특화 아님 |
| [[AWS Device Farm]] | 디바이스 테스트 | 앱 품질 검증 | 호스팅 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> AWS Amplify는 `풀스택 앱 개발 플랫폼` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 세밀한 엔터프라이즈 IaC/배포 통제는 개별 서비스 조합이 적합할 수 있다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `AWS Amplify`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| web/mobile app, hosting, CI/CD, backend integration | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[AWS Amplify]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `풀스택 앱 개발 플랫폼`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 프론트엔드/모바일 앱을 빠르게 배포하고 AWS 백엔드와 연결하면 Amplify다.
- Amplify는 여러 AWS 서비스를 묶어 개발 경험을 단순화한다.

## 참고 링크

- [AWS Amplify 공식 문서](https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
