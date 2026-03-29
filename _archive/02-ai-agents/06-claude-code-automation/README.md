# 06. Claude Code 자동화: Hooks & Commands

> **개발자 심화** — 이 단원은 터미널과 코드 편집에 익숙한 분을 위한 내용입니다.
> 비개발자라면 이 단원을 건너뛰어도 됩니다.

---

> 반복 작업을 자동화하고 나만의 워크플로우를 만든다

---

## 1. 슬래시 커맨드 (Slash Commands)

매일 반복하는 작업을 `/command` 하나로 실행합니다.

### 커맨드 파일 위치

```
your-project/
└── .claude/
    └── commands/
        ├── review.md       → /review
        ├── deploy-check.md → /deploy-check
        └── daily-brief.md  → /daily-brief
```

### 커맨드 파일 작성법

**.claude/commands/review.md**

```markdown
현재 변경된 파일들을 코드 리뷰해줘.

체크 항목:
1. 버그 가능성
2. 성능 문제
3. 보안 취약점
4. 가독성 개선 포인트

각 이슈는 심각도(High/Medium/Low)와 함께 줄 번호를 표시해줘.
```

이제 Claude Code에서 `/review` 만 입력하면 됩니다.

### 유용한 커맨드 아이디어

| 커맨드 | 용도 |
|--------|------|
| `/review` | 변경 파일 코드 리뷰 |
| `/test-gen` | 현재 파일 테스트 자동 생성 |
| `/doc-update` | 코드 변경에 맞게 문서 업데이트 |
| `/commit-msg` | 변경 내용 기반 커밋 메시지 생성 |
| `/debug` | 에러 로그 기반 디버깅 시작 |
| `/daily` | 오늘 작업한 내용 요약 |

---

## 2. Hooks: 이벤트 기반 자동화

Hooks는 특정 이벤트(도구 실행 전/후)에 자동으로 명령을 실행합니다.

### Hook 설정 위치

**.claude/settings.local.json** (개인 설정, Git 제외)
**.claude/settings.json** (팀 공유 설정)

### Hook 타입

| 타입 | 실행 시점 |
|------|-----------|
| `PreToolUse` | 도구 실행 **전** |
| `PostToolUse` | 도구 실행 **후** |

### 실전 예시 1: 파일 수정 후 자동 포맷팅

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write $CLAUDE_TOOL_INPUT_FILE_PATH || true"
          }
        ]
      }
    ]
  }
}
```

**효과**: Claude가 파일을 수정할 때마다 Prettier가 자동 실행됩니다.

### 실전 예시 2: 위험한 명령어 차단

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo $CLAUDE_TOOL_INPUT_COMMAND | grep -qE '(rm -rf|DROP TABLE|format C)' && echo 'BLOCKED: 위험한 명령어' && exit 1 || exit 0"
          }
        ]
      }
    ]
  }
}
```

**효과**: 특정 위험 명령어를 자동으로 차단합니다.

### 실전 예시 3: 작업 로그 자동 기록

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit|Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date '+%Y-%m-%d %H:%M:%S') - $CLAUDE_TOOL_NAME: $CLAUDE_TOOL_INPUT_FILE_PATH\" >> .claude/activity.log"
          }
        ]
      }
    ]
  }
}
```

**효과**: Claude의 모든 파일 작업이 로그에 기록됩니다.

---

## 3. CLAUDE.md 실전 작성법

프로젝트 루트의 `CLAUDE.md`는 Claude가 항상 참조하는 **프로젝트 헌법**입니다.

### 효과적인 CLAUDE.md 구조

```markdown
# 프로젝트명

## 프로젝트 개요
[2-3줄: 이 프로젝트가 무엇인지]

## 기술 스택
- Frontend: React 18 + TypeScript
- Backend: Node.js + Express
- DB: PostgreSQL
- 패키지 매니저: pnpm (npm, yarn 사용 금지)

## 코딩 컨벤션
- type 사용, interface 지양
- enum 금지 → string literal union 사용
- 함수형 컴포넌트만 사용

## 금지 사항
- console.log 남기지 말 것 (logger 사용)
- any 타입 사용 금지
- 외부 라이브러리 추가 시 먼저 논의

## 자주 쓰는 명령어
- 개발 서버: pnpm dev
- 테스트: pnpm test
- 빌드: pnpm build

## 주의사항
- DB 마이그레이션은 항상 백업 후 실행
- main 브랜치에 직접 push 금지
```

### CLAUDE.md 발전시키기

```
처음: 기본 기술 스택과 금지사항
  ↓ Claude가 실수할 때마다 규칙 추가
1개월 후: 팀의 모든 컨벤션이 담긴 문서
  ↓ 신규 팀원이 빠르게 적응
6개월 후: 살아있는 팀 지식 베이스
```

**핵심 원칙**: Claude가 같은 실수를 두 번 하면 CLAUDE.md에 추가하세요.

---

## 4. 권한 관리

### 권한 모드

| 모드 | 설명 | 사용 시 |
|------|------|---------|
| 기본 | 중요 작업 전 승인 요청 | 일반 개발 |
| `--auto-approve` | 파일 작업 자동 승인 | 신뢰하는 작업 |
| `--dangerously-skip-permissions` | 모든 작업 자동 승인 | 주의! |

### 신뢰 목록 설정

**.claude/settings.json**

```json
{
  "allowedTools": [
    "Read",
    "Write",
    "Edit",
    "Glob",
    "Grep"
  ],
  "deniedTools": [
    "Bash(rm -rf*)",
    "Bash(sudo*)"
  ]
}
```

---

## 실습

1. 프로젝트에 `.claude/commands/review.md` 파일 만들기
2. Claude Code에서 `/review` 실행해보기
3. `.claude/settings.local.json`에 PostToolUse Hook 추가해서 자동 포맷팅 설정

---

## 다음 단원

[07. MCP & 팀 최적화 →](../07-mcp-integration/README.md)
