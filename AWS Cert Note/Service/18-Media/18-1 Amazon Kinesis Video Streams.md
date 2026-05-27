---
type: aws-service
service_name: "Amazon Kinesis Video Streams"
category: "Media"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: medium
aliases: ["KVS"]
tags: [aws, sap-c02, media, video, streaming]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Kinesis Video Streams

> [!summary] 한 줄 요약
> 카메라/디바이스의 비디오 스트림을 AWS로 안전하게 수집·저장·처리하는 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | video stream ingest, storage, real-time processing, WebRTC |
| 대표 키워드 | KVS, media, video, streaming |
| 자주 비교되는 서비스 | [[Amazon Elastic Transcoder]], [[Amazon Kinesis Data Streams]], [[Amazon Rekognition]] |
| 암기 우선순위 | Medium |

## 1. 핵심 개념

- **무엇인가?**: 비디오 producers가 스트림을 전송하고 consumer/ML/재생이 이를 사용한다.
- **왜 쓰는가?**: 라이브 영상 분석, 보안 카메라, IoT 비디오 수집에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 파일 기반 트랜스코딩은 Elastic Transcoder/MediaConvert 계열과 구분한다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Video ingest | 디바이스/카메라 스트림 수집 | 실시간 영상 |
| Storage/replay | 스트림 보존/재생 | 분석/감사 |
| WebRTC | 저지연 양방향 미디어 | 실시간 통신 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-media-selection-map.png]]

이 그림은 18. Media 영역에서 `Amazon Kinesis Video Streams`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Elastic Transcoder]] | 파일 기반 미디어 변환 | S3 입력/출력 | 스트림 수집 아님 |
| [[Amazon Kinesis Data Streams]] | 일반 데이터 스트림 | 레코드 기반 | 비디오 특화 기능 없음 |
| [[Amazon Rekognition]] | 비디오/이미지 분석 | ML 분석 | 스트림 수집 저장 자체는 KVS |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Kinesis Video Streams는 `비디오 스트림 수집/처리` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 파일 기반 트랜스코딩은 Elastic Transcoder/MediaConvert 계열과 구분한다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Kinesis Video Streams`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| video stream ingest, storage, real-time processing, WebRTC | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Kinesis Video Streams]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `비디오 스트림 수집/처리`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- 라이브/IoT 비디오 스트림 수집은 Kinesis Video Streams다.
- 파일 변환 서비스와 스트림 수집 서비스를 구분한다.

## 참고 링크

- [Amazon Kinesis Video Streams 공식 문서](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/what-is-kinesis-video.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
