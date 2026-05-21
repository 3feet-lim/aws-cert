---
type: aws-service
service_name: "Amazon Lightsail"
category: "03-Computing/Virtual Machine"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
status: draft
priority: low
aliases:
  - Lightsail
tags:
  - aws
  - sap-c02
  - compute
  - vps
created: 2026-05-20
updated: 2026-05-20
---

# Amazon Lightsail

> [!summary] 한 줄 요약
> Amazon Lightsail은 소규모 웹사이트와 웹 애플리케이션을 예측 가능한 월 비용으로 빠르게 시작하기 위한 단순화된 VPS형 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 단순 웹사이트/소규모 앱, 빠른 시작, 예측 가능한 비용 |
| 핵심 의사결정 | 엔터프라이즈급 세밀 제어보다 단순성과 고정 월비용이 중요한가 |
| 대표 키워드 | simple VPS, website, WordPress, predictable monthly price, small business |
| 자주 비교되는 서비스 | [[Amazon EC2]], [[AWS Elastic Beanstalk]], [[AWS App Runner]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 인스턴스, 스토리지, 네트워킹, DNS, 로드 밸런서, 데이터베이스 등을 단순 UI와 번들 가격으로 제공하는 서비스.
- **왜 쓰는가?**: AWS 경험이 적거나 소규모 웹서비스를 빠르게 시작해야 할 때 운영 복잡도를 낮추기 위해 사용한다.
- **관리형/비관리형 여부**: Lightsail이 단순화된 관리 경험을 제공하지만, 인스턴스 내부 OS/애플리케이션 관리는 여전히 사용자 책임이다.
- **리전/글로벌 서비스 여부**: 리전 기반 리소스다.
- **핵심 제약/한계**: 복잡한 VPC 아키텍처, 세밀한 오토스케일링, 대규모 엔터프라이즈 통합에는 일반 EC2/VPC 서비스가 적합하다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Lightsail instance | 사전 구성된 VPS | WordPress/소규모 웹앱 빠른 시작에 적합하다. |
| Bundled pricing | 월 단위 예측 가능한 가격 | 비용 예측성이 키워드일 때 등장할 수 있다. |
| Managed database | 단순 데이터베이스 옵션 | 복잡한 RDS 기능/HA가 필요하면 RDS를 검토한다. |
| Load balancer/CDN/DNS | 단순 웹 운영 구성요소 | 엔터프라이즈급 세부 제어보다 빠른 구성이 목적이다. |
| Snapshot | 백업/복구 | DR 자동화나 복잡한 백업 정책은 별도 설계가 필요하다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Lightsail]] vs [[Amazon EC2]] | Lightsail은 단순 패키지, EC2는 세밀 제어 | 소규모 웹사이트·고정 비용·쉬운 관리면 Lightsail | 복잡한 Auto Scaling/VPC/보안 요구에는 EC2가 적합하다. |
| [[Amazon Lightsail]] vs [[AWS Elastic Beanstalk]] | Beanstalk는 앱 플랫폼 배포/스케일 관리, Lightsail은 VPS 중심 | 코드 배포 플랫폼보다 서버 패키지가 필요하면 Lightsail | Beanstalk는 내부적으로 EC2/ALB/ASG를 구성할 수 있다. |
| [[Amazon Lightsail]] vs [[AWS App Runner]] | App Runner는 소스/컨테이너에서 웹서비스 직접 배포 | 컨테이너/소스 기반 관리형 웹서비스면 App Runner | OS-level 서버 접근이 필요하면 Lightsail/EC2가 더 자연스럽다. |

## 4. 언제 사용하는가

- WordPress, 블로그, 소규모 회사 웹사이트, 개발/테스트 서버처럼 단순성과 비용 예측성이 중요한 경우.
- AWS 세부 서비스 학습 없이 빠르게 웹 리소스를 만들고 싶을 때.

## 5. 언제 사용하지 않는가

- 복잡한 네트워크 분리, 멀티 AZ 자동 확장, 세밀한 보안/관찰성/배포 파이프라인이 필요한 엔터프라이즈 워크로드.
- 대규모 트래픽과 서비스별 최적화가 중요한 경우에는 EC2/ECS/Fargate/App Runner/Elastic Beanstalk를 검토한다.

## 6. 헷갈리는 포인트

> [!warning] 주의
> Lightsail은 “쉬운 AWS 시작점”이지 모든 EC2 아키텍처의 대체재가 아니다.

- 단순한 월 비용은 장점이지만, 고급 AWS 서비스 조합이 필요한 문제에서는 오답일 수 있다.
- OS와 애플리케이션 관리는 완전 서버리스처럼 사라지지 않는다.
- SAP-C02에서는 출제 빈도가 높지 않으며, 단순성/소규모/예측 가격 단서가 중요하다.

## 7. 암기 문장

- 작은 웹사이트를 빠르게, 싸고, 단순하게 시작하면 Lightsail이다.
- 엔터프라이즈 HA/Auto Scaling/복잡한 VPC 요구가 보이면 EC2 계열 아키텍처로 넘어간다.

## 8. 참고 링크

- [What is Amazon Lightsail?](https://docs.aws.amazon.com/lightsail/latest/userguide/what-is-amazon-lightsail.html)
- [Lightsail FAQ](https://docs.aws.amazon.com/lightsail/latest/userguide/amazon-lightsail-frequently-asked-questions-faq-general.html)
- [Amazon Lightsail, AWS Elastic Beanstalk, or Amazon EC2?](https://docs.aws.amazon.com/decision-guides/latest/lightsail-elastic-beanstalk-ec2/lightsail-elastic-beanstalk-ec2.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
