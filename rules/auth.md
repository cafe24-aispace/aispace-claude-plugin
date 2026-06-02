# 인증 에러 대응 (공통 규칙)

MCP 도구 호출 시 `requires re-authorization`, `token expired`, `Needs authentication` 에러가 발생하면:

1. **`/login`은 해결 방법이 아닙니다.** `/login`은 Claude Code 자체 인증이며 MCP 서버 인증과 무관합니다.
2. 사용자에게 **`/mcp` 명령을 입력**하도록 안내합니다.
3. 서버 목록에서 **cafe24-aispace**를 선택하고 **Authenticate**를 진행하여 브라우저에서 Cafe24 AI SPACE를 신청한 계정으로 로그인을 완료합니다.
4. 로그인 완료 후 다시 요청하면 정상 동작합니다.

> 이 인증은 MCP 서버의 OAuth 토큰 갱신이며, `/login`이나 `/cafe24-login`과는 별개입니다.
