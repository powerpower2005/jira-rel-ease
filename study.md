Project Version = Jira Release
https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-project-versions/#api-group-project-versions



프로젝트 정보 조회	/rest/api/3/project/{PROJECT_KEY}	GET	projectId 조회 용
FixVersion 목록 조회	/rest/api/3/project/{PROJECT_KEY}/versions	GET	기존 FixVersion 확인
FixVersion 생성	/rest/api/3/version	POST	FixVersion이 없을 경우 생성
이슈 업데이트	/rest/api/3/issue/{ISSUE_KEY}	PUT	FixVersion 필드에 값 추가
