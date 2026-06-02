---
description: Cafe24 AI SPACE에 새 웹 앱을 배포합니다. "배포해줘", "사이트 만들어줘", "앱 올려줘", "deploy" 등을 요청할 때 자동으로 사용됩니다.
argument-hint: "[프로젝트 설명 또는 요청사항]"
---

# AI SPACE 앱 배포

사용자의 요청에 따라 Cafe24 AI SPACE에 웹 앱을 배포합니다.

## 배포 절차

### 1단계: 빈 공간 확인

`list_my_spaces`를 호출하여 배포 가능한 빈 공간을 확인합니다.

- **빈 공간 없음**: "빈 공간이 없습니다. AI SPACE 웹콘솔(https://aispace.cafe24.com)에서 공간을 추가해주세요." 안내 후 중단
- **빈 공간 1개**: 자동 선택
- **빈 공간 2개 이상**: 사용자에게 선택 요청

### 2단계: 소스 코드 준비

- **사용자가 코드를 제공한 경우**: 제공된 코드를 그대로 사용
- **자연어로 요청한 경우** (예: "커피숍 홈페이지 만들어줘"): 요청에 맞는 코드를 생성
- **GitHub 저장소 지정한 경우**: `/cafe24-aispace:github-connect` 워크플로우로 전환

### 3단계: 배포

`project_upload`를 사용하여 배포합니다.

1. `project_upload` (action: `create_session`)으로 업로드 세션 생성
2. 파일을 세션에 업로드
3. `project_upload` (action: `finalize`)로 배포 실행

### 4단계: 결과 확인

`site_verify`로 배포된 사이트의 접속 상태를 확인하고 사용자에게 URL을 안내합니다.

## 지원 런타임

| 런타임 | 버전 | 포트 |
|--------|------|------|
| PHP | 8.2 (Apache) | 80 |
| Node.js | 20 | 3000 |
| Python | 3.11 (FastAPI/Flask/Django) | 8000 |
| Static | Nginx | 80 |

## 데이터베이스 옵션

배포 시 DB가 필요하면 사용자에게 확인 후 추가합니다.

- **MySQL** / **PostgreSQL**: `project_option`으로 추가. DB 환경변수(DB_HOST, DB_PORT, DB_NAME, DB_USER, DB_PASSWORD)는 서버가 자동 주입
- **SQLite**: `/app/user_data/db/` 경로에 파일 생성
- **Redis** / **Memcached**: `project_option`으로 추가

## 주의사항

- **Dockerfile 생성 금지**: 런타임 이미지 기반 배포이므로 Dockerfile, docker-compose.yml 등을 생성하지 마세요
- **DB 환경변수 하드코딩 금지**: DB_HOST 등은 서버가 자동 주입합니다. 코드에서 `os.getenv()` 또는 `getenv()` 등으로 환경변수를 읽도록 작성하세요
- **영속 데이터 경로**: 업로드, DB 파일 등 영속 데이터는 반드시 `/app/user_data/` 하위에 저장하세요
- **미지원 런타임**: Go, Java, Rust 등은 현재 미지원입니다. 요청 시 안내하세요

## 인증 에러 대응

→ `rules/auth.md` 참조
