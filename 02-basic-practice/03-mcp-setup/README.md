# 03. MCP 연결하기

> Claude를 Slack, Notion, GitHub 같은 도구와 직접 연결한다

---

## MCP란?

**MCP (Model Context Protocol)** = Claude가 외부 서비스와 직접 대화할 수 있게 해주는 연결 방식

### MCP 없을 때
```
나: Slack 메시지 내용을 붙여넣기 → Claude에게 질문 → 답변 복사 → Slack에 붙여넣기
    (모든 복붙 과정을 내가 직접)
```

### MCP 있을 때
```
나: "오늘 #공지 채널 내용을 요약해서 보고서로 만들어줘"
Claude: Slack 직접 읽기 → 요약 → 보고서 파일 생성
    (중간 과정 없이 한 번에)
```

---

## 연결 가능한 서비스

| 카테고리 | 서비스 |
|----------|--------|
| 커뮤니케이션 | Slack, Gmail, Google Calendar |
| 문서/협업 | Notion, Google Docs, Confluence |
| 개발 | GitHub, GitLab, Jira, Linear |
| 데이터 | Supabase, PostgreSQL, Airtable |
| 파일 | 로컬 파일 시스템, Google Drive |
| 브라우저 | 웹페이지 읽기, 스크린샷 |

---

## 실습 1: 파일 시스템 MCP (가장 쉬운 시작)

파일을 다루는 가장 기본적인 MCP입니다. 추가 계정 없이 바로 됩니다.

### 설정 방법

`.claude/settings.json` 파일 생성:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/your-name/Documents"
      ]
    }
  }
}
```

> `your-name` 부분을 본인 계정명으로 바꿔주세요.
> Mac에서 계정명 확인: 터미널에서 `whoami` 입력

### 사용해보기

Claude Code 실행 후:

```
Documents 폴더에서 지난달 작성한 파일들을 찾아서
파일명, 크기, 마지막 수정일을 표로 정리해줘.
```

---

## 실습 2: Notion MCP

Notion 페이지를 Claude가 직접 읽고 쓸 수 있게 됩니다.

### 준비물

1. Notion 계정
2. Notion API 키 발급

### Notion API 키 발급 방법

1. [notion.so/my-integrations](https://www.notion.so/my-integrations) 접속
2. "+ New integration" 클릭
3. 이름 입력 (예: "Claude 연동")
4. Submit → **Internal Integration Secret** 복사

5. 연결할 Notion 페이지 열기
6. 오른쪽 상단 `...` → Connections → 방금 만든 integration 선택

### 설정

`.claude/settings.json`:

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notionhq/mcp"],
      "env": {
        "NOTION_API_KEY": "여기에_복사한_키_입력"
      }
    }
  }
}
```

### 사용해보기

```
Notion에서 "회의록" 데이터베이스를 찾아서
이번 달 회의록들을 요약해줘.
```

```
오늘 회의 내용을 Notion "회의록" 데이터베이스에 새 페이지로 추가해줘.
내용: [회의 내용 입력]
```

---

## 실습 3: Slack MCP

Slack 메시지를 읽고, 요약하고, 보낼 수 있습니다.

### 준비물

- Slack 계정
- Slack Bot Token (워크스페이스 관리자 필요)

### Slack Bot Token 발급

1. [api.slack.com/apps](https://api.slack.com/apps) 접속
2. "Create New App" → "From scratch"
3. 앱 이름과 워크스페이스 선택
4. "OAuth & Permissions" → Scopes 추가:
   - `channels:read`, `channels:history`
   - `chat:write` (메시지 전송 필요 시)
5. "Install to Workspace" → 승인
6. **Bot User OAuth Token** 복사 (xoxb-로 시작)

### 설정

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "xoxb-여기에_토큰_입력",
        "SLACK_TEAM_ID": "워크스페이스_ID"
      }
    }
  }
}
```

> 워크스페이스 ID: Slack 웹에서 URL `https://app.slack.com/client/T12345ABCD/...`의 `T12345ABCD` 부분

### 사용해보기

```
오늘 #general 채널의 대화를 요약해줘.
중요한 결정 사항이나 액션 아이템이 있으면 강조해줘.
```

---

## 여러 MCP 동시 사용

여러 서비스를 한 번에 연결할 수 있습니다:

```json
{
  "mcpServers": {
    "filesystem": { ... },
    "notion": { ... },
    "slack": { ... }
  }
}
```

그러면 이런 것이 가능합니다:

```
오늘 Slack #프로젝트 채널에서 언급된 이슈들을 찾아서
Notion의 "이슈 트래킹" 데이터베이스에 추가해줘.
각 이슈마다 담당자, 우선순위, 설명을 포함해줘.
```

---

## 문제 해결

### "MCP server not found" 오류

Node.js가 설치되어 있는지 확인:
```bash
node --version
```
버전이 나오지 않으면 [nodejs.org](https://nodejs.org)에서 설치

### "권한 없음" 오류

API 키가 올바른지, 필요한 권한(Scope)이 있는지 확인

### 연결은 됐는데 동작 안 할 때

Claude에게 이렇게 물어보세요:
```
MCP가 연결됐는지 확인해줘.
어떤 도구들을 사용할 수 있어?
```

---

## 다음 단원

[04. Skill 만들기 →](../04-skills/README.md)
