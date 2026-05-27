---
type: aws-service
service_name: "Amazon WorkSpaces"
category: "End User Computing"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["WorkSpaces"]
tags: [aws, sap-c02, vdi, desktop]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon WorkSpaces

> [!summary] 한 줄 요약
> 사용자에게 관리형 클라우드 가상 데스크톱을 제공하는 DaaS 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | virtual desktop, persistent desktop, directory integration |
| 대표 키워드 | WorkSpaces, vdi, desktop |
| 자주 비교되는 서비스 | [[Amazon AppStream 2.0]], [[Amazon EC2]], [[AWS Client VPN]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 사용자는 클라이언트로 개인 데스크톱 환경에 접속한다.
- **왜 쓰는가?**: VDI, 원격 근무, 데이터 중앙화 요구에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 개별 애플리케이션 스트리밍은 AppStream 2.0이 더 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Persistent desktop | 사용자별 데스크톱 | VDI 경험 |
| Directory integration | AD/Identity 연동 | 기업 인증 |
| Bundles/Images | 표준 데스크톱 구성 | 운영 표준화 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-end-user-computing-selection-map.png]]

이 그림은 16. End User Computing 영역에서 `Amazon WorkSpaces`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon AppStream 2.0]] | 애플리케이션 스트리밍 | 특정 앱 제공 | 전체 데스크톱 아님 |
| [[Amazon EC2]] | 가상 서버 | 직접 데스크톱 구성 가능 | VDI 관리형 경험 부족 |
| [[AWS Client VPN]] | 네트워크 접속 | 원격 네트워크 접근 | 데스크톱 제공 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon WorkSpaces는 `관리형 가상 데스크톱` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 개별 애플리케이션 스트리밍은 AppStream 2.0이 더 적합하다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon WorkSpaces`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| virtual desktop, persistent desktop, directory integration | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon WorkSpaces]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 가상 데스크톱`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 영구 개인 클라우드 데스크톱은 WorkSpaces다.
- 앱만 스트리밍하면 AppStream 2.0과 구분한다.

## 참고 링크

- [Amazon WorkSpaces 공식 문서](https://docs.aws.amazon.com/workspaces/latest/adminguide/amazon-workspaces.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
