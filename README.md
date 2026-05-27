# Cafe24 AI SPACE Plugin for Claude Code

Cafe24 AI SPACE를 Claude Code에서 대화만으로 사용할 수 있는 플러그인입니다.

## 기능

- **앱 배포**: 코드 생성부터 배포까지 대화로 완료
- **상태 조회**: 프로젝트 상태, 로그, 리소스 확인
- **환경변수 관리**: API 키, 설정값 등을 대화로 관리
- **백업**: 소스 코드 + DB 데이터 백업 및 다운로드
- **GitHub 연동**: 외부 저장소를 연결하여 배포

## 설치

### 공식 마켓플레이스 (등록 후)

```bash
claude plugin install cafe24-aispace
```

### 로컬 테스트

```bash
claude --plugin-dir ./cafe24-aispace
```

## 사전 준비

- [카페24 계정](https://www.cafe24.com)
- [AI SPACE 서비스 신청](https://aispace.cafe24.com) (14일 무료 체험)
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

## 인증

OAuth 2.0 기반 카페24 계정 인증을 사용합니다. 처음 도구 호출 시 브라우저에서 카페24 로그인만 하면 되며, 이후 토큰 갱신은 자동으로 처리됩니다.

## 라이선스

MIT
