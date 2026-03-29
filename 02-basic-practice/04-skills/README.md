# 04. Skill 만들기 — 반복 작업을 한 줄로

> 자주 쓰는 긴 지시를 `/명령어` 하나로 저장한다

---

## Skill이란?

**Skill** = 자주 쓰는 프롬프트를 저장해두고 짧은 명령어로 실행하는 기능

```
Skill 없을 때:
  매번 입력: "현재 변경된 파일들을 검토해줘.
              보안 취약점, 성능 문제, 가독성 순으로
              각 이슈의 심각도(상/중/하)와 줄 번호를 표시해줘."

Skill 있을 때:
  /review 만 입력하면 위 내용이 자동 실행
```

---

## Skill 파일 위치

```
your-project/
└── .claude/
    └── commands/
        ├── review.md        → /review
        ├── summary.md       → /summary
        └── brief.md         → /brief
```

파일 이름이 명령어가 됩니다.

---

## 실습 1: 첫 번째 Skill 만들기

### 폴더 만들기

```bash
mkdir -p .claude/commands
```

### Skill 파일 작성

**.claude/commands/summary.md**

```markdown
현재 프로젝트의 주요 내용을 요약해줘.

포함할 내용:
1. 전체 구조 (폴더/파일 구성)
2. 최근 변경된 파일 목록
3. 주요 기능 3가지

한국어로, 3분 안에 읽을 수 있는 분량으로 작성해줘.
```

### 사용해보기

Claude Code에서:
```
/summary
```

---

## 업무별 Skill 예시

### 마케팅/기획용

**.claude/commands/content-brief.md**

```markdown
콘텐츠 기획서 초안을 작성해줘.

아래 폴더에서 관련 자료를 먼저 찾아봐:
- docs/references/
- docs/brand-guide/

기획서 구조:
1. 콘텐츠 목적 및 타깃
2. 핵심 메시지 3가지
3. 채널별 포맷 제안 (SNS, 블로그, 이메일)
4. 참고할 레퍼런스

브랜드 톤앤매너: 전문적이지만 친근하게
```

사용:
```
/content-brief
그리고 이번 달 캠페인 주제는 "여름 할인 프로모션"이야.
```

---

**.claude/commands/meeting-notes.md**

```markdown
방금 회의 내용을 정리해줘.

형식:
## 회의 요약
- 날짜:
- 참석자:
- 주요 논의 내용 (3~5줄)

## 결정 사항
(번호 목록)

## 액션 아이템
| 담당자 | 할 일 | 기한 |

회의 내용은 내가 아래에 붙여넣을게.
```

---

### HR/총무용

**.claude/commands/jd.md**

```markdown
채용 공고(Job Description)를 작성해줘.

다음 정보를 먼저 알려줘:
1. 포지션 이름
2. 팀/부서
3. 주요 업무 (내가 입력하면 다듬어줘)
4. 자격 요건

형식:
- 회사 소개 (2~3줄, 간결하게)
- 포지션 소개
- 주요 업무
- 자격 요건 (필수 / 우대)
- 복리후생

친근하면서도 전문적인 톤으로 작성해줘.
```

---

### 영업용

**.claude/commands/proposal.md**

```markdown
제안서 초안을 만들어줘.

고객사 정보:
- 회사명:
- 업종:
- 담당자:
- 주요 니즈/문제:

제안 구조:
1. 현황 파악 (고객 문제 공감)
2. 제안 솔루션 (우리 강점 포함)
3. 예상 효과 (수치 포함)
4. 추진 일정
5. 가격 및 조건

설득력 있고 간결하게, A4 2~3장 분량으로 작성해줘.
```

---

## 더 강력한 Skill: 파라미터 사용

Skill에 변수를 추가해서 상황에 맞게 쓸 수 있습니다:

**.claude/commands/translate.md**

```markdown
아래 내용을 번역해줘.

번역 방향: 한국어 → 영어
톤: 비즈니스 공식 문서 스타일
주의사항:
- 전문 용어는 원문 병기
- 이메일 형식이면 이메일 형식 유지

번역할 내용은 내가 아래에 붙여넣을게.
```

사용:
```
/translate
[번역할 내용 붙여넣기]
```

---

## Skill 관리 팁

### 팀 공유

`.claude/commands/` 폴더를 Git으로 관리하면
팀 전체가 같은 Skill을 사용할 수 있습니다.

```bash
git add .claude/commands/
git commit -m "팀 공통 Skill 추가"
```

### 개인용 Skill

팀 프로젝트에 포함시키고 싶지 않은 개인 Skill은:

```
~/.claude/commands/    ← 내 컴퓨터 전체에 적용
```

### Skill 목록 보기

Claude Code에서:
```
사용 가능한 슬래시 커맨드 목록을 보여줘.
```

---

## 기초 실습 마무리

**오늘 배운 것:**
- Claude Code 설치 및 기본 사용
- MCP로 외부 서비스 연결
- Skill로 반복 작업 자동화

**다음 단계:**

> 실제 서비스를 만들고 싶다면 → [03 고급 실습](../../03-advanced-practice/README.md)
