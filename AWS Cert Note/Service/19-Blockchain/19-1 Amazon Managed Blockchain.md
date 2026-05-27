---
type: aws-service
service_name: "Amazon Managed Blockchain"
category: "Blockchain"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Managed Blockchain"]
tags: [aws, sap-c02, blockchain, ledger]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Managed Blockchain

> [!summary] 한 줄 요약
> 여러 조직이 공유 원장과 멤버십 거버넌스를 필요로 할 때 블록체인 네트워크/노드 운영 부담을 줄이는 관리형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | permissioned blockchain, consortium, Ethereum nodes, shared ledger |
| 대표 키워드 | Managed Blockchain, blockchain, ledger |
| 자주 비교되는 서비스 | [[Amazon QLDB]], [[Amazon DynamoDB]], [[AWS Database Migration Service]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 멤버, 네트워크, 노드 운영을 관리형으로 제공해 애플리케이션이 원장과 상호작용하게 한다.
- **왜 쓰는가?**: 중앙 신뢰 주체 없이 여러 조직이 거래 기록을 공유해야 할 때 사용한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 중앙 DB나 단일 조직 원장으로 충분하면 블록체인은 과한 선택이다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Network/members | 컨소시엄 멤버십 | 조직 간 거버넌스 |
| Nodes | 원장 접근 노드 | 애플리케이션 연동 |
| Managed operations | 인프라/가용성 관리 | 운영 부담 감소 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-blockchain-selection-map.png]]

이 그림은 19. Blockchain 영역에서 `Amazon Managed Blockchain`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon QLDB]] | 중앙 신뢰 기관의 변경 불가 원장 | 단일 조직 감사 원장 | 분산 합의/컨소시엄 불필요 |
| [[Amazon DynamoDB]] | NoSQL DB | 고성능 앱 데이터 | 블록체인 합의 없음 |
| [[AWS Database Migration Service]] | DB 마이그레이션 | 데이터 이전 | 원장 네트워크 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Managed Blockchain는 `관리형 블록체인 네트워크/노드` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 중앙 DB나 단일 조직 원장으로 충분하면 블록체인은 과한 선택이다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Managed Blockchain`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| permissioned blockchain, consortium, Ethereum nodes, shared ledger | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Managed Blockchain]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `관리형 블록체인 네트워크/노드`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 여러 조직 간 탈중앙 공유 원장과 멤버십 거버넌스가 핵심이면 Managed Blockchain이다.
- 중앙 기관을 신뢰할 수 있으면 QLDB/일반 DB가 더 단순하다.

## 참고 링크

- [Amazon Managed Blockchain 공식 문서](https://docs.aws.amazon.com/managed-blockchain/latest/managementguide/managed-blockchain-overview.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
