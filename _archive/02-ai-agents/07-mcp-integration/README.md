# 07. MCP & 팀 최적화

> **개발자/팀 리더 심화** — MCP 설정은 개발 지식이 필요합니다.
> **팀 최적화(4번 섹션)** 는 비개발자도 참고할 수 있습니다.

---

> Claude를 외부 도구와 연결하고, 팀 전체가 AI를 활용하게 한다

---

## 1. MCP란? (Model Context Protocol)

**MCP**는 Claude가 외부 서비스와 직접 통신할 수 있게 해주는 프로토콜입니다.

```
기존 방식:
  사람 → Slack 열기 → 메시지 복사 → Claude에 붙여넣기 → 결과 복사 → Slack에 붙여넣기

MCP 방식:
  사람 → "어제 #개발팀 채널 요약해줘" → Claude가 직접 Slack 읽고 요약
```

### MCP로 연결 가능한 도구들

| 카테고리 | 도구 |
|----------|------|
| 커뮤니케이션 | Slack, Gmail, Google Calendar |
| 개발 | GitHub, Jira, Linear |
| 문서 | Notion, Confluence, Google Docs |
| 데이터 | Supabase, PostgreSQL, Snowflake |
| 디자인 | Figma, Canva |
| 브라우저 | 웹 크롤링, 스크린샷 |

---

## 2. MCP 설정하기

### 설정 파일 위치

```
~/.claude/mcp.json        # 전역 (모든 프로젝트)
your-project/.mcp.json    # 프로젝트별
```

### GitHub MCP 설정 예시

**.mcp.json**

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

설정 후 Claude Code에서:

```
오늘 우리 레포에 머지된 PR들을 요약해줘.
각 PR의 주요 변경사항과 작성자를 포함해서.
```

### Notion MCP 설정 예시

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notionhq/mcp"],
      "env": {
        "NOTION_API_KEY": "${NOTION_API_KEY}"
      }
    }
  }
}
```

### Slack MCP 설정 예시

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "${SLACK_BOT_TOKEN}",
        "SLACK_TEAM_ID": "${SLACK_TEAM_ID}"
      }
    }
  }
}
```

---

## 3. MCP 실전 활용 사례

### 사례 1: 데일리 스크럼 자동화

```
매일 오전 9시에 할 일:

GitHub에서 어제 닫힌 이슈와 오늘 마감 이슈를 가져와서
Slack #개발팀 채널의 어제 대화를 요약하고
오늘 스크럼 내용을 아래 형식으로 작성해줘:

어제 완료: ...
오늘 예정: ...
블로커: ...
```

### 사례 2: PR 코드 리뷰 보조

```
PR #123을 리뷰해줘.
코드 변경사항을 분석하고:
1. 버그 가능성
2. 성능 이슈
3. 테스트 누락 여부
를 GitHub 코멘트로 직접 달아줘.
```

### 사례 3: 문서 자동 동기화

```
방금 배포된 API 변경사항을 기반으로
Notion의 "API 문서" 페이지를 업데이트해줘.
```

---

## 4. 팀 최적화

### CLAUDE.md를 팀 자산으로 만들기

```
개인 CLAUDE.md → 팀 CLAUDE.md

1. Git으로 버전 관리
2. PR 리뷰 중 발견한 규칙을 CLAUDE.md에 추가
3. 새 팀원 온보딩 시 자동으로 AI 규칙 학습
4. 분기마다 CLAUDE.md 리뷰 & 정리
```

### GitHub Actions와 Claude 연동

PR에 `@claude` 멘션하면 자동으로 코드 리뷰:

**.github/workflows/claude-review.yml**

```yaml
name: Claude Code Review
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          trigger_phrase: "@claude"
```

### 팀 Claude 활용 성숙도 모델

```
Level 1: 개인이 각자 사용
Level 2: 공통 CLAUDE.md 도입
Level 3: 공통 커맨드 (.claude/commands/) 표준화
Level 4: CI/CD에 Claude 통합
Level 5: MCP로 사내 도구 연결
```

---

## 5. 보안 고려사항

### API 키 관리

```bash
# 절대 안 됨 - 코드에 직접 작성
ANTHROPIC_API_KEY=sk-ant-...  ← Git에 올리면 큰일

# 올바른 방법 - 환경 변수
export ANTHROPIC_API_KEY=sk-ant-...

# .gitignore에 추가
.env
.claude/settings.local.json  ← 개인 API 키 포함 가능
```

### MCP 권한 최소화 원칙

```
필요한 권한만 부여:
  GitHub: read-only (쓰기는 신중하게)
  Slack: 필요한 채널만
  DB: SELECT 전용 계정 사용
```

---

## 모듈 02 완료

Claude Code Agent 전체 내용을 마쳤습니다!

**학습 경로 요약:**
```
01. Agent 개념 이해
02. Claude Code 기본 Agent 활용
03. Subagent 패턴
04. Agent 설계 패턴
05. 멀티 에이전트 시스템
06. 자동화 (Hooks & Commands)  ← 방금 완료
07. MCP & 팀 최적화            ← 지금 여기
```

**다음 모듈:** [모듈 03: AI 워크플로우 →](../../03-ai-workflow/README.md)
