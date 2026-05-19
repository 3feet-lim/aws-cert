# AWS 그림 보관 규칙

이 폴더는 Obsidian 노트에서 사용하는 AWS 관련 그림 보관 위치입니다.

## 기본 원칙

- 그림 원본은 **draw.io / diagrams.net** 형식으로 보관합니다.
- 노트에는 draw.io에서 export한 PNG를 임베드합니다.
- 모든 서비스에 그림을 강제하지 않습니다. 트래픽 흐름, 신뢰 경계, HA/DR, 마이그레이션, 연동 구조가 시험 이해에 도움이 될 때만 추가합니다.

권장 파일명:

```text
서비스명-architecture.drawio
서비스명-architecture.png
서비스명-flow.drawio
서비스명-flow.png
서비스명-comparison.drawio
서비스명-comparison.png
```

예시:

```text
amazon-vpc-architecture.drawio
amazon-vpc-architecture.png
aws-iam-policy-flow.drawio
aws-iam-policy-flow.png
amazon-s3-storage-class-comparison.drawio
amazon-s3-storage-class-comparison.png
```

노트에서는 다음처럼 링크합니다:

```markdown
![[attachments/aws/amazon-vpc-architecture.png]]
```

## 스타일

- AWS 공식 아이콘을 우선 사용합니다.
- 기본 흐름은 좌→우로 배치합니다.
- 계정, 리전, AZ, VPC, 서브넷, 온프레미스 같은 경계는 컨테이너 박스로 표현합니다.
- 색상은 최소화합니다.
  - 파랑: AWS 관리형 서비스 / 컨트롤 플레인
  - 초록: VPC 내부 / 프라이빗 데이터 경로
  - 주황: 인터넷, 엣지, 외부 사용자
  - 빨강: 장애, 위험, 오답 함정, 주의 콜아웃
- SAP-C02 암기에 도움이 되는 라벨만 남깁니다.
  - 예: Multi-AZ, Cross-Region replication, PrivateLink, NAT 경로, SCP 적용 범위, trust boundary
