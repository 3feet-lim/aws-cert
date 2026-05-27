---
type: aws-service
service_name: "Amazon AppStream 2.0"
category: "End User Computing"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["AppStream"]
tags: [aws, sap-c02, application-streaming]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon AppStream 2.0

> [!summary] 한 줄 요약
> 데스크톱 애플리케이션을 브라우저/클라이언트로 스트리밍하는 관리형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | application streaming, non-persistent sessions, fleets |
| 대표 키워드 | AppStream, application-streaming |
| 자주 비교되는 서비스 | [[Amazon WorkSpaces]], [[Amazon EC2]], [[AWS Device Farm]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 사용자는 로컬 설치 없이 AWS에서 실행되는 앱 화면을 스트리밍한다.
- **왜 쓰는가?**: 특정 앱 제공, 교육/파트너 접근, 데이터 유출 감소에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 영구 개인 데스크톱은 WorkSpaces가 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Fleets/Stacks | 앱 실행 인프라/사용자 노출 | 확장 운영 |
| Image Builder | 표준 앱 이미지 구성 | 배포 관리 |
| Non-persistent session | 세션 기반 앱 사용 | 보안/운영 단순화 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-end-user-computing-selection-map.png]]

이 그림은 16. End User Computing 영역에서 `Amazon AppStream 2.0`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon WorkSpaces]] | 전체 데스크톱 | 사용자별 VDI | 앱 스트리밍과 다름 |
| [[Amazon EC2]] | 직접 앱 서버 | 자체 운영 | 관리형 스트리밍 아님 |
| [[AWS Device Farm]] | 앱 테스트 | 품질 검증 | 앱 제공 서비스 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon AppStream 2.0는 `애플리케이션 스트리밍` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 영구 개인 데스크톱은 WorkSpaces가 적합하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon AppStream 2.0`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| application streaming, non-persistent sessions, fleets | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon AppStream 2.0]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `애플리케이션 스트리밍`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 특정 애플리케이션을 스트리밍하면 AppStream 2.0이다.
- 전체 데스크톱 요구는 WorkSpaces다.

## 참고 링크

- [Amazon AppStream 2.0 공식 문서](https://docs.aws.amazon.com/appstream2/latest/developerguide/what-is-appstream.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
