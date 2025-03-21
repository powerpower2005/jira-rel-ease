# 자주 발생한 문제 및 해결

## 1. ❌ 인증 실패

- **현상**: Jira FixVersion 업데이트 시 실패
- **원인**: Secrets가 전달되지 않음 (`DOMAIN`, `USER`, `API_TOKEN`)
- **해결**: Secret 추가 및 environment 변경

## 2. 🧵 $GITHUB_OUTPUT 포맷 오류
현상: 커밋 메시지 여러 줄 저장 시 에러 발생
해결: Base64 인코딩
bash
복사
편집
COMMITS_BASE64=$(echo "$COMMITS" | base64 -w 0)
echo "commits_base64=$COMMITS_BASE64" >> $GITHUB_OUTPUT
3. 🚫 Slack 메시지가 실패 시 전송되지 않음
원인: 실패한 step 이후는 GitHub Actions가 다음 step을 생략
해결:
yaml
복사
편집
if: always()
4. 📛 Slack 메시지 포맷 깨짐
현상: 이모지, 줄바꿈 등 포함된 메시지 Slack 전송 실패
해결:
<url|텍스트> 포맷으로 링크 처리
echo 또는 printf로 안전하게 문자열 출력
