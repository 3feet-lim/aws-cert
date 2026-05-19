# AWS 그림 보관 규칙

이 폴더는 Obsidian 노트에서 사용하는 AWS 관련 그림 보관 위치입니다.

## 기본 원칙

- 그림은 **PNG**로 보관합니다. Obsidian에서 바로 보이게 하는 것이 우선입니다.
- draw.io 스타일은 “파일 형식”이 아니라 “박스·화살표 기반의 선형 아키텍처 스타일”을 뜻합니다.
- `.drawio` 원본은 기본 산출물이 아닙니다. 필요할 때만 별도로 만들고, 노트에는 항상 PNG를 임베드합니다.
- 그림 생성/수정 시 프로젝트 스킬 `aws-exam-diagram-style-system`을 기준으로 합니다.
- 최종 PNG는 가능한 경우 최신 OpenAI 이미지 생성 모델을 사용합니다. 현재 기본값은 `gpt-image-2`입니다.
- 그림 안의 설명은 한국어 기반으로 작성하되, AWS 서비스명이나 자연스러운 기술 용어는 영어를 그대로 사용해도 됩니다.
- 모든 서비스에 그림을 강제하지 않습니다. 트래픽 흐름, 신뢰 경계, HA/DR, 마이그레이션, 연동 구조가 시험 이해에 도움이 될 때만 추가합니다.
- 아키텍처가 필요 없는 서비스는 비교표, 결정트리, 정책 평가 흐름, 라이프사이클 등 개념 정리에 도움이 되는 PNG를 사용합니다.

권장 파일명:

```text
서비스명-architecture.png
서비스명-flow.png
서비스명-comparison.png
서비스명-decision-tree.png
```

예시:

```text
amazon-vpc-architecture.png
aws-iam-policy-flow.png
amazon-s3-storage-class-comparison.png
amazon-ecs-vs-eks-decision-tree.png
```

노트에서는 다음처럼 링크합니다:

```markdown
![[attachments/aws/amazon-vpc-architecture.png]]
```

## 스타일

- 흰 배경, 평면 구조, 직사각형 그룹, 직각 연결선을 사용합니다.
- 선은 라벨이나 박스를 관통하지 않게 배치합니다.
- VPC 기반 아키텍처는 위에서 아래로 인터넷/엣지 → 퍼블릭 서브넷 → 프라이빗 애플리케이션 → 데이터/스토리지 계층 순서를 우선합니다.
- 색상은 최소화하고 일관되게 사용합니다.
  - VPC 경계: 초록
  - 퍼블릭 서브넷: 연한 초록
  - 프라이빗 애플리케이션 계층: 연한 파랑
  - 데이터베이스 계층: 옅은 파랑
  - 관리형 AWS 서비스: 보라
  - 보안/주의 콜아웃: 빨강
- SAP-C02 암기에 도움이 되는 라벨만 남깁니다.
  - 예: 멀티 AZ, 교차 리전 복제, PrivateLink, NAT 경로, SCP 적용 범위, 신뢰 경계
