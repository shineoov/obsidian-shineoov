---
tags:
  - AI
  - GEMINI
---

# Gemini CLI

Google이 만든 오픈소스 터미널 AI 에이전트. 코딩, 파일 편집, 웹 검색, 작업 자동화 등을 자연어로 수행

## 📦 설치

```bash
# 전역 설치
npm install -g @google/gemini-cli

# 설치 없이 바로 실행
npx @google/gemini-cli
```

## 🔐 인증

```bash
# 실행하면 인증 방법 선택 화면 나옴
gemini
```

| 방법 | 설명 |
|---|---|
| Google 계정 로그인 | 무료 (Gemini 2.5 Pro, 분당 60회 제한) |
| API Key | Google AI Studio에서 발급 → 환경변수 설정 |

```bash
# API Key 사용 시
export GEMINI_API_KEY=your_api_key_here
```

---

## 🚀 시작하기

```bash
# 대화형 모드 (REPL)
gemini

# 단일 명령 실행 (대화 없이 바로 결과)
gemini -p "현재 디렉토리 파일 목록 보여줘"

# 모델 지정해서 실행
gemini -m gemini-2.5-flash   # Flash 모델 (빠름, 저렴)
gemini -m gemini-2.5-pro     # Pro 모델 (기본값, 고성능)
```

---

## 💬 슬래시 명령어

### 기본

| 명령어 | 설명 |
|---|---|
| `/help` | 도움말 및 전체 명령어 목록 |
| `/about` | 버전, 현재 모델, 인증 방법 확인 |
| `/quit` | Gemini CLI 종료 |
| `/clear` | 화면 초기화 (메모리는 유지됨) |
| `/settings` | 설정 에디터 열기 |
| `/theme` | UI 테마 변경 |
| `/stats` | 현재 세션 토큰 사용량 통계 |
| `/tools` | 사용 가능한 툴 목록 확인 |
| `/bug` | GitHub에 버그 리포트 제출 |

### 프로젝트 & 메모리

| 명령어 | 설명 |
|---|---|
| `/init` | 프로젝트 분석 후 `GEMINI.md` 자동 생성 |
| `/memory show` | 현재 AI가 기억하는 내용 확인 |
| `/memory add` | 메모리 수동 추가 (`pnpm 써줘` 등) |
| `/memory refresh` | 메모리 강제 새로고침 |
| `/memory list` | 활성 GEMINI.md 파일 경로 목록 |

### 대화 관리

| 명령어 | 설명 |
|---|---|
| `/compress` | 대화 내용을 요약해서 토큰 절약 (내용은 유지) |
| `/chat save <이름>` | 현재 대화 저장 |
| `/chat resume <이름>` | 저장된 대화 불러오기 |
| `/chat list` | 저장된 대화 목록 |
| `/chat delete <이름>` | 저장된 대화 삭제 |

### 파일 복구

| 명령어 | 설명 |
|---|---|
| `/restore` | 마지막 툴 실행 전 상태로 파일 복구 |
| `/rewind` | 대화 기록 되감기 (파일 변경도 함께 취소) |

### 기타

| 명령어 | 설명 |
|---|---|
| `/copy` | 마지막 Gemini 출력을 클립보드에 복사 |
| `/vim` | vim 모드 토글 |
| `/editor` | 선호하는 외부 에디터 설정 |
| `/mcp` | MCP 서버 목록 및 툴 확인 |
| `/auth` | 인증 방법 변경 |

---

## 단축 입력

| 입력 | 설명 |
|---|---|
| `@파일명` | 파일 내용을 프롬프트에 포함 (이미지, PDF, 오디오, 영상도 가능) |
| `@디렉토리명` | 디렉토리 전체를 컨텍스트에 포함 (git ignore 자동 적용) |
| `!명령어` | 쉘 명령 바로 실행 (결과가 컨텍스트에 포함됨) |
| `!` | 쉘 모드 토글 |

---

## ⌨️ 키보드 단축키

| 단축키 | 설명 |
|---|---|
| `ESC` | 현재 작업 중단 |
| `ESC` `ESC` | 대화 되감기 (`/rewind` 단축키) |
| `Shift` + `Tab` | auto-apply 모드 토글 (파일 수정 자동 적용) |
| `Ctrl` + `C` (×2) | CLI 종료 |
| `Ctrl` + `L` | 화면 초기화 (메모리 유지) |
| `Ctrl` + `J` | 전송 없이 줄바꿈 |
| `Ctrl` + `X` | 현재 프롬프트를 외부 에디터에서 편집 |
| `Ctrl` + `T` | 툴 설명 표시/숨김 토글 |
| `Ctrl` + `Z` | 입력 되돌리기 |
| `Ctrl` + `Shift` + `Z` | 입력 다시 실행 |

---

## 🔄 모드

`Shift` + `Tab` 으로 전환

| 모드 | 설명 |
|---|---|
| `default` | 파일 수정 전 허락 구함 |
| `auto-apply` | 허락 없이 바로 수정 |

---

## 📝 GEMINI.md 작성법

`/init` 으로 생성되는 프로젝트 메모리 파일. 대화 시작 때마다 자동으로 읽음

### 권장 구조

```markdown
# 프로젝트 개요
어떤 서비스인지 한 줄 설명

# 기술 스택
- Next.js 14, TypeScript, Tailwind CSS
- DB: Supabase

# 코드 스타일
- 컴포넌트는 함수형으로 작성
- 파일명은 PascalCase

# 자주 쓰는 명령어
pnpm dev     # 개발 서버
pnpm build   # 빌드

# 주의사항
- .env 파일 절대 커밋 금지
```

### 파일 적용 우선순위 (계층적으로 로드됨)

```
~/.gemini/GEMINI.md          ← 전역 (모든 프로젝트)
~/my-project/GEMINI.md       ← 프로젝트 루트
~/my-project/src/GEMINI.md   ← 서브 디렉토리
```

---

## 🛠️ 커스텀 명령어

TOML 파일로 반복 작업을 `/명령어`로 실행하는 기능

### 저장 위치

| 위치 | 범위 |
|---|---|
| `~/.gemini/commands/*.toml` | 내 모든 프로젝트 (전역) |
| `.gemini/commands/*.toml` | 해당 프로젝트만 (로컬) |

### 명령어 이름 규칙

파일 경로가 명령어 이름이 됨

```
commands/
├── review.toml        →  /review
└── test/
    └── gen.toml       →  /test:gen
```

### 예시: `review.toml` → `/review`

```toml
name = "review"
description = "코드 리뷰해줘"

[parameters.focus]
type = "string"
description = "리뷰 집중 포인트 (성능 | 보안 | 가독성)"
default = "전체"

prompt = """
아래 코드를 리뷰해줘. 집중 포인트: {{focus}}

- 버그 가능성
- 개선할 수 있는 부분
- 좋은 점도 언급해줘
"""
```

---

## 🔌 MCP 설정

```bash
# MCP 서버 추가
gemini mcp add <이름> <실행명령>

# 목록 확인
gemini mcp list

# 제거
gemini mcp remove <이름>

# CLI에서 현재 연결된 MCP 확인
/mcp
```

---

## 💰 컨텍스트 & 비용 관리

| 방법 | 명령어 | 설명 |
|---|---|---|
| 요약 압축 | `/compress` | 대화를 요약해서 토큰 줄임 |
| 대화 저장 | `/chat save` | 나중에 이어서 사용 |
| 파일 지정 | `@파일명` | 전체 프로젝트 대신 특정 파일만 참조 |
| 통계 확인 | `/stats` | 현재 세션 토큰 사용량 확인 |

---

## 💡 Tips

- `!` 로 실행한 쉘 명령은 에러가 나도 Gemini가 자동으로 해결 방법 제안
- `/restore` 로 잘못된 파일 수정을 빠르게 원복 가능
- `@` 로 이미지, PDF, 오디오, 영상 파일도 컨텍스트에 포함 가능
- `.geminiignore` 파일로 민감한 파일을 `@` 참조에서 제외 가능

---

## 🔗 Ref

- [공식 문서](https://geminicli.com/docs/)
- [GitHub](https://github.com/google-gemini/gemini-cli)
- [Cheatsheet by Phil Schmid](https://www.philschmid.de/gemini-cli-cheatsheet)
