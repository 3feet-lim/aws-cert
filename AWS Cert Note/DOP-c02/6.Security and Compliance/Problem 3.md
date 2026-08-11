
한 회사의 보안팀은 모든 외부용 Application Load Balancer(ALB)와 Amazon API Gateway API가 AWS WAF 웹 ACL과 연결되어 있을 것을 요구한다. 회사는 수백 개의 AWS 계정을 보유하고 있으며, 모두 AWS Organizations의 단일 조직에 포함되어 있다. 회사는 조직 전체에 AWS Config를 구성해 두었다. 감사 중에, 회사는 AWS WAF 웹 ACL과 연결되지 않은 일부 외부 노출 ALB를 발견했다.

향후 위반을 방지하기 위해 DevOps 엔지니어가 취해야 할 단계의 조합은? (2개 선택)

**A.** AWS Firewall Manager를 보안 계정에 위임(delegate)한다.

**B.** Amazon GuardDuty를 보안 계정에 위임한다.

**C.** 새로 생성되는 ALB와 API Gateway API에 AWS WAF 웹 ACL을 연결하는 AWS Firewall Manager 정책을 만든다.

**D.** 새로 생성되는 ALB와 API Gateway API에 AWS WAF 웹 ACL을 연결하는 Amazon GuardDuty 정책을 만든다.

**E.** 새로 생성되는 ALB와 API Gateway API에 AWS WAF 웹 ACL을 연결하는 AWS Config 관리형 규칙을 구성한다.




# 해설


정답: A, C

해설:

핵심은 "수백 개 계정으로 구성된 AWS Organizations 조직 전체"에 WAF 연결을 강제하고, 향후 새로 만들어지는 리소스까지 자동으로 준수시키는 것이다. 이 다계정 방화벽/WAF 일괄 관리가 바로 AWS Firewall Manager의 존재 이유다.

A — Firewall Manager는 Organizations와 연동되며, 사용 전 조직 관리 계정이 Firewall Manager 관리 권한을 특정 보안(관리자) 계정에 **위임**해야 한다. 이것이 전제 단계다.

C — 그런 다음 Firewall Manager 정책을 만들어 조직 내 모든 계정의 ALB·API Gateway에 WAF 웹 ACL을 자동으로 연결·강제한다. Firewall Manager 정책은 신규 생성 리소스에 자동 적용되고 미준수 리소스를 지속적으로 교정하므로 "향후 위반 방지"라는 요구를 충족한다.

오답 이유:

B. GuardDuty는 위협 탐지(악성 활동·이상 행위 모니터링) 서비스이지, WAF 웹 ACL을 리소스에 연결하거나 방화벽 정책을 강제하는 서비스가 아니다. 용도 자체가 맞지 않는다.

D. GuardDuty에는 "ALB/API Gateway에 WAF를 연결하는 정책" 같은 기능이 존재하지 않는다. 서비스 용도와 무관한 함정이다.

E. AWS Config 관리형 규칙은 리소스의 준수 여부를 **탐지·평가**하는 것이 본질이다. WAF 미연결 ALB를 컴플라이언스 실패로 표시할 수는 있어도, "WAF 웹 ACL을 연결한다"는 것을 수행하는 관리형 규칙은 없다(연결은 별도 교정 작업의 몫). 또한 다계정 조직 전반의 WAF 강제·자동 적용에는 Firewall Manager가 정석이며 Config 규칙만으로는 신규 리소스에 WAF를 자동 부착할 수 없다.