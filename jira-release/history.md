# 자주 발생한 문제 및 해결

## 1. ❌ 인증 실패

- **현상**: Jira FixVersion 업데이트 시 실패
- **원인**: Secrets가 전달되지 않음 (`DOMAIN`, `USER`, `API_TOKEN`)
- **해결**: Secret 추가 및 environment 변경

## 2. 🧵 $GITHUB_OUTPUT 포맷 오류
현상: 커밋 메시지 여러 줄 저장 시 에러 발생
해결: Base64 인코딩

COMMITS_BASE64=$(echo "$COMMITS" | base64 -w 0)
echo "commits_base64=$COMMITS_BASE64" >> $GITHUB_OUTPUT

## 3. 🚫 Slack 메시지가 실패 시 전송되지 않음
원인: 실패한 step 이후는 GitHub Actions가 다음 step을 생략
해결:
yaml
if: always()

## 4. 📛 Slack 메시지 포맷 깨짐
현상: 이모지, 줄바꿈 등 포함된 메시지 Slack 전송 실패
해결:
<url|텍스트> 포맷으로 링크 처리
echo 또는 printf로 안전하게 문자열 출력




## 5. Slack webhook 오류
원인
Slack 메시지 변수 $MSG 안에 줄바꿈(\n), 따옴표("), 백슬래시 등이 포함되어 있고
해당 문자열이 --data-urlencode "payload=..."에 직접 삽입되면 쉘이 문자열을 잘못 인식하여 명령어처럼 실행됨
해결
메시지를 직접 인라인으로 삽입하지 않고, 안전하게 이스케이프 처리하는 jq -Rs 방식을 사용
