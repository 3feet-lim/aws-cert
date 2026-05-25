---
type: aws-service
service_name: "Amazon Inspector"
category: "02-Security&Compliance"
exam: SAP-C02
exam_domains: ["3. 기존 솔루션 개선"]
status: complete
priority: high
aliases: ["Inspector"]
tags: [aws, sap-c02, security, vulnerability]
created: 2026-05-26
updated: 2026-05-26
---

# Amazon Inspector

> [!summary] 한 줄 요약
> EC2, 컨테이너 이미지, Lambda 함수 등의 소프트웨어 취약점과 네트워크 노출을 자동 평가하는 취약점 관리 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | vulnerability management, CVE, EC2, ECR, Lambda, package scanning |
| 핵심 의사결정 | 워크로드의 CVE/패키지 취약점과 노출 평가가 필요하면 Inspector를 선택한다. |
| 대표 키워드 | vulnerability, CVE, ECR image scan, EC2, Lambda, exposure, SBOM |
| 자주 비교되는 서비스 | [[Amazon GuardDuty]], [[AWS Security Hub]], [[Amazon Macie]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: Amazon Inspector의 시험 역할은 vulnerability management, CVE, EC2, ECR, Lambda, package scanning 요구를 해결하는 것이다.
- **왜 쓰는가?**: EC2, 컨테이너 이미지, Lambda 함수 등의 소프트웨어 취약점과 네트워크 노출을 자동 평가하는 취약점 관리 서비스다.
- **관리형 여부**: 서비스 자체는 AWS 관리형이지만 정책, 범위, 예외 처리, 운영 프로세스 설계는 사용자 책임이다.
- **범위/적용 위치**: 대부분 계정/리전/조직 범위 요구를 지문에서 확인해야 한다.
- **핵심 제약/한계**: 비슷한 보안 서비스와 역할이 겹쳐 보여도 탐지·예방·조사·거버넌스 중 목적을 먼저 구분해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Continuous scanning | 지원 리소스 자동 스캔 | 취약점 지속 평가 |
| CVE findings | 패키지/라이브러리 취약점 매핑 | 패치 우선순위 |
| ECR image scanning | 컨테이너 이미지 취약점 | CI/CD와 런타임 이미지 보안 |
| Lambda/EC2 coverage | 서버/서버리스 코드 패키지 평가 | 워크로드 범위 확인 |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Inspector]] | 취약점 평가 | CVE/패키지/이미지 스캔 | 공격 행위 탐지가 아님 |
| [[Amazon GuardDuty]] | 위협 탐지 | 침해/악성 활동 | 패치 대상 CVE 목록 제공 목적 아님 |
| [[AWS Security Hub]] | finding 집계/표준 | 여러 소스 통합 | 스캐너 자체는 아님 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-security-detection-response-map.png]]

- 그림은 이 서비스가 속한 보안 의사결정 영역을 보여준다.
- 시험에서는 개별 기능보다 **identity / encryption / detection / network protection / governance** 중 어느 문제인지 먼저 분류한다.

## 5. SAP-C02 시나리오 패턴

### 패턴 1: 컨테이너 이미지 취약점

- **요구사항**: ECR 이미지의 CVE 지속 스캔
- **정답 단서**: vulnerability, ECR, CVE
- **선택할 구성**: Amazon Inspector
- **오답 함정**: GuardDuty로 이미지 스캔

## 6. 헷갈리는 포인트

> [!warning] 주의
> 보안/거버넌스 문제는 서비스 이름보다 **보호 대상, 통제 위치, 조직 범위, 자동화 수준, 감사 증거** 단서를 먼저 읽어야 한다.

- Inspector는 취약점 관리, GuardDuty는 위협 탐지다.
- Security Hub로 findings를 모을 수 있지만 Inspector의 스캔 기능을 대체하지 않는다.

## 7. 암기 문장

- CVE/취약점 스캔은 Inspector다.
- 공격 정황 탐지는 GuardDuty와 구분한다.

## 참고 링크

- [What is Amazon Inspector?](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
