---
type: aws-service
service_name: "AWS Lambda"
category: "03-Computing/Serverless"
exam: SAP-C02
exam_domains:
  - "2. 신규 솔루션"
  - "3. 기존 솔루션 개선"
status: draft
priority: high
aliases:
  - Lambda
tags:
  - aws
  - sap-c02
  - compute
  - serverless
created: 2026-05-20
updated: 2026-05-20
---

# AWS Lambda

> [!summary] 한 줄 요약
> AWS Lambda는 서버를 프로비저닝하지 않고 이벤트에 반응해 코드를 실행하는 함수형 서버리스 컴퓨팅 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 이벤트 기반 아키텍처, 서버리스 API/파일 처리/스트림 처리, 운영 부담 최소화, 비용 최적화 |
| 핵심 의사결정 | 짧고 이벤트 기반이며 상태를 외부화할 수 있는 작업인가 |
| 대표 키워드 | event-driven, serverless, S3 event, API Gateway, DynamoDB Streams, short duration, pay per invocation |
| 자주 비교되는 서비스 | [[AWS Fargate]], [[Amazon EC2]], [[AWS Step Functions]], [[Amazon ECS]] |
| 암기 우선순위 | High |

## 1. 핵심 개념

- **무엇인가?**: 이벤트 소스가 함수를 호출하면 AWS가 실행 환경을 준비하고 코드를 실행하는 서버리스 컴퓨팅 서비스.
- **왜 쓰는가?**: 서버 운영 없이 이벤트 처리, API 백엔드, 자동화, 스트림/파일 처리, 비동기 작업을 구현하기 위해 사용한다.
- **관리형/비관리형 여부**: 인프라와 스케일링은 AWS가 관리하지만, 함수 코드, IAM 권한, 타임아웃/메모리, 재시도/오류 처리는 사용자가 설계한다.
- **리전/글로벌 서비스 여부**: 리전 서비스. Lambda@Edge/CloudFront Functions와는 용도와 위치가 다르다.
- **핵심 제약/한계**: 실행 시간 제한, 패키지/임시 저장소/동시성/콜드 스타트, VPC 연결 지연, 상태 저장 부적합성을 고려한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Event source | S3, API Gateway, EventBridge, SQS, DynamoDB Streams 등 | 이벤트 기반/느슨한 결합 요구에서 자주 정답이 된다. |
| Execution role | 함수가 AWS 서비스에 접근할 때 쓰는 IAM 역할 | 최소 권한과 cross-service access가 핵심이다. |
| Concurrency | 동시에 실행 가능한 함수 수 | 폭주 보호, 예약 동시성, 제한과 throttling을 이해해야 한다. |
| Async retry/DLQ/destination | 비동기 호출 실패 처리 | 재시도와 실패 이벤트 보관 설계가 시험 포인트다. |
| VPC access | Lambda를 VPC 리소스에 연결 | RDS/ElastiCache private 접근에는 필요하지만 NAT/endpoint 설계를 고려한다. |
| Layers/container image | 공통 라이브러리/컨테이너 패키징 | 배포 패키지 관리와 런타임 의존성에 유용하다. |
| Provisioned concurrency | 콜드 스타트 완화 | 지연시간 민감 API에서 비용과 함께 고려한다. |

## 3. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[AWS Lambda]] vs [[AWS Fargate]] | Lambda는 함수/이벤트, Fargate는 서버리스 컨테이너 태스크 | 짧은 이벤트 처리와 호출 기반 과금은 Lambda | 장기 실행 프로세스나 세밀한 CPU/메모리 컨테이너 제어는 Fargate가 낫다. |
| [[AWS Lambda]] vs [[Amazon EC2]] | Lambda는 서버 운영 없음, EC2는 OS/서버 제어 | 운영 부담 최소화와 자동 확장이 우선이면 Lambda | 커스텀 OS/에이전트/장기 실행은 EC2가 적합하다. |
| [[AWS Lambda]] vs [[AWS Step Functions]] | Lambda는 실행 단위, Step Functions는 워크플로 오케스트레이션 | 여러 단계/재시도/분기/상태 관리가 핵심이면 Step Functions와 함께 사용 | Lambda 안에 긴 워크플로를 직접 구현하면 관찰성과 재시도 제어가 나빠진다. |
| [[AWS Lambda]] vs [[CloudFront Functions]] | Lambda는 일반 서버리스, CloudFront Functions는 초경량 edge JavaScript | 복잡한 백엔드 처리는 Lambda, viewer request의 초간단 조작은 CloudFront Functions | Edge 위치/제한이 다르다. |

## 4. 설계 시 고려사항

- 함수는 stateless로 만들고 상태는 DynamoDB, S3, RDS, ElastiCache, Step Functions 등에 외부화한다.
- SQS를 이벤트 소스로 두면 burst를 완충하고 DLQ를 통해 실패 메시지를 보관할 수 있다.
- VPC Lambda가 인터넷이나 AWS public endpoint에 나가야 하면 NAT Gateway 또는 VPC endpoint 설계가 필요하다.
- 지연시간 민감 워크로드는 콜드 스타트, 패키지 크기, 런타임, provisioned concurrency를 고려한다.

## 5. 비용 / 운영 포인트

- 요청 수와 실행 시간/메모리 기반 과금이므로 간헐적·버스티 워크로드에 유리하다.
- 매우 높은 지속 트래픽이나 장기 실행 컨테이너는 Fargate/EC2가 비용상 유리할 수 있다.
- CloudWatch Logs, X-Ray, Lambda Insights로 모니터링하며 오류율, duration, throttles, iterator age를 확인한다.

## 6. SAP-C02 시나리오 패턴

### 패턴 1: S3 업로드 후 이미지 처리

- **요구사항**: 파일이 올라오면 자동으로 썸네일 생성.
- **정답 단서**: event-driven, no server management, S3 object created.
- **선택할 구성**: S3 event notification → Lambda → S3/DynamoDB.
- **오답 함정**: 항상 켜진 EC2 워커는 간헐적 이벤트에 비용/운영 부담이 크다.

### 패턴 2: API Gateway 백엔드

- **요구사항**: 트래픽 변동이 큰 API, 서버 운영 최소화.
- **정답 단서**: serverless REST/HTTP API, bursty traffic.
- **선택할 구성**: API Gateway + Lambda + DynamoDB/RDS Proxy.
- **오답 함정**: DB 연결 폭증은 RDS Proxy나 연결 관리 없이 Lambda만으로 해결되지 않는다.

## 7. 헷갈리는 포인트

> [!warning] 주의
> Lambda는 자동 확장되지만 무한 확장은 아니다. 동시성 한도, downstream 보호, 재시도 폭주를 설계해야 한다.

- Lambda 함수 내부 로컬 디스크/메모리에 영구 상태를 두면 안 된다.
- 비동기 이벤트는 실패 시 재시도될 수 있으므로 idempotency가 중요하다.
- Lambda가 VPC 안에 있다고 해서 자동으로 인터넷 접근이 되는 것은 아니다.
- 15분을 넘는 실행이나 지속 서버 프로세스는 다른 컴퓨팅 서비스를 검토한다.

## 8. 암기 문장

- 이벤트 기반 짧은 작업 + 서버 운영 제거 = Lambda.
- 긴 컨테이너/상시 프로세스는 Fargate, OS 제어는 EC2, 여러 단계 상태 관리는 Step Functions와 비교한다.

## 9. 참고 링크

- [How Lambda works](https://docs.aws.amazon.com/lambda/latest/dg/concepts-basics.html)
- [AWS Lambda function scaling](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html)
- [Invoking Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation.html)
- [AWS Fargate or AWS Lambda?](https://docs.aws.amazon.com/decision-guides/latest/fargate-or-lambda/fargate-or-lambda.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
