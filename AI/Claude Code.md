---
tags:
  - CLAUDE
  - AI
---

# Claude Code

## 🚀 시작하기

```bash
# Claude Code 실행
$ claude

# 대화 선택해서 이어가기
$ claude --resume
$ claude -r

# 최근 대화 이어가기
$ claude --continue
$ claude -c
```

---

## 💬 슬래시 명령어

### 초기 설정

| 명령어 | 설명 |
|---|---|
| `/init` | `CLAUDE.md` 파일 생성 (프로젝트 메모리) |
| `/terminal-setup` | `Shift`+`Enter` 줄바꿈 키 바인딩 설정 |
| `/config` | 환경 설정 |
| `/permissions` | 권한 관리 |
| `/model` | 모델 변경 (`sonnet` \| `opus`) |

### 대화 관리

| 명령어 | 설명 |
|---|---|
| `/clear` | 대화 초기화 |
| `/compact` | 대화 내용 요약 정리 |
| `/resume` | 대화 재개 |

### 출력 스타일 `/output-style`

| 옵션 | 설명 |
|---|---|
| `Default` | 효율적으로 완료, 간결한 답변 |
| `Explanatory` | 구현 선택 사항과 코드베이스 패턴 설명 |
| `Learning` | 잠시 멈추고 실습용 작은 코드 조각 작성 요청 |
| `Concise Korean` | 한국어 간결 모드 |

### 단축 입력

| 입력 | 설명 |
|---|---|
| `#` | `CLAUDE.md`에 내용 추가 (메모리 기능) |
| `@` | 파일 / 디렉토리 자동완성 |
| `!` | Bash 명령어 직접 실행 |

---

## 🔄 모드

`Shift` + `Tab` 으로 전환

| 모드 | 설명 |
|---|---|
| `default` | 파일 수정 전 허락 구함 |
| `auto-accept` | 허락 없이 바로 수정 |
| `plan` | 실행 없이 계획 · 분석만 수행 |

---

## ⌨️ 키보드 단축키

| 단축키 | 설명 |
|---|---|
| `ESC` | 작업 중단 |
| `ESC` `ESC` | 이전 대화로 이동 |
| `Shift` + `Tab` | 모드 전환 (default → auto-accept → plan) |
| `Shift` + `Enter` | 줄바꿈 (⚠️ `/terminal-setup` 먼저 실행 필요) |
| `↑` | 이전 명령어 불러오기 |
| `Ctrl` + `C` | 강제 종료 |

---

## 💡 Tips

### 기본 사용

- 명령어 수행 중에도 추가 명령어 입력 가능
- 이미지는 Claude Code 창에 **드래그 앤 드롭**하면 바로 업로드

---

## 📝 CLAUDE.md 작성법

`/init` 으로 생성되는 프로젝트 메모리 파일. Claude가 대화 시작 때마다 자동으로 읽는다.

### 권장 구조

```markdown
# 프로젝트 개요
어떤 서비스인지 한 줄 설명

# 기술 스택
- Next.js 14, TypeScript, Tailwind CSS
- 상태관리: Zustand
- DB: Supabase

# 디렉토리 구조
src/
├── app/        # 페이지
├── components/ # 공통 컴포넌트
└── lib/        # 유틸리티

# 코드 스타일
- 컴포넌트는 함수형으로 작성
- 파일명은 PascalCase
- CSS는 Tailwind 우선, 복잡한 건 CSS Module

# 자주 쓰는 명령어
npm run dev     # 개발 서버
npm run build   # 빌드
npm run test    # 테스트

# 주의사항
- .env 파일 절대 커밋 금지
- PR 전 반드시 lint 확인
```

### 대화 중 메모리 추가

```
# 기억해줘: API 응답 타입은 항상 Zod로 검증해
```
`#` 으로 시작하면 CLAUDE.md에 자동으로 추가됨

---

## 💰 컨텍스트 & 비용 관리

Claude Code는 대화가 길어질수록 토큰(비용)이 늘어남

### 컨텍스트 줄이는 방법

| 방법 | 명령어 | 설명 |
|---|---|---|
| 요약 압축 | `/compact` | 대화를 요약해서 컨텍스트 줄임 (대화는 유지) |
| 완전 초기화 | `/clear` | 대화 전부 삭제하고 새로 시작 |
| 파일 지정 | `@파일명` | 전체 프로젝트 대신 특정 파일만 참조 |

### 비용 아끼는 팁

- 큰 작업은 `/compact` → 새 세션으로 이어가기
- 반복 지시사항은 `CLAUDE.md`에 적어두기 (매번 말 안 해도 됨)
- 파일 전체보다 `@특정파일` 지정이 훨씬 저렴
- `plan` 모드로 계획 먼저 확인 후 실행

---

## 🛠️ 커스텀 명령어

반복 작업을 마크다운 파일로 정의해두고 `/명령어`로 실행하는 기능

### 저장 위치

| 위치 | 범위 | git 커밋 |
|---|---|---|
| `~/.claude/commands/*.md` | 내 모든 프로젝트 (전역) | ❌ |
| `.claude/commands/*.md` | 해당 프로젝트만 (로컬) | ✅ |

### 기본 구조

```
my-project/
└── .claude/
    └── commands/
        ├── review.md      →  /review
        ├── deploy.md      →  /deploy
        └── test-all.md    →  /test-all
```

### 예시: `css-order.md` → `/css-order`

```markdown
---
argument-hint: "[optional: file path or 'current' for current file]"
description: "CSS 속성 순서 정리"
---
# CSS Properties Ordering

아래 정의된 정렬 기준에 따라 CSS 속성 순서를 정리해줍니다.

## 정리 기준

### 1. Layout
display,
flex-direction, justify-content, align-items, gap
position, (top/right/bottom/left), z-index, float, clear, overflow,

### 2. Box Model
width, min-width, max-width, height, min-height, max-height, aspect-ratio
box-sizing
margin, padding,
border, border-radius, outline

### 3. Color & Background
color, background, box-shadow, text-shadow

### 4. Typography
font-*, text-align, text-decoration, text-transform,
letter-spacing, line-height, white-space,
word-break, overflow-wrap

### 5. Etc
opacity, visibility, cursor, transition, transform, animation

---
적용 대상: Tailwind CSS / Styled Components / 일반 CSS

$ARGUMENTS
```

---

## 🔔 알림 훅 설정

### 설정 파일 우선순위

| 우선순위 | 파일 | 범위 |
|---|---|---|
| 1 | `.claude/settings.local.json` | 로컬 개인 설정 |
| 2 | `.claude/settings.json` | 프로젝트 팀 공유 설정 |
| 3 | `~/.claude/settings.json` | 전역 개인 설정 |

### 설정 예시

```bash
$ vim ~/.claude/settings.json
```

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude가 입력을 기다립니다\" with title \"Claude Code\"'"
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"작업 완료!\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```
