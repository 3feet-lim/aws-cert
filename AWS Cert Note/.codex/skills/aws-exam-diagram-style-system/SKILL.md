---
name: aws-exam-diagram-style-system
description: Generates AWS architecture and concept diagrams in a consistent SAP-C02 study-note style. Use when creating PNG diagrams for AWS notes, architecture flows, network/security boundaries, service comparisons, or exam-oriented visual explanations. Diagrams should be Korean-first, while natural AWS/service/technical terms may remain in English when clearer.
---

# AWS Exam Diagram Style System

## Purpose

Generate AWS diagrams for SAP-C02 exam preparation, AWS study notes, concept visualization, network flow explanation, architecture comparison, and security boundary explanation.

Prioritize:

1. conceptual correctness
2. AWS architectural best practices
3. educational readability
4. clean draw.io-style layouts
5. visually understandable traffic flow

Artistic styling is not the priority. The final artifact should be a **PNG** suitable for immediate Obsidian embedding.

## Generation model

Use an image generation model for the final PNG whenever this environment provides one.

- Default to the latest OpenAI image generation model, currently `gpt-image-2`.
- Prefer high quality for final diagrams.
- Use a landscape canvas for architecture diagrams unless the service concept is better shown as a vertical flow.
- The prompt must explicitly request:
  - flat AWS reference architecture style
  - clean draw.io-like boxes and arrows
  - readable sans-serif text
  - no decorative or cinematic styling
  - no label overlap
  - no broken connectors
  - Korean-first explanatory text with natural AWS/technical English allowed
- After generation, visually inspect the PNG. If text is unreadable, connectors overlap, or AWS placement rules are wrong, regenerate or revise.

If image generation is unavailable, use a deterministic fallback such as SVG/HTML-to-PNG or a local drawing script, but treat that as a fallback rather than the preferred path.

## Language rule

The diagram should be **Korean-first**, meaning the overall explanation, learning guidance, warnings, and callouts should be understandable to Korean readers.

Do not force awkward Korean translations for common AWS or architecture terms. Use English when it is the natural exam/study term or improves readability.

English is allowed for official AWS service names and common technical labels, such as:

- Application Load Balancer (ALB)
- NAT Gateway
- Amazon S3
- AWS Lambda
- Amazon Aurora
- Public Subnet / Private Subnet
- Outbound Internet Access
- Multi-AZ
- Route Table

Good examples:

- `프라이빗 서브넷`
- `Private Subnet`
- `Outbound Internet Access`
- `멀티 AZ 구성`
- `NAT Gateway: 프라이빗 서브넷의 아웃바운드 통신`

Avoid:

- Korean that sounds unnatural or hides standard AWS terminology
- English-only diagrams with no Korean learning context

## Global visual style

Use:

- flat architecture diagram style
- draw.io-like structure
- AWS reference architecture aesthetics
- clean spacing
- structured grouping
- orthogonal connector lines
- white background
- rectangular layout blocks
- clean sans-serif font

Avoid:

- cinematic rendering
- neon effects
- glassmorphism
- 3D rendering
- dark background
- excessive gradients
- decorative visual noise
- unreadable tiny text
- pixel/bitmap-looking fonts

## Color rules

| Component | Color |
|---|---|
| VPC boundary | Green |
| Public subnet | Light green |
| Private application layer | Light blue |
| Database layer | Pale blue |
| Managed AWS services | Purple |
| Security/warning callouts | Red |
| VPC endpoint/private access | Green or purple |

Use colors consistently and sparingly. The diagram must remain understandable in a study-note context.

## Connector rules

All connectors must:

- remain visually clean
- never overlap unnecessarily
- never appear broken
- clearly indicate direction
- use consistent arrowheads
- use orthogonal routes where possible
- avoid crossing labels or passing through boxes

Availability Zone dashed borders must:

- form complete rectangles
- never break or overlap
- remain aligned vertically

## Common AWS architecture rules

### Internet traffic

Always visualize internet flow clearly:

`사용자 → 인터넷 → CloudFront / IGW / WAF → 로드 밸런서 → 애플리케이션 계층`

The traffic path must be immediately understandable.

### Public vs private subnets

Public subnet means:

- route to Internet Gateway
- internet-facing resources allowed

Private subnet means:

- no direct inbound internet access
- outbound access only through controlled paths

Private resources should visually appear isolated. Use lock icons or red callouts only when they improve exam understanding.

### NAT Gateway rules

NAT Gateway must:

- be placed inside a public subnet
- visually connect to Internet Gateway
- never appear internet-facing to end users

The diagram should communicate clearly, for example:

`프라이빗 서브넷의 Outbound Internet Access용`

Do not describe NAT Gateway as an inbound access component.

### Load balancer rules

Public ALB:

- resides in public subnets
- receives internet traffic

Internal ALB:

- may reside in private subnets

ALB should visually appear as one logical distributed service, not multiple unrelated standalone devices.

### Database rules

Databases should:

- default to private DB subnets
- support Multi-AZ visualization
- never appear publicly exposed unless explicitly required

Preferred visual hierarchy:

`ALB → 웹/애플리케이션 계층 → 데이터베이스 계층`

### VPC endpoint rules

Gateway endpoint:

- visually separate from internet routing
- communicate: `AWS 서비스에 인터넷 없이 접근`

Interface endpoint:

- visually connected using ENI-style endpoint representation
- communicate private access clearly

## Diagram organization rules

For VPC-based architectures, prefer this vertical organization:

Top:

- Internet
- CloudFront
- Route 53
- WAF

Middle:

- Public subnet
- ALB
- NAT Gateway

Lower:

- Private application layer
- ECS/EKS/EC2/Lambda integrations

Bottom:

- Database layer
- Storage layer

Right side:

- AWS managed services
- Amazon S3
- DynamoDB
- EventBridge
- SNS/SQS

## Non-architecture concept diagrams

If a service does not need an architecture diagram, create a concept-helping PNG instead when visual memory helps:

- comparison table image
- decision tree
- policy/evaluation flow
- lifecycle/state diagram
- shared responsibility split
- service selection map

These visuals must follow the same Korean-first, clean-spacing, and readable-font rules.

## Prohibited outputs

Never:

- break dashed AZ borders
- overlap labels
- distort routing lines
- place DB in public subnet unless explicitly required
- place NAT Gateway in private subnet
- use random floating arrows
- overdecorate the image
- use unreadable tiny text
- create infographic posters instead of architecture diagrams
- use English-only explanatory labels when Korean context is needed for study clarity

## Educational goal

Every generated diagram should feel like:

> 프리미엄 AWS SAP-C02 학습 노트

The viewer should understand traffic flow, security boundaries, subnet purpose, routing intent, and service interaction within a few seconds.

## Example architectures

### ECS Fargate architecture

Flow:

`사용자 → CloudFront → WAF → ALB → ECS Service → Aurora`

Include:

- Multi-AZ
- NAT Gateway
- Auto Scaling
- VPC Endpoint
- ECR Pull path

### Serverless architecture

Flow:

`사용자 → Route 53 → CloudFront → API Gateway → Lambda → DynamoDB`

Include:

- edge routing
- IAM auth
- Lambda triggers
- private/public distinction

### Hybrid enterprise network

Flow:

`온프레미스 ↔ Direct Connect ↔ Transit Gateway ↔ 공유 서비스 VPC ↔ 워크로드 VPC`

Include:

- centralized egress
- inspection VPC
- TGW route tables
- PrivateLink

## Final output quality check

Before finishing, verify the PNG:

- is technically correct
- resembles AWS reference architecture diagrams
- uses Korean-first labels and annotations, with natural AWS/technical English where clearer
- maintains consistent educational styling
- is visually clean
- has no overlapping arrows or labels
- has complete AZ/VPC/subnet boundaries
- prioritizes understanding over decoration
- is suitable for professional AWS study documentation
