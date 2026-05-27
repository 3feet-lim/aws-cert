---
type: aws-service
service_name: "Amazon Polly"
category: "Machine Learning"
exam: SAP-C02
exam_domains: ["2. 신규 솔루션", "3. 기존 솔루션 개선"]
status: complete
priority: low
aliases: ["Polly"]
tags: [aws, sap-c02, text-to-speech]
created: 2026-05-27
updated: 2026-05-27
---

# Amazon Polly

> [!summary] 한 줄 요약
> 텍스트를 자연스러운 음성으로 변환하는 관리형 TTS 서비스다.

## 0. SAP-C02 시험 포커스

| 항목 | 정리 |
|---|---|
| 출제 관점 | 2. 신규 솔루션, 3. 기존 솔루션 개선 |
| 핵심 의사결정 | text to speech, neural voices, SSML |
| 대표 키워드 | Polly, text-to-speech |
| 자주 비교되는 서비스 | [[Amazon Transcribe]], [[Amazon Lex]], [[Amazon Translate]] |
| 암기 우선순위 | Low |

## 1. 핵심 개념

- **무엇인가?**: 텍스트/SSML 입력을 음성 파일이나 스트림으로 변환한다.
- **왜 쓰는가?**: 음성 안내, 접근성, 콘텐츠 내레이션에 적합하다.
- **관리형 여부**: AWS 관리형 서비스. 사용자는 데이터 모델, 권한, 통합 방식, 비용/운영 정책을 설계한다.
- **리전/글로벌**: 대부분 리전 단위로 설계하며, 글로벌 사용자 경험은 CloudFront/Route 53/멀티 리전 패턴과 조합한다.
- **핵심 제약/한계**: 음성을 텍스트로 바꾸는 것은 Transcribe다.

## 2. 주요 기능과 시험 포인트

| 기능/개념 | 설명 | SAP-C02 포인트 |
|---|---|---|
| Neural voices | 고품질 음성 | 사용자 경험 |
| SSML | 발음/속도/강세 제어 | 세밀한 TTS |
| Speech marks | 입모양/하이라이트 동기화 | 앱 연동 |

## 3. 아키텍처 / 선택 맵

![[attachments/aws/aws-machine-learning-selection-map.png]]

이 그림은 13. Machine Learning 영역에서 `Amazon Polly`가 어떤 위치의 정답 후보인지 빠르게 구분하기 위한 맵이다. 시험에서는 서비스 이름보다 **문제의 요구사항이 데이터 수집/처리/보안/운영 중 무엇인지**를 먼저 본다.

## 4. 비교 / 선택 기준

| 비교 대상 | 차이점 | 선택 기준 | 오답 함정 |
|---|---|---|---|
| [[Amazon Transcribe]] | 음성→텍스트 | 전사 | 방향 반대 |
| [[Amazon Lex]] | 대화형 봇 | 대화 흐름 | TTS 단독 아님 |
| [[Amazon Translate]] | 번역 | 언어 변환 | 음성 합성 아님 |

## 5. 헷갈리는 포인트 / 오답 함정

> [!warning] 주의
> Amazon Polly는 `텍스트→음성` 역할로 기억한다. 이름이 비슷한 서비스라도 데이터 흐름의 위치가 다르면 정답이 달라진다.

- 음성을 텍스트로 바꾸는 것은 Transcribe다.
- 요구사항이 단순 전송/저장/시각화/보안인지, 아니면 직접 처리·운영이 필요한지 구분한다.
- 여러 서비스가 함께 등장하면 `Amazon Polly`가 전체 아키텍처에서 담당하는 책임만 좁혀서 판단한다.

## 6. SAP-C02 시나리오 패턴

| 문제 상황 | 정답 단서 | 선택할 구성 |
|---|---|---|
| text to speech, neural voices, SSML | 운영 부담 감소, 확장성, AWS 관리형 통합 | [[Amazon Polly]] 중심 구성 |
| 유사 서비스가 함께 제시됨 | 데이터 흐름상 `텍스트→음성`가 핵심 | 비교표의 선택 기준으로 소거 |

## 7. 암기 문장

- Text-to-speech는 Polly다.
- 음성 기반 봇은 Lex와 Polly/Transcribe 조합으로 이해한다.

## 참고 링크

- [Amazon Polly 공식 문서](https://docs.aws.amazon.com/polly/latest/dg/what-is.html)
- [SAP-C02 Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/solutions-architect-professional-02/solutions-architect-professional-02.html)
