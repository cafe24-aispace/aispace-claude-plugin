# Cafe24 AI SPACE — Claude Code 플러그인 사용 매뉴얼

Cafe24 AI SPACE를 Claude Code에서 대화만으로 사용할 수 있는 플러그인입니다.

---

## 1. 사전 준비

| 항목 | 설명 |
|------|------|
| **Claude Code** | Anthropic의 터미널 AI 에이전트. `npm install -g @anthropic-ai/claude-code`로 설치 |
| **카페24 계정** | [카페24](https://www.cafe24.com) 회원가입 필요 |
| **AI SPACE 신청** | [AI SPACE](https://aispace.cafe24.com)에서 서비스 신청 (14일 무료 체험) |
| **API 키** | 불필요 — OAuth 2.0 자동 인증 사용 |

---

## 2. 설치 방법

Claude Code 터미널에서 아래 명령을 순서대로 입력합니다.

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

> ✅ 설치는 최초 1회만 하면 됩니다. 이후 Claude Code를 실행할 때마다 플러그인이 자동으로 로드됩니다.

---

## 3. 계정 연결 (인증)

플러그인 설치 후 Cafe24 계정을 연결해야 합니다. **최초 1회**만 필요합니다.

> ⚠️ **필수 단계입니다.** 플러그인 설치만으로는 인증이 자동으로 진행되지 않습니다. 아래 절차를 반드시 수행해야 합니다.

### Step 1. MCP 서버 관리 화면 열기

```
/mcp
```

### Step 2. cafe24-aispace 서버 선택

서버 목록에서 **cafe24-aispace** 를 찾아 선택합니다.

### Step 3. 인증 진행

**Authenticate**를 선택하면 브라우저가 열립니다. Cafe24 AI SPACE를 신청한 계정으로 로그인을 완료합니다.

### Step 4. 연결 확인

로그인이 완료되면 Claude Code 터미널에 **"Authentication successful"** 메시지가 표시됩니다. 이제 대화에서 바로 사용할 수 있습니다.

> ℹ️ 인증 토큰은 자동으로 갱신됩니다. 장기간 미사용 후 토큰이 만료되면 동일한 `/mcp` 절차로 다시 인증하면 됩니다.

---

## 4. 사용 가능한 기능

플러그인은 5가지 스킬을 제공합니다. 슬래시 명령어로 직접 호출하거나 자연어로 요청하면 자동으로 활성화됩니다.

| 기능 | 명령어 | 설명 |
|------|--------|------|
| **앱 배포** | `/cafe24-aispace:deploy` | 코드를 생성하고 AI SPACE에 배포. DB 설정, 런타임 감지 자동 처리 |
| **상태 조회** | `/cafe24-aispace:status` | 프로젝트 목록, 실행 상태, 빌드 로그, 리소스 사용량 조회 |
| **환경변수** | `/cafe24-aispace:env` | API 키, 설정값 등 환경변수 조회/추가/수정/삭제 |
| **백업** | `/cafe24-aispace:backup` | 소스 코드 + DB 데이터 백업, 다운로드 링크 제공 |
| **GitHub 연동** | `/cafe24-aispace:github-connect` | GitHub 저장소를 연결하여 배포 및 코드 업데이트 반영 |

### 지원 런타임

| 런타임 | 버전 | 데이터베이스 |
|--------|------|-------------|
| PHP (Apache) | 8.2 | MySQL, PostgreSQL, SQLite, Redis, Memcached |
| Node.js | 20 | (동일) |
| Python (FastAPI/Flask/Django) | 3.11 | (동일) |
| Static (Nginx) | - | (동일) |

---

## 5. 사용 방법 및 예시

명령어를 외울 필요 없이 자연어로 요청하면 됩니다.

### 앱 배포

```
커피숍 홈페이지를 만들어서 배포해줘
이 코드를 AI SPACE에 배포해줘
```

Claude가 코드를 생성하고, 런타임을 자동 감지하여 배포합니다. DB가 필요하면 자동으로 설정합니다.

### 상태 확인 및 관리

```
내 프로젝트 목록 보여줘
왜 배포 실패했는지 로그 확인해줘
```

### 환경변수 관리

```
my-blog에 API_KEY 환경변수 설정해줘
현재 환경변수 보여줘
```

### 백업 및 GitHub 연동

```
내 프로젝트 백업해줘
내 GitHub 저장소를 연결해서 배포해줘
```

---

## 6. 유의사항

### 🔐 인증은 `/mcp`에서 진행합니다

인증 관련 에러가 나면 `/login`이 아니라 `/mcp` → cafe24-aispace → Authenticate 순서로 진행하세요. `/login`은 Claude Code 자체 인증이며 AI SPACE MCP 서버 인증과는 별개입니다.

### 🐳 Dockerfile을 생성하지 마세요

AI SPACE는 런타임 이미지 기반 배포를 사용합니다. Dockerfile, docker-compose.yml 등을 만들면 배포가 실패할 수 있습니다.

### 🗄️ DB 환경변수를 직접 설정하지 마세요

`DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`는 서버가 자동으로 주입합니다. 코드에서는 환경변수를 읽기만 하면 됩니다.

### 💾 영속 데이터는 `/app/user_data/`에 저장하세요

업로드 파일, SQLite DB 등 유지해야 하는 데이터는 반드시 이 경로 하위에 저장해야 합니다. 다른 경로는 재배포 시 초기화됩니다.

### 📦 지원하지 않는 런타임이 있습니다

Go, Java, Rust 등은 현재 미지원입니다. PHP, Node.js, Python, Static(HTML/CSS/JS)만 사용 가능합니다.

### ⏰ 백업 다운로드 링크는 7일간 유효합니다

기간이 지나면 다시 백업을 요청하세요. DB가 있는 프로젝트는 SQL 덤프가 자동 포함됩니다.

---

## 7. 문제 해결

### "requires re-authorization" / "token expired" 에러

> 🚫 **`/login`은 해결 방법이 아닙니다.** `/login`은 Claude Code 자체 인증이며 MCP 서버 인증과 무관합니다.

**올바른 해결 방법:**

1. `/mcp` 입력
2. cafe24-aispace 선택
3. Authenticate 진행
4. 브라우저에서 Cafe24 AI SPACE를 신청한 계정으로 로그인

### "Needs authentication" 상태로 도구가 호출되지 않음

플러그인 설치 직후에 발생하는 정상적인 상태입니다. 위와 동일하게 `/mcp`에서 인증을 진행하세요.

### 플러그인 설치 후 MCP 도구가 보이지 않음

Claude Code를 재시작하세요. 플러그인의 MCP 서버는 재시작 후에 로드됩니다.

```
exit
claude
```

### 플러그인 재설치가 필요한 경우

문제가 지속되면 플러그인을 완전히 제거한 뒤 다시 설치합니다.

```
# 삭제
/plugin uninstall cafe24-aispace
/plugin marketplace remove cafe24-aispace-plugins

# 재설치
/plugin marketplace add cafe24-aispace/aispace-claude-plugin
/plugin install cafe24-aispace
```

---

## 8. 자주 묻는 질문

**Q. 무료 체험 기간이 지나면 어떻게 되나요?**

14일 무료 체험 후 유료 플랜으로 전환됩니다. 배포된 앱은 플랜 전환 전까지 정상 운영되며, 전환하지 않으면 서비스가 중단됩니다.

**Q. 한 번에 몇 개까지 배포할 수 있나요?**

AI SPACE 웹콘솔에서 공간(Space)을 추가할 수 있습니다. `/cafe24-aispace:status`로 현재 사용 가능한 빈 공간을 확인할 수 있습니다.

**Q. Claude.ai 웹 버전의 커넥터와 동시에 사용할 수 있나요?**

네. Claude Code 플러그인과 Claude.ai 웹 커넥터는 독립적으로 동작합니다. 같은 Cafe24 계정으로 양쪽 모두 사용할 수 있고, 배포된 프로젝트도 공유됩니다.

**Q. 플러그인 업데이트는 어떻게 하나요?**

`/plugin update cafe24-aispace`로 최신 버전으로 업데이트할 수 있습니다. MCP 서버는 서버 측에서 자동 업데이트되므로 별도 작업이 필요 없습니다.

**Q. 플러그인 없이 MCP 서버만 직접 등록해서 쓸 수 있나요?**

네. `claude mcp add cafe24-aispace -t http -u https://aih-proxy.cafe24.com/mcp` 명령으로 MCP 서버를 직접 등록할 수도 있습니다. 다만 이 경우 스킬(deploy, status 등)은 제공되지 않습니다.

**Q. Windows에서 설치 시 에러가 발생합니다.**

Windows에서 간헐적으로 파일 잠금(EBUSY) 에러가 발생할 수 있습니다. Claude Code를 완전히 종료하고, `C:\Users\{사용자명}\.claude\plugins\marketplaces\` 폴더 안의 내용을 삭제한 뒤 다시 설치를 시도하세요.
