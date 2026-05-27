---
type: aws-service
service_name: "Amazon Elastic Transcoder"
category: "Media"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Elastic Transcoder"]
tags: [aws, sap-c02, media, transcoding]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Elastic Transcoder

> [!summary] 한 줄 요약
> S3에 있는 미디어 파일을 다양한 포맷/해상도로 변환하는 관리형 파일 기반 트랜스코딩 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | media transcoding, S3 pipeline, legacy/simple transcoding |
| 대표 키워드 | Elastic Transcoder, media, transcoding |
| 자주 비교되는 서비스 | [[Amazon Kinesis Video Streams]], [[AWS Lambda]], [[Amazon S3]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: S3 입력 파일을 파이프라인/잡으로 처리해 출력 파일을 생성한다.
- **왜 쓰는가?**: 간단한 미디어 변환과 배포 준비에 사용한다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 최신 미디어 워크로드는 AWS Elemental MediaConvert 등 대안과 비교해야 한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Pipeline/Job | 입력/출력 버킷과 변환 작업 | 미디어 처리 |
| Presets | 포맷/해상도 설정 | 다중 디바이스 지원 |
| S3/CloudFront | 저장과 배포 | 미디어 전달 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-media-selection-map.png]]

이 그림은 18. Media 영역에서 `Amazon Elastic Transcoder`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Kinesis Video Streams]] | 비디오 스트림 수집 | 라이브/IoT 비디오 | 파일 변환 아님 |
| [[AWS Lambda]] | 이벤트 처리 | 간단 처리 자동화 | 전문 트랜스코딩 아님 |
| [[Amazon S3]] | 객체 저장 | 원본/결과 저장 | 변환 엔진 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Elastic Transcoder는 `파일 기반 미디어 변환` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 최신 미디어 워크로드는 AWS Elemental MediaConvert 등 대안과 비교해야 한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Elastic Transcoder`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| media transcoding, S3 pipeline, legacy/simple transcoding | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Elastic Transcoder]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `파일 기반 미디어 변환`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- S3 파일을 다른 미디어 포맷으로 변환하면 Elastic Transcoder 계열이다.
- 라이브 비디오 수집은 Kinesis Video Streams다.

## 참고 링크

- [Amazon Elastic Transcoder 공식 문서](https://docs.aws.amazon.com/elastictranscoder/latest/developerguide/introduction.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
