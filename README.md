# Cafe24 AI SPACE Plugin for Claude Code

Cafe24 AI SPACE를 Claude Code에서 대화만으로 사용할 수 있는 플러그인입니다.

## 기능

- **앱 배포**: 코드 생성부터 배포까지 대화로 완료
- **상태 조회**: 프로젝트 상태, 로그, 리소스 확인
- **환경변수 관리**: API 키, 설정값 등을 대화로 관리
- **백업**: 소스 코드 + DB 데이터 백업 및 다운로드
- **GitHub 연동**: 외부 저장소를 연결하여 배포

## 설치 방법

Claude Code 터미널에서 아래 명령을 순서대로 입력하세요.

### Step 1. 마켓플레이스 등록

```
/plugin marketplace add cafe24-aispace/aispace-claude-plugin
```

### Step 2. 플러그인 설치

```
/plugin install cafe24-aispace
```

설치 범위를 묻는 화면이 나타나면 **Install for you (user scope)** 를 선택합니다.

### Step 3. Claude Code 재시작

```
exit
claude
```

플러그인의 MCP 서버를 로드하려면 Claude Code를 재시작해야 합니다.

### Step 4. Cafe24 계정 연결 (최초 1회)

```
/mcp
```

1. `/mcp` 입력 후 서버 목록에서 **cafe24-aispace** 를 선택합니다.
2. **Authenticate** 를 진행하여 브라우저에서 Cafe24 AI SPACE를 신청한 계정으로 로그인을 완료합니다.

> ⚠️ **이 단계는 필수입니다.** 플러그인 설치만으로는 인증이 자동으로 진행되지 않습니다.
> `/mcp`에서 수동으로 인증을 한 번 진행해야 합니다. 이후에는 토큰이 자동 갱신됩니다.

### Step 5. 사용 시작

인증이 완료되면 대화에서 바로 사용할 수 있습니다.

```
내 프로젝트 목록 보여줘
```

## 사전 준비

- [카페24 호스팅센터 계정](https://hosting.cafe24.com)
- [AI SPACE 서비스 신청](https://hosting.cafe24.com/?controller=new_product_page&page=ai-space) (14일 무료 체험)
- 별도 API 키 불필요 (OAuth 2.0 자동 인증)

## Skills

| Skill | 호출 | 설명 |
|-------|------|------|
| deploy | `/cafe24-aispace:deploy` | 새 웹 앱 배포 |
| status | `/cafe24-aispace:status` | 프로젝트 상태/로그 조회 |
| backup | `/cafe24-aispace:backup` | 프로젝트 백업 |
| env | `/cafe24-aispace:env` | 환경변수 조회/설정/삭제 |
| github-connect | `/cafe24-aispace:github-connect` | GitHub 저장소 연결 배포 |

자연어로 요청하면 적절한 Skill이 자동으로 활성화됩니다.

## 사용 예시

```
커피숍 홈페이지를 만들어서 배포해줘
내 프로젝트 상태 보여줘
my-blog에 환경변수 API_KEY를 설정해줘
my-blog 백업해줘
내 GitHub 저장소를 연결해서 배포해줘
```

## 지원 런타임

- PHP 8.2, Node.js 20, Python 3.11, Static (HTML/CSS/JS)
- DB: MySQL, PostgreSQL, SQLite, Redis, Memcached

## 라이선스

MIT
