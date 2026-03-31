# practice_adv.html 실습 강화 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** `practice_adv.html`에 실습 슬라이드 6개 추가 및 Skills 슬라이드 강화로 파트별 30분 실습을 지원

**Architecture:** 단일 HTML 파일(`practice_adv.html`) 수정. 기존 슬라이드 사이에 HTML 블록 삽입 후 `simpleToc` 인덱스 전체 재조정. 기존 CSS 클래스 재사용, 신규 CSS 없음.

**Tech Stack:** HTML/CSS/JS (단일 파일), 기존 클래스: `code-block`, `workflow`, `strategy-list`, `compare-grid`, `warn-box`, `stat-grid`, `quote-box`, `principle-grid`

---

## 파일 변경 맵

| 파일 | 변경 유형 | 내용 |
|------|---------|------|
| `01-general/practice_adv.html` | Modify | 슬라이드 6개 삽입 + Skills 슬라이드 강화 + simpleToc 재조정 |

### 삽입 후 슬라이드 인덱스 (총 30개, 기존 24개)

| 인덱스 | 슬라이드 | 변경 |
|--------|---------|------|
| 0 | 커버 | 유지 |
| 1 | 목차 | 유지 |
| 2 | 섹션1 divider | 유지 |
| 3 | 컨텍스트 관리 | 유지 |
| 4 | Context Rot | 유지 |
| 5 | OpenClaw | 유지 |
| 6 | Harness | 유지 |
| 7 | Paperclip | 유지 |
| **8** | **[NEW] CLAUDE.md 작성 실습** | **신규** |
| 9 | 섹션2 divider | 유지 (was 8) |
| 10 | MCP 개요 | 유지 (was 9) |
| 11 | Stitch MCP | 유지 (was 10) |
| 12 | Supabase MCP | 유지 (was 11) |
| **13** | **[NEW] Supabase MCP 실습** | **신규** |
| 14 | 섹션3 divider | 유지 (was 12) |
| 15 | Skills 개념 | 유지 (was 13) |
| 16 | Skills 실습 | 강화 (was 14) |
| 17 | 섹션4 divider | 유지 (was 15) |
| 18 | Agent Team 개념 | 유지 (was 16) |
| 19 | 오케스트레이션 패턴 | 유지 (was 17) |
| 20 | Agent Team 실습 | 유지 (was 18) |
| **21** | **[NEW] Agent Team 설계 실습** | **신규** |
| 22 | 섹션5 divider | 유지 (was 19) |
| 23 | 서비스 기획 프레임워크 | 유지 (was 20) |
| **24** | **[NEW] 기획 워크시트** | **신규** |
| 25 | 구현 가이드 & 체크리스트 | 유지 (was 21) |
| **26** | **[NEW] 30분 구현 타임박스** | **신규** |
| 27 | 발표 구성 & 평가 기준 | 유지 (was 22) |
| **28** | **[NEW] 발표 스크립트 템플릿** | **신규** |
| 29 | 마무리 | 유지 (was 23) |

---

## Task 1: Skills 실습 슬라이드에 weekly-report 완성 예시 추가

**Files:**
- Modify: `01-general/practice_adv.html` (Skills 실습 슬라이드, 기존 slide 14)

- [ ] **Step 1: 기존 Skills 실습 슬라이드의 quote-box 찾기**

`practice_adv.html`에서 아래 텍스트를 검색:
```
실습 과제:</strong> 본인 업무에서 반복하는 작업 1가지를 Skill로 만들어보기
```

- [ ] **Step 2: quote-box 바로 뒤에 code-block 삽입**

아래 HTML을 `</div>\n    </div>\n    </div>\n\n    <!-- ─── 섹션 4` 바로 앞에 삽입:

```html
        <div class="code-block" style="margin-top:8px;">
          <div class="code-label">완성 예시 — .claude/commands/weekly-report.md</div>
          <code><span class="ky">---</span></code>
          <code><span class="ky">name:</span> <span class="st">weekly-report</span></code>
          <code><span class="ky">description:</span> <span class="st">이번 주 업무 내용을 보고서 형식으로 정리</span></code>
          <code><span class="ky">---</span></code>
          <code><span class="cm"># 주간 업무 보고서 작성</span></code>
          <code><span class="st">아래 형식으로 이번 주 완료한 업무를 정리해줘:</span></code>
          <code><span class="st">1. 완료 업무 (3가지 이내)</span></code>
          <code><span class="st">2. 진행 중인 업무</span></code>
          <code><span class="st">3. 다음 주 계획</span></code>
          <code><span class="st">4. 이슈 / 요청 사항</span></code>
        </div>
```

- [ ] **Step 3: 브라우저에서 확인**

`01-general/practice_adv.html`을 브라우저로 열어 Skills 실습 슬라이드에 code-block이 추가되었는지 확인.

- [ ] **Step 4: 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: Skills 실습 슬라이드에 weekly-report 완성 예시 추가"
```

---

## Task 2: 1부 끝 — CLAUDE.md 작성 실습 슬라이드 추가

**Files:**
- Modify: `01-general/practice_adv.html` (Paperclip 슬라이드 뒤, 섹션2 divider 앞)

- [ ] **Step 1: 삽입 위치 확인**

`practice_adv.html`에서 아래 주석을 찾기:
```
<!-- ─── 섹션 2 ─── -->
```

- [ ] **Step 2: 섹션2 divider 바로 앞에 슬라이드 삽입**

```html
    <!-- 1부 실습: CLAUDE.md 작성해보기 -->
    <div class="slide-card" data-section="s1">
      <div class="slide-section-badge">1부 실습</div>
      <h2>즉시 실습: CLAUDE.md <span class="accent">직접 작성</span></h2>
      <div class="slide-body">
        <div class="code-block" style="margin-bottom:10px;">
          <div class="code-label">나의 CLAUDE.md 템플릿 — 빈 칸을 채워보세요</div>
          <code><span class="ky"># 나의 프로젝트</span></code>
          <code></code>
          <code><span class="ky">## 프로젝트 목적</span></code>
          <code><span class="st">[내가 만들려는 것을 한 줄로 설명]</span></code>
          <code></code>
          <code><span class="ky">## 기술 스택</span></code>
          <code><span class="st">[사용할 도구: Lovable / Claude Code / MCP 등]</span></code>
          <code></code>
          <code><span class="ky">## 금지 사항</span></code>
          <code><span class="st">- [AI에게 하지 말라고 할 것 1가지]</span></code>
        </div>
        <div class="workflow">
          <div class="workflow-step"><div class="w-step">Step 1</div><div class="w-text">위 템플릿을 채워 프로젝트 루트에 <code style="background:#f0f0f0;padding:1px 5px;border-radius:3px;font-family:monospace;">CLAUDE.md</code> 파일로 저장</div></div>
          <div class="workflow-step"><div class="w-step">Step 2</div><div class="w-text">Claude Code 실행 → <code style="background:#f0f0f0;padding:1px 5px;border-radius:3px;font-family:monospace;">/clear</code> 입력으로 이전 컨텍스트 정리</div></div>
          <div class="workflow-step highlight"><div class="w-step">Step 3</div><div class="w-text">첫 번째 질문 입력 → CLAUDE.md 내용이 자동으로 참조되는지 확인</div></div>
        </div>
        <div class="quote-box" style="margin-top:8px;">
          <p>"CLAUDE.md 한 장이 100번의 반복 설명을 대체합니다"</p>
        </div>
      </div>
    </div>

```

- [ ] **Step 3: 브라우저에서 확인**

슬라이드 8번이 CLAUDE.md 실습 슬라이드인지 확인. 좌측 TOC는 아직 업데이트 전이라 인덱스 불일치 상태 — Task 6에서 수정.

- [ ] **Step 4: 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: 1부 끝 CLAUDE.md 작성 실습 슬라이드 추가"
```

---

## Task 3: 2부 끝 — Supabase MCP 실습 슬라이드 추가

**Files:**
- Modify: `01-general/practice_adv.html` (Supabase MCP 슬라이드 뒤, 섹션3 divider 앞)

- [ ] **Step 1: 삽입 위치 확인**

`practice_adv.html`에서 아래 주석을 찾기:
```
<!-- ─── 섹션 3 ─── -->
```

- [ ] **Step 2: 섹션3 divider 바로 앞에 슬라이드 삽입**

```html
    <!-- 2부 실습: Supabase MCP 연결하기 -->
    <div class="slide-card" data-section="s2">
      <div class="slide-section-badge">2부 실습</div>
      <h2>즉시 실습: Supabase MCP <span class="accent">연결 따라하기</span></h2>
      <div class="slide-body">
        <div class="code-block" style="margin-bottom:10px;">
          <div class="code-label">.mcp.json — 아래 내용을 프로젝트 루트에 저장</div>
          <code><span class="ky">{</span></code>
          <code>&nbsp;&nbsp;<span class="ky">"mcpServers"</span><span class="ky">: {</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"supabase"</span><span class="ky">: {</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"command"</span><span class="ky">:</span> <span class="st">"npx"</span><span class="ky">,</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"args"</span><span class="ky">: [</span><span class="st">"-y"</span><span class="ky">,</span> <span class="st">"@supabase/mcp-server-supabase@latest"</span><span class="ky">,</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"--supabase-url"</span><span class="ky">,</span> <span class="st">"YOUR_PROJECT_URL"</span><span class="ky">,</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"--supabase-api-key"</span><span class="ky">,</span> <span class="st">"YOUR_ANON_KEY"</span><span class="ky">]</span></code>
          <code>&nbsp;&nbsp;&nbsp;&nbsp;<span class="ky">}</span></code>
          <code>&nbsp;&nbsp;<span class="ky">}</span></code>
          <code><span class="ky">}</span></code>
        </div>
        <div class="workflow">
          <div class="workflow-step"><div class="w-step">Step 1</div><div class="w-text">Supabase → Settings → API에서 Project URL + anon key 복사</div></div>
          <div class="workflow-step"><div class="w-step">Step 2</div><div class="w-text">YOUR_PROJECT_URL, YOUR_ANON_KEY 교체 후 <code style="background:#f0f0f0;padding:1px 5px;border-radius:3px;font-family:monospace;">.mcp.json</code>으로 저장</div></div>
          <div class="workflow-step highlight"><div class="w-step">Step 3</div><div class="w-text">Claude Code 재시작 → <strong>"테이블 목록 보여줘"</strong> 입력해보기</div></div>
        </div>
        <div class="warn-box" style="margin-top:8px;">⚠ API 키는 <code style="background:#fff3d4;padding:1px 5px;border-radius:3px;font-family:monospace;">.gitignore</code>에 추가하거나 환경변수로 분리하세요</div>
      </div>
    </div>

```

- [ ] **Step 3: 브라우저에서 확인**

슬라이드 13번이 Supabase MCP 실습 슬라이드인지 확인.

- [ ] **Step 4: 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: 2부 끝 Supabase MCP 연결 실습 슬라이드 추가"
```

---

## Task 4: 4부 끝 — Agent Team 설계 실습 슬라이드 추가

**Files:**
- Modify: `01-general/practice_adv.html` (Agent Team 실습 슬라이드 뒤, 섹션5 divider 앞)

- [ ] **Step 1: 삽입 위치 확인**

`practice_adv.html`에서 아래 주석을 찾기:
```
<!-- ─── 섹션 5 ─── -->
```

- [ ] **Step 2: 섹션5 divider 바로 앞에 슬라이드 삽입**

```html
    <!-- 4부 실습: 내 Agent Team 설계하기 -->
    <div class="slide-card" data-section="s4">
      <div class="slide-section-badge">4부 실습</div>
      <h2>즉시 실습: 내 <span class="accent">Agent Team</span> 설계하기</h2>
      <div class="slide-body">
        <div class="principle-grid" style="margin-bottom:10px;">
          <div class="principle-item">
            <div class="p-num">에이전트 1</div>
            <div class="p-title">[역할 이름]</div>
            <div class="p-desc">[담당 업무를 한 줄로]<br><em style="font-size:10px;color:#aaa;">예: 리서치 에이전트 — 최신 정보 3가지 수집</em></div>
          </div>
          <div class="principle-item">
            <div class="p-num">에이전트 2</div>
            <div class="p-title">[역할 이름]</div>
            <div class="p-desc">[담당 업무를 한 줄로]<br><em style="font-size:10px;color:#aaa;">예: 작성 에이전트 — 수집 결과로 초안 작성</em></div>
          </div>
          <div class="principle-item">
            <div class="p-num">오케스트레이션</div>
            <div class="p-title">패턴 선택</div>
            <div class="p-desc">Sequential / Parallel / Evaluator<br><em style="font-size:10px;color:#aaa;">위 에이전트들을 어떤 순서·방식으로 조율?</em></div>
          </div>
          <div class="principle-item">
            <div class="p-num">Claude Code 실행</div>
            <div class="p-title">위 설계를 그대로 입력</div>
            <div class="p-desc"><code style="background:#f0f0f0;padding:1px 4px;border-radius:3px;font-family:monospace;font-size:11px;">"Agent tool로 팀 구성해줘: 1. [에이전트1 역할] 2. [에이전트2 역할]"</code></div>
          </div>
        </div>
        <div class="quote-box">
          <p>팀 설계가 먼저, 코딩은 AI가 — <strong>당신의 역할은 오케스트레이터</strong></p>
        </div>
      </div>
    </div>

```

- [ ] **Step 3: 브라우저에서 확인**

슬라이드 21번이 Agent Team 설계 실습 슬라이드인지 확인.

- [ ] **Step 4: 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: 4부 끝 Agent Team 설계 실습 슬라이드 추가"
```

---

## Task 5: 5부 실습 슬라이드 3장 추가

**Files:**
- Modify: `01-general/practice_adv.html` (5부 각 슬라이드 뒤에 1장씩)

- [ ] **Step 1: 기획 워크시트 삽입 위치 확인**

`practice_adv.html`에서 아래 주석을 찾기:
```
<!-- 14. 구현 가이드 -->
```

- [ ] **Step 2: 구현 가이드 슬라이드 바로 앞에 기획 워크시트 삽입**

```html
    <!-- 5부 실습: 나의 서비스 기획 워크시트 -->
    <div class="slide-card" data-section="s5">
      <div class="slide-section-badge">5부 실습</div>
      <h2>나의 서비스 <span class="accent">기획 워크시트</span></h2>
      <div class="slide-body">
        <div class="strategy-list">
          <div class="strategy-item">
            <div class="s-num">1</div>
            <div class="s-content">
              <div class="s-title">문제 정의</div>
              <div class="s-desc">"나는 <strong>[&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]</strong>이 반복되어 귀찮다"</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num">2</div>
            <div class="s-content">
              <div class="s-title">솔루션</div>
              <div class="s-desc">"<strong>[도구]</strong>로 <strong>[기능]</strong>을 만들어 <strong>[시간/노력]</strong>을 줄인다"</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num">3</div>
            <div class="s-content">
              <div class="s-title">MVP 범위</div>
              <div class="s-desc">"오늘 만들 딱 하나 → <strong>[&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]</strong>"</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num">4</div>
            <div class="s-content">
              <div class="s-title">사용 도구 선택</div>
              <div class="s-desc" style="display:flex;gap:8px;flex-wrap:wrap;">
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">Lovable</span>
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">AI Studio</span>
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">Claude Code</span>
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">MCP</span>
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">Skills</span>
                <span style="background:#f8f4ff;border:1px solid #ddd6fe;border-radius:4px;padding:3px 10px;font-size:12px;">Agent Team</span>
              </div>
            </div>
          </div>
        </div>
        <div class="quote-box" style="margin-top:8px;">
          <p>"MVP는 작을수록 좋다. 오늘 30분 안에 <strong>동작하는 것 하나</strong>만."</p>
        </div>
      </div>
    </div>

```

- [ ] **Step 3: 30분 구현 타임박스 삽입 위치 확인**

아래 주석을 찾기:
```
<!-- 15. 발표 기준 -->
```

- [ ] **Step 4: 발표 기준 슬라이드 바로 앞에 30분 타임박스 삽입**

```html
    <!-- 5부 실습: 30분 구현 타임박스 -->
    <div class="slide-card" data-section="s5">
      <div class="slide-section-badge">5부 실습</div>
      <h2>30분 <span class="accent">구현 타임박스</span></h2>
      <div class="slide-body">
        <div class="stat-grid" style="margin-bottom:10px;">
          <div class="stat-item">
            <div class="num" style="font-size:18px;">0~10분</div>
            <div class="desc">CLAUDE.md 작성 + 첫 프롬프트 실행<br><em style="font-size:10px;">화면에 뭔가 나오면 성공</em></div>
          </div>
          <div class="stat-item">
            <div class="num" style="font-size:18px;">10~20분</div>
            <div class="desc">핵심 기능 1개 작동 확인<br><em style="font-size:10px;">안 되면 더 작게 쪼개기</em></div>
          </div>
          <div class="stat-item">
            <div class="num" style="font-size:18px;">20~30분</div>
            <div class="desc">데모 화면 정리<br>발표 문장 2줄 작성</div>
          </div>
        </div>
        <div class="compare-grid">
          <div class="compare-card before">
            <div class="label">막혔을 때</div>
            <p style="font-size:12px;">에러 메시지 복사 + <strong>"기대 결과는 이것"</strong>을 함께 전달<br><br>3번 이상 같은 에러 → <code style="background:#f0f0f0;padding:1px 4px;border-radius:3px;font-family:monospace;">/clear</code> 후 새 접근</p>
          </div>
          <div class="compare-card after">
            <div class="label">시간이 남으면</div>
            <p style="font-size:12px;">디자인 개선<br>기능 1개 추가<br>Skills로 반복 동작 자동화</p>
          </div>
        </div>
        <div class="warn-box" style="margin-top:8px;">⚠ 완성보다 동작이 우선 — 일부만 되어도 발표 가능합니다</div>
      </div>
    </div>

```

- [ ] **Step 5: 발표 스크립트 템플릿 삽입 위치 확인**

아래 주석을 찾기:
```
<!-- 16. 마무리 -->
```

- [ ] **Step 6: 마무리 슬라이드 바로 앞에 발표 스크립트 템플릿 삽입**

```html
    <!-- 5부 실습: 5분 발표 스크립트 템플릿 -->
    <div class="slide-card" data-section="s5">
      <div class="slide-section-badge">5부 실습</div>
      <h2>발표 <span class="accent">스크립트 템플릿</span></h2>
      <div class="slide-body">
        <div class="strategy-list">
          <div class="strategy-item">
            <div class="s-num" style="background:#f59e0b;color:#000;">①</div>
            <div class="s-content">
              <div class="s-title">문제 & 동기 <em style="font-size:11px;font-weight:400;color:#888;">(30초)</em></div>
              <div class="s-desc">"저는 <strong>[문제/불편함]</strong>이 있어서 이걸 만들었습니다."</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num" style="background:#f59e0b;color:#000;">②</div>
            <div class="s-content">
              <div class="s-title">라이브 데모 <em style="font-size:11px;font-weight:400;color:#888;">(2분)</em></div>
              <div class="s-desc">실제 작동하는 화면 직접 시연 — 안 되면 만드는 과정 화면으로 대체 가능</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num" style="background:#f59e0b;color:#000;">③</div>
            <div class="s-content">
              <div class="s-title">기술 설명 <em style="font-size:11px;font-weight:400;color:#888;">(1분)</em></div>
              <div class="s-desc">"<strong>[도구명]</strong>과 <strong>[기법]</strong>을 사용했고, <strong>[어려웠던 점]</strong>은 <strong>[이렇게]</strong> 해결했습니다."</div>
            </div>
          </div>
          <div class="strategy-item">
            <div class="s-num" style="background:#f59e0b;color:#000;">④</div>
            <div class="s-content">
              <div class="s-title">배운 점 & 계획 <em style="font-size:11px;font-weight:400;color:#888;">(30초)</em></div>
              <div class="s-desc">"앞으로 <strong>[실무 적용 계획]</strong>에 활용할 예정입니다."</div>
            </div>
          </div>
        </div>
        <div class="quote-box" style="margin-top:8px;">
          <p>"동작하지 않아도 괜찮습니다. <strong>과정과 배운 점</strong>이 발표의 핵심입니다."</p>
        </div>
      </div>
    </div>

```

- [ ] **Step 7: 브라우저에서 5부 슬라이드 3장 모두 확인**

슬라이드 24(기획 워크시트), 26(타임박스), 28(스크립트 템플릿) 확인.

- [ ] **Step 8: 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: 5부 실습 슬라이드 3장 추가 (기획 워크시트, 타임박스, 스크립트)"
```

---

## Task 6: simpleToc 전체 재조정

**Files:**
- Modify: `01-general/practice_adv.html` (JS의 `simpleToc` 배열)

- [ ] **Step 1: 기존 simpleToc 배열 전체를 아래 내용으로 교체**

`const simpleToc = [` 부터 `];` 까지를 아래로 교체:

```javascript
const simpleToc = [
  { num: '01', text: '표지', slide: 0 },
  { num: '02', text: '실습 목차', slide: 1 },
  { divider: '1부: 바이브 코딩 트랜드' },
  { num: '03', text: '컨텍스트 관리 전략', slide: 3 },
  { num: '04', text: 'Context Rot', slide: 4 },
  { num: '05', text: 'OpenClaw', slide: 5 },
  { num: '06', text: 'Harness', slide: 6 },
  { num: '07', text: 'Paperclip', slide: 7 },
  { num: '실습', text: 'CLAUDE.md 작성 실습', slide: 8 },
  { divider: '2부: MCP' },
  { num: '08', text: 'MCP 개요 — AI의 USB', slide: 10 },
  { num: '09', text: 'Stitch MCP', slide: 11 },
  { num: '10', text: 'Supabase MCP', slide: 12 },
  { num: '실습', text: 'Supabase MCP 실습', slide: 13 },
  { divider: '3부: Skills' },
  { num: '11', text: 'Skills 구조와 작동', slide: 15 },
  { num: '12', text: 'Skills 실습', slide: 16 },
  { divider: '4부: Agent Team' },
  { num: '13', text: 'Agent Team 개념', slide: 18 },
  { num: '14', text: '오케스트레이션 패턴', slide: 19 },
  { num: '15', text: 'Agent Team 실습', slide: 20 },
  { num: '실습', text: 'Agent Team 설계 실습', slide: 21 },
  { divider: '5부: 서비스 만들기' },
  { num: '16', text: '서비스 기획 프레임워크', slide: 23 },
  { num: '실습', text: '기획 워크시트', slide: 24 },
  { num: '17', text: '구현 가이드 & 체크리스트', slide: 25 },
  { num: '실습', text: '30분 구현 타임박스', slide: 26 },
  { num: '18', text: '발표 구성 & 평가 기준', slide: 27 },
  { num: '실습', text: '발표 스크립트 템플릿', slide: 28 },
  { num: '19', text: '마무리', slide: 29 },
];
```

- [ ] **Step 2: 브라우저에서 전체 TOC 동작 확인**

좌측 사이드바에서 각 항목 클릭 시 해당 슬라이드로 이동하는지 확인.
총 슬라이드 카운터가 `1 / 30`으로 표시되는지 확인.

- [ ] **Step 3: 최종 커밋**

```bash
git add 01-general/practice_adv.html
git commit -m "feat: simpleToc 인덱스 재조정 — 총 30 슬라이드"
```

---

## Self-Review 결과

**스펙 커버리지 체크:**
- ✅ 신규 1 (CLAUDE.md 실습) → Task 2
- ✅ 신규 2 (Supabase MCP 실습) → Task 3
- ✅ 신규 3 (Agent Team 설계) → Task 4
- ✅ 신규 4 (기획 워크시트) → Task 5 Step 2
- ✅ 신규 5 (30분 타임박스) → Task 5 Step 4
- ✅ 신규 6 (발표 스크립트) → Task 5 Step 6
- ✅ Skills 실습 강화 → Task 1
- ✅ simpleToc 재조정 → Task 6

**플레이스홀더:** 없음. 모든 HTML 코드 완성본 포함.

**타입 일관성:** HTML 클래스명 — `slide-section-badge`, `code-block`, `workflow`, `workflow-step`, `w-step`, `w-text`, `highlight`, `quote-box`, `warn-box`, `strategy-list`, `strategy-item`, `s-num`, `s-content`, `s-title`, `s-desc`, `stat-grid`, `stat-item`, `compare-grid`, `compare-card`, `principle-grid`, `principle-item` — 모두 기존 파일에 정의된 클래스만 사용.
