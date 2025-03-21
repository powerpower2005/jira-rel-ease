
# 🛠️ Update Jira Fix Version GitHub Workflow


## Job: AfterReleaseTagJob.yml


### 📋 개요

이 워크플로우는 GitHub Actions를 사용해 Git 저장소의 릴리스 버전 기준으로 커밋 로그를 분석하고, 커밋 메시지에 포함된 Jira 티켓의 Fix Version을 Jira API를 통해 자동으로 업데이트  
각 주요 단계의 상태는 Slack Webhook을 통해 실시간으로 알림

---

### 🚀 기능 요약

- GitHub 저장소에서 태그 기준 커밋 로그 조회
- 커밋 메시지에서 Jira 티켓 키 추출 (`[A-Z][A-Z0-9]+-[0-9]+` 패턴)
- Jira API를 사용한 Fix Version 자동 업데이트
- Slack Webhook을 통한 단계별 알림 전송

---

### ⚙️ 트리거 조건

이 워크플로우는 **수동 실행 (workflow_dispatch)** 으로 동작합니다.
우선적으로 


---

## 📋 전제 조건 (Assumptions)

워크플로우는 다음과 같은 조건을 **전제로 하여 설계**

1. **Git 태그는 삭제되거나 수정되지 않는다**
   - `v{version}-dev` 및 `{version}` 태그가 항상 존재하고 불변함을 가정
   - 태그 범위 기준으로 커밋을 분석하기 때문에 이 범위가 바뀌면 결과가 달라질 수 있음

2. **Jira 이슈(티켓)는 삭제되지 않는다**
   - 릴리스에 포함된 커밋에서 추출된 Jira 티켓은 워크플로우 실행 시 항상 유효하다고 가정
   - 삭제되거나 접근 불가능한 이슈가 없다는 전제 하에 동작

3. **동일한 파라미터로 재실행해도 Jira FixVersion 중복 등록이 실패를 유발하지 않는다**
   - Jira 인스턴스가 동일한 FixVersion을 중복으로 등록할 경우 **오류를 발생시키지 않고 무시하거나 무해하게 처리**한다고 가정
   - 이 조건 하에서 워크플로우는 **멱등성(idempotency)**을 가짐

> 이러한 전제 조건 하에서는 같은 파라미터로 워크플로우를 반복 실행해도 오류 없이 동일한 결과를 생성
