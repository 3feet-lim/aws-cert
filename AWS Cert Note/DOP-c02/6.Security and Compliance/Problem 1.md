
한 회사는 개발자들이 계정 내 모든 Amazon EBS 볼륨에 원하는 백업 주기를 나타내는 태그를 지정하도록 요구한다. 이 요구사항은 백업이 필요 없는 EBS 볼륨까지 포함한다. 회사는 `Backup_Frequency`라는 커스텀 태그를 사용하며, 값은 원하는 백업 주기에 대응하는 none, daily, weekly 중 하나다. 감사 결과, 개발자들이 이따금 EBS 볼륨에 태그를 지정하지 않는다는 사실이 발견됐다.

DevOps 엔지니어는 다른 값이 지정되지 않는 한 회사가 최소 주 1회 백업을 수행할 수 있도록, 모든 EBS 볼륨이 항상 `Backup_Frequency` 태그를 갖도록 보장해야 한다.

이 요구사항을 충족하는 솔루션은?

**A.** 계정에 AWS Config를 설정한다. `Backup_Frequency` 태그가 없는 모든 Amazon EC2 리소스에 대해 컴플라이언스 실패를 반환하는 커스텀 규칙을 만든다. 커스텀 AWS Systems Manager Automation 런북을 사용해 `Backup_Frequency` 태그를 weekly 값으로 적용하는 교정 작업을 구성한다.

**B.** 계정에 AWS Config를 설정한다. `Backup_Frequency` 태그가 없는 EC2::Volume 리소스에 대해 컴플라이언스 실패를 반환하는 관리형 규칙(managed rule)을 사용한다. 커스텀 AWS Systems Manager Automation 런북을 사용해 `Backup_Frequency` 태그를 weekly 값으로 적용하는 교정 작업을 구성한다.

**C.** 계정에 AWS CloudTrail을 켠다. EBS CreateVolume 이벤트에 반응하는 Amazon EventBridge 규칙을 만든다. `Backup_Frequency` 태그를 weekly 값으로 적용하는 커스텀 AWS Systems Manager Automation 런북을 구성한다. 이 런북을 규칙의 대상(target)으로 지정한다.

**D.** 계정에 AWS CloudTrail을 켠다. EBS CreateVolume 이벤트 또는 EBS ModifyVolume 이벤트에 반응하는 Amazon EventBridge 규칙을 만든다. `Backup_Frequency` 태그를 weekly 값으로 적용하는 커스텀 AWS Systems Manager Automation 런북을 구성한다. 이 런북을 규칙의 대상으로 지정한다.




# 해설


정답: B

해설:

핵심 요구는 "모든 EBS 볼륨이 **항상** `Backup_Frequency` 태그를 갖도록 보장"하는 것이다. 즉 신규 생성 시점뿐 아니라 이미 존재하는 볼륨과 태그가 누락된 상태까지 지속적으로 감지·교정해야 한다. AWS Config는 리소스 구성을 상시 평가하는 서비스이고, 태그 존재 여부를 검사하는 `required-tags` **관리형 규칙**이 기본 제공된다. 이 관리형 규칙을 EC2::Volume 리소스에 적용하면 태그 없는 볼륨을 컴플라이언스 실패로 표시하고, SSM Automation 런북을 교정 작업으로 연결해 weekly 값을 자동으로 붙인다. 관리형 규칙을 쓰므로 커스텀 규칙을 직접 작성·유지할 필요가 없어 오버헤드도 낮다. "다른 값이 지정되지 않는 한 최소 주 1회"라는 조건도 태그가 없을 때만 weekly로 채우는 방식과 정확히 맞는다.

오답 이유:

A. AWS Config를 쓰는 방향은 맞지만 두 가지가 나쁘다. 첫째, 태그 검사는 이미 관리형 규칙(`required-tags`)이 있는데 굳이 커스텀 규칙을 만들어 오버헤드를 키운다. 둘째, 평가 대상을 "모든 EC2 리소스"로 잡아 볼륨이 아닌 인스턴스·기타 리소스까지 범위가 어긋난다. 대상이 EC2::Volume으로 정확한 B가 우월하다.

C. CloudTrail + EventBridge로 CreateVolume 이벤트에만 반응하는 방식은 **신규로 생성되는 볼륨만** 처리한다. 이미 존재하면서 태그가 누락된 볼륨은 전혀 교정되지 않아 "항상 태그를 갖도록 보장"이라는 요구를 충족하지 못한다. 이벤트 기반은 시점 트리거일 뿐 상태를 지속 평가하지 못한다.

D. C에 ModifyVolume 이벤트를 추가해 커버리지를 조금 넓혔지만, 여전히 이벤트가 발생하는 순간에만 반응하는 방식이다. 이벤트를 유발하지 않는 채로 이미 존재하는 태그 누락 볼륨은 잡아내지 못하므로 상시 컴플라이언스 보장이 안 된다. 지속 평가·교정에는 AWS Config가 정석이다.