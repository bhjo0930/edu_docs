# 02. 실전 프로젝트: 자동 일일 브리핑 시스템

> 매일 아침 팀에게 전달되는 브리핑을 AI 에이전트팀이 자동으로 만든다

---

## 프로젝트 개요

**목표**: 매일 아침 9시, 팀장에게 자동으로 전달되는 종합 브리핑 생성

**포함 내용**:
- 어제 팀의 GitHub/Jira 업무 현황
- Slack 주요 대화 요약
- 오늘 캘린더 일정
- 주요 알림 및 블로커

**가치**: 매일 30~60분 소요되는 현황 파악 작업을 자동화

---

## 에이전트팀 설계

```
[Orchestrator: BriefingDirector]
  - 전체 브리핑 구조 관리
  - Worker들에게 수집 지시
  - 최종 브리핑 문서 통합
        ↓ 동시 실행
┌───────────────────────────────────────┐
│ [SlackAgent]  │ [CalendarAgent] │ [TaskAgent] │
│ Slack 채널    │ Google Calendar │ GitHub/Jira │
│ 요약          │ 오늘 일정       │ 업무 현황   │
└───────────────────────────────────────┘
        ↓ 결과 통합
[Writer: BriefingWriter]
  - 수집된 정보를 읽기 좋은 브리핑으로 작성
        ↓
[Distributor]
  - Slack #경영진 채널에 전송
  - 이메일 발송
```

---

## Step 1: 프로젝트 폴더 구성

```bash
mkdir daily-briefing
cd daily-briefing
```

폴더 구조:
```
daily-briefing/
├── CLAUDE.md              ← 프로젝트 지시사항
├── .claude/
│   ├── settings.json      ← MCP 설정
│   └── commands/
│       └── briefing.md    ← /briefing 커맨드
├── agents/
│   ├── orchestrator.md    ← Orchestrator 지시사항
│   ├── slack-agent.md     ← Slack 수집 Agent
│   ├── calendar-agent.md  ← 캘린더 Agent
│   └── writer.md          ← 브리핑 작성 Agent
└── output/                ← 생성된 브리핑 저장
```

---

## Step 2: CLAUDE.md 작성

**CLAUDE.md**

```markdown
# Daily Briefing System

## 프로젝트 목적
매일 아침 팀장을 위한 종합 브리핑을 자동 생성한다.

## 브리핑 시간
매일 오전 9:00

## 대상
팀장 및 주요 의사결정자

## 브리핑 구성
1. 어제 완료된 주요 업무
2. 오늘 예정 일정
3. 블로커 및 주요 이슈
4. 팀 분위기/특이사항

## 톤
간결하고 실용적으로. 경영진이 5분 안에 읽을 수 있도록.
```

---

## Step 3: MCP 설정

**.claude/settings.json**

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
    },
    "google-calendar": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-google-calendar"],
      "env": {
        "GOOGLE_CLIENT_ID": "${GOOGLE_CLIENT_ID}",
        "GOOGLE_CLIENT_SECRET": "${GOOGLE_CLIENT_SECRET}"
      }
    },
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "./output"
      ]
    }
  }
}
```

---

## Step 4: Skill 작성

**.claude/commands/briefing.md**

```markdown
오늘의 일일 브리핑을 생성해줘.

다음 단계로 진행해줘:

1. **정보 수집** (병렬로 처리)
   - Slack: 어제 #팀전체, #개발팀, #긴급공지 채널 수집
   - Calendar: 오늘 등록된 모든 일정
   - (GitHub/Jira가 연결됐다면 어제 완료/오픈된 이슈)

2. **브리핑 작성**
   아래 형식으로 작성:

   ---
   # 일일 브리핑 — {날짜}

   ## 📌 핵심 요약 (3줄 이내)

   ## ✅ 어제 완료된 일

   ## 📅 오늘 주요 일정

   ## ⚠️ 블로커 & 이슈

   ## 💬 팀 현황
   ---

3. **저장**
   output/briefing-{날짜}.md 로 저장

생성 완료 후 "브리핑이 완성됐습니다. output 폴더를 확인해주세요." 알려줘.
```

---

## Step 5: 실행 및 테스트

```bash
claude
```

```
/briefing
```

처음 실행 시 어떤 채널들이 있는지 확인하고 채널명을 조정해보세요.

---

## Step 6: 고도화 아이디어

### 자동 전송 추가

Slack으로 자동 전송하는 기능 추가:

```
브리핑 작성이 완료되면 Slack #경영진-브리핑 채널에 전송해줘.
전송 형식: 마크다운으로 포맷팅해서 보기 좋게.
```

### 우선순위 판단 추가

```
수집된 이슈 중에서 오늘 당장 처리해야 할 것과
나중에 해도 되는 것을 구분해줘.
판단 기준: 마감일, 영향 범위, 관련 인원
```

### 주간 요약 추가

매주 금요일에는:

```
이번 주 브리핑 5개를 요약해서
주간 리뷰 보고서를 만들어줘.
```

---

## 다음 단원

[03. 실전 프로젝트: 고객 응대 자동화 →](../03-project-customer/README.md)
