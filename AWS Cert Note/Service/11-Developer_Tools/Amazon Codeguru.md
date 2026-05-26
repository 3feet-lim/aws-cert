---
title: Amazon CodeGuru
category: 11. Developer Tools
service: Amazon CodeGuru
status: complete
created: 2026-05-27
updated: 2026-05-27
tags:
  - aws
  - sap-c02
  - developer-tools
  - code-review
  - profiler
  - codeguru
---

# Amazon CodeGuru

> [!summary]
> **Amazon CodeGuru**는 코드 품질/보안 권고(CodeGuru Reviewer)와 런타임 성능 병목 분석(CodeGuru Profiler)을 제공하는 개발자 도구 계열 서비스다. 단, Reviewer의 신규 repository 연결 제한 등 수명주기 변화가 있으므로 신규 아키텍처에서는 Amazon Q Developer와 대체 코드 분석 옵션을 함께 검토해야 한다.

## 0. SAP-C02 시험 포커스

| 출제 포인트 | 핵심 판단 |
| --- | --- |
| 코드 리뷰 권고 | CodeGuru Reviewer는 정적 분석 기반 코드 품질/보안 권고 |
| 성능 병목 분석 | CodeGuru Profiler는 production runtime의 CPU/latency/cost hotspot 분석 |
| CI/CD 피드백 | CodePipeline/CodeBuild 이후 품질 피드백 루프와 연결 가능 |
| X-Ray와 구분 | X-Ray는 분산 요청 추적, CodeGuru Profiler는 코드 실행 hotspot |
| Lifecycle 주의 | 신규 도입 시 Reviewer 지원 정책과 Amazon Q Developer 대안을 확인 |

## 1. 핵심 개념

- **CodeGuru Reviewer**: 저장소 또는 pull request의 코드를 분석해 결함, 보안 위험, 모범 사례 위반을 권고한다.
- **CodeGuru Profiler**: 실행 중인 애플리케이션의 runtime profile을 수집해 CPU 사용, latency, 비용 hotspot을 찾는다.
- **Profiling group**: Profiler가 애플리케이션 프로파일 데이터를 묶어 분석하는 단위.
- **Recommendation**: 분석 결과로 생성되는 개선 권고.

## 2. 주요 기능과 시험 포인트

### CodeGuru Reviewer

Reviewer는 코드 변경에 대한 정적 분석 권고를 제공한다. 다만 AWS 서비스 수명주기 변화로 신규 repository 연결 제한이 있으므로, 실제 설계에서는 공식 공지와 Amazon Q Developer 기반 코드 리뷰/보안 분석 대안을 확인해야 한다.

### CodeGuru Profiler

Profiler는 production 또는 staging 애플리케이션의 실행 프로파일을 수집해 CPU를 많이 쓰는 메서드, latency 병목, 비효율적인 코드 경로를 찾는다. 비용 최적화와 성능 개선 시나리오에 연결된다.

### 관측성 도구와의 관계

- X-Ray: 요청이 어떤 서비스들을 거쳐 지연되는지 추적.
- CloudWatch: 메트릭/로그/알람.
- CodeGuru Profiler: 코드 내부의 실행 비용과 hotspot.

## 3. 비교 / 선택 기준

| 요구사항 | 선택 | 이유 |
| --- | --- | --- |
| Pull request 코드 품질 권고 | CodeGuru Reviewer 또는 Amazon Q Developer | 정적 분석/AI 기반 리뷰. 신규 도입은 지원 정책 확인 |
| 런타임 CPU/latency hotspot | CodeGuru Profiler | production profile 기반 분석 |
| 분산 호출 경로 병목 | X-Ray | 서비스 간 trace 분석 |
| 로그 기반 오류 조사 | CloudWatch Logs | 로그 검색과 보관 |
| CI/CD 단계 조정 | CodePipeline | 분석 도구 호출 흐름 구성 |

## 4. 아키텍처 / 동작 흐름

![[attachments/aws/aws-developer-tools-supporting-services.png]]

1. 개발자가 코드 변경을 생성한다.
2. Reviewer 또는 대체 코드 분석 도구가 결함/보안/품질 권고를 제공한다.
3. 애플리케이션이 실행되면 Profiler agent가 runtime profile을 수집한다.
4. Profiler가 CPU/latency/cost hotspot을 분석한다.
5. 개선 사항은 CodePipeline/CodeBuild를 통해 다시 배포되고 CloudWatch/X-Ray로 검증한다.

## 5. SAP-C02 시나리오 패턴

- “코드 변경의 잠재 결함과 보안 이슈를 자동 권고받고 싶다” → CodeGuru Reviewer 개념 또는 Amazon Q Developer 대안 검토.
- “운영 Java/Python 애플리케이션에서 비용이 높은 코드 경로를 찾아야 한다” → CodeGuru Profiler.
- “서비스 간 호출 중 어느 서비스가 느린지 알고 싶다” → X-Ray.
- “CPU가 높은데 어떤 메서드가 원인인지 알고 싶다” → CodeGuru Profiler.

## 6. 헷갈리는 포인트

- CodeGuru Profiler는 분산 trace 도구가 아니다. 요청 흐름 전체는 X-Ray가 더 적합하다.
- CodeGuru Reviewer는 빌드/배포 서비스가 아니다. CI/CD 흐름은 CodePipeline/CodeBuild와 조합한다.
- 신규 설계에서 CodeGuru Reviewer를 답으로 고를 때는 서비스 지원 정책과 Amazon Q Developer 대안을 함께 고려해야 한다.

## 7. 암기 문장

> **CodeGuru Reviewer는 코드 권고, CodeGuru Profiler는 런타임 hotspot, X-Ray는 분산 trace.**

## 8. 참고 링크

- [Amazon CodeGuru Reviewer User Guide](https://docs.aws.amazon.com/codeguru/latest/reviewer-ug/welcome.html)
- [What is Amazon CodeGuru Profiler?](https://docs.aws.amazon.com/codeguru/latest/profiler-ug/what-is-codeguru-profiler.html)
- [Amazon Q Developer](https://aws.amazon.com/q/developer/)
- [SAP-C02 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-professional/)
