# 01. 환경 설정

> Claude Code를 설치하고 첫 번째 대화를 시작한다

---

## Claude Code란?

**Claude Code** = 내 컴퓨터 파일에 직접 접근해서 작업하는 AI 도구

- 파일 읽기, 쓰기, 수정 가능
- 폴더 안 파일 전체를 한 번에 처리
- 웹 검색 후 결과 파일로 저장

---

## 설치 전 필요한 것

### 1. Node.js 설치

Claude Code는 Node.js 위에서 동작합니다.

**확인 방법** (이미 설치됐는지 확인):
- Mac: 터미널 열기 → `node --version` 입력 → 버전 숫자 나오면 설치됨
- Windows: PowerShell 열기 → `node --version` 입력

**없으면 설치:**
1. [nodejs.org](https://nodejs.org) 접속
2. **LTS 버전** 다운로드 클릭 (왼쪽 버튼)
3. 설치 파일 실행 → 기본 옵션으로 설치

> **터미널(Terminal) 여는 방법**
> - Mac: Spotlight 검색(Cmd+Space) → "Terminal" 입력 → Enter
> - Windows: 시작 → "PowerShell" 검색 → 실행

---

## Claude Code 설치

터미널에 아래를 한 줄씩 입력합니다:

```bash
npm install -g @anthropic-ai/claude-code
```

설치 완료 확인:
```bash
claude --version
```

버전 숫자가 나오면 성공입니다.

---

## 계정 연결

```bash
claude
```

처음 실행하면 로그인 화면이 나옵니다:
1. 브라우저가 자동으로 열리거나, 링크를 복사해서 브라우저에 붙여넣기
2. [claude.ai](https://claude.ai) 계정으로 로그인
3. 터미널로 돌아오면 연결 완료

---

## 첫 번째 실습

### 작업 폴더 만들기

```bash
mkdir my-first-project
cd my-first-project
claude
```

### 대화 시작

Claude Code가 실행되면 대화창이 나타납니다.
입력해보세요:

```
안녕! 이 폴더에 간단한 TODO 앱 HTML 파일을 만들어줘.
항목 추가, 완료 체크, 삭제 기능이 있어야 해.
```

잠시 후 `index.html` 파일이 생성됩니다.
파일을 브라우저로 열어보세요.

---

## Claude Code 기본 명령어

| 상황 | 입력 |
|------|------|
| 대화 종료 | `Ctrl + C` 또는 `/exit` |
| 이전 대화 이어서 | `claude --continue` |
| 도움말 | `/help` |
| 파일 목록 보기 | `/ls` |

---

## 문제 해결

### "command not found: claude"

Node.js 설치 후 터미널을 새로 열고 다시 시도해보세요.

### 설치 중 에러가 날 때

```bash
sudo npm install -g @anthropic-ai/claude-code
```

비밀번호 입력 후 다시 시도 (Mac)

### 로그인이 안 될 때

Claude 계정이 있는지 확인하고, [claude.ai](https://claude.ai)에서 직접 로그인 테스트해보세요.

---

## 다음 단원

[02. Claude Code 기초 →](../02-claude-code-basics/README.md)
