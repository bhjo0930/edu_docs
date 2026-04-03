# 강의 프레젠테이션 템플릿

새 강의를 만들 때 이 폴더를 복사해서 시작합니다.

## 파일 구성

| 파일 | 역할 |
|------|------|
| `slides.html` | 슬라이드 프레젠테이션 (수강생 화면) |
| `speaker.html` | 강사 노트 (타이머, 다음 슬라이드, 스크립트 포함) |
| `README.md` | 이 가이드 |

`speaker.html`은 `slides.html?embed=1`을 iframe으로 임베드합니다.
같은 폴더 안에 있으면 폴더를 어디로 복사해도 자동으로 연결됩니다.

---

## 새 강의 만들기

### 1단계: 폴더 복사

```bash
cp -r templates/ 폴더명/
# 예: cp -r templates/ 02-ai-tools/
```

### 2단계: `slides.html` 수정

`<!-- CUSTOMIZE -->` 주석을 검색해서 해당 위치를 교체합니다.

```
Ctrl+F (또는 Cmd+F) → "CUSTOMIZE" 검색
```

교체 항목:
- [ ] `<title>` 강의 제목
- [ ] 사이드바 로고·제목 (커버 위 작은 텍스트)
- [ ] 커버 슬라이드 제목·부제·태그라인
- [ ] TOC 슬라이드 파트명 (5개)
- [ ] 섹션 divider 제목·설명 (5개)
- [ ] 각 콘텐츠 슬라이드 내용 (10개)
- [ ] 마무리 슬라이드 텍스트
- [ ] `simpleToc` 배열 슬라이드 제목·인덱스

슬라이드 수가 바뀌면 `simpleToc`의 `slide` 인덱스도 함께 업데이트하세요.
인덱스는 0부터 시작합니다.

### 3단계: `speaker.html` 수정

교체 항목:
- [ ] `<title>` 강의 제목
- [ ] `slides` 배열 — `slides.html`의 슬라이드 순서와 동일하게 제목·섹션 입력
- [ ] `notesData` 배열 — 각 슬라이드 `summary`(1-2줄 요약)와 `script`(강사 말할 내용)
- [ ] 하단 카운터 `1 / N` — 슬라이드 수에 맞게 변경

### 4단계: 확인

```bash
# 슬라이드 열기
open slides.html

# 강사 화면 열기 (다른 창에서)
open speaker.html
```

확인 항목:
- [ ] `slides.html` 사이드바 TOC 클릭 → 해당 슬라이드 이동
- [ ] `speaker.html` 이전/다음 버튼 → `slides.html`과 동기화
- [ ] `simpleToc` 인덱스가 실제 슬라이드와 일치 (TOC 클릭 시 엉뚱한 슬라이드 이동하면 인덱스 오류)

---

## 슬라이드 타입 참조

### 사용 가능한 CSS 클래스

| 클래스 | 용도 | 예시 슬라이드 |
|-------|------|-------------|
| `compare-grid` | 2칸 비교 (Before/After, A vs B) | 1부 슬라이드 A, 4부 슬라이드 B |
| `workflow` | 단계별 흐름 (Step 1→2→3) | 1부 슬라이드 B, 4부 슬라이드 A |
| `principle-grid` | 카드 그리드 (개념 4개) | 2부 슬라이드 A |
| `code-block` | 코드·명령어 블록 | 2부 슬라이드 B |
| `stat-grid` | 통계/수치 강조 (3칸) | 3부 슬라이드 A, 5부 슬라이드 B |
| `strategy-list` | 번호 목록 (전략, 단계) | 3부 슬라이드 B, 5부 슬라이드 A |
| `quote-box` | 인용구·핵심 메시지 강조 | 1부 슬라이드 A 등 |
| `warn-box` | 주의사항·경고 | 2부 슬라이드 B, 5부 슬라이드 A |
| `slide-section-badge` | 슬라이드 좌상단 섹션 표시 | 모든 콘텐츠 슬라이드 |
| `workflow-step.highlight` | 워크플로우 강조 단계 | 1부 슬라이드 B 등 |

### 슬라이드 추가 방법

1. `slide-area` 안에 새 `<div class="slide-card" data-section="sN">` 추가
2. `simpleToc`에 새 항목 추가 (인덱스는 HTML 순서대로 0부터)
3. `speaker.html`의 `slides`와 `notesData` 배열에 같은 위치에 항목 추가

### 슬라이드 삭제 방법

1. `slide-area`에서 해당 `<div class="slide-card">` 블록 삭제
2. `simpleToc`에서 해당 항목 삭제
3. 이후 슬라이드의 `simpleToc slide` 인덱스를 1씩 줄임
4. `speaker.html`의 `slides`와 `notesData`에서 같은 위치 항목 삭제

---

## 기존 강의 파일 참조

더 많은 슬라이드 예시가 필요하면 기존 파일을 참조하세요:

| 파일 | 슬라이드 수 | 특징 |
|------|-----------|------|
| `01-general/slides.html` | 30개 | 강의용, 이론 중심 |
| `01-general/practice_basic.html` | 25개 | 기초 실습용 |
| `01-general/practice_adv.html` | 30개 | 심화 실습용, 실습 슬라이드 포함 |
