
# 🛠️ Update Jira Fix Version GitHub Workflow


##Job: AfterReleaseTagJob.yml

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
