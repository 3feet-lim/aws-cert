# Error log note format

Use this structure for each `error_log/` Markdown note. Omit fields only when they are truly irrelevant.

```markdown
---
type: aws-exam-error-log
exam: SAP-C02
created: YYYY-MM-DD
updated: YYYY-MM-DD
question_source: "미제공"
services: ["Amazon S3", "AWS KMS"]
related_notes: ["[[Amazon S3]]", "[[AWS KMS]]"]
tags: [aws, sap-c02, error-log]
---

# {{짧은 문제 주제}}

> [!summary] 오답 요약
> {{한 문장으로 내가 놓친 판단 기준을 정리}}

## 1. 문제 상황 요약

- **시나리오**: {{상황을 저작권 문제 없이 요약}}
- **핵심 요구사항**: {{가용성/보안/비용/마이그레이션 등}}
- **제약 조건**: {{시간, 운영 부담, 계정 구조, 리전, 온프레미스 등}}
- **관련 서비스**: [[{{Service}}]], [[{{Distractor}}]]

## 2. 정답과 오답

| 구분 | 선택지/서비스 | 판단 |
|---|---|---|
| 정답 | {{correct answer}} | {{요구사항을 만족하는 이유}} |
| 내가 고른 답 | {{wrong answer or 미제공}} | {{틀린 이유}} |
| 주요 오답 함정 | {{distractor}} | {{왜 매력적이지만 틀렸는지}} |

## 3. 왜 정답인가

- {{정답 선택의 결정적 단서}}
- {{관련 AWS 기능/제약}}
- {{비교 서비스와의 경계}}

## 4. 다시 풀 때의 판단 규칙

- **키워드**: {{문제에서 봐야 할 표현}}
- **바로 떠올릴 서비스**: [[{{Service}}]]
- **버릴 선택지**: {{조건이 맞지 않는 서비스와 이유}}
- **암기 문장**: {{한 문장}}

## 5. 서비스 노트 보강 여부

- [ ] 관련 서비스 노트가 존재한다.
- [ ] 정답 개념이 서비스 노트에 있다.
- [ ] 오답 비교/함정이 서비스 노트에 있다.
- [ ] 필요 시 서비스 노트를 업데이트했다.

## 6. 참고 링크

- [AWS 공식 문서]({{url}})
```

Keep the final note concise: one screen to a few screens is usually enough. Add a short `복습 질문` section only when it helps memory.
