# 강의 프레젠테이션 템플릿 설계 스펙

**날짜:** 2026-04-03
**목표:** 새 강의를 만들 때 기존 파일을 복사해 내용만 교체하는 방식으로 재사용할 수 있는 템플릿 세트 생성

---

## 컨텍스트

현재 `01-general/` 폴더에 세 쌍의 프레젠테이션 파일이 있다:

| 슬라이드 | 강사 노트 | 슬라이드 수 |
|---------|---------|-----------|
| `slides.html` | `slides_speaker.html` | 30개 |
| `practice_basic.html` | `practice_basic_speaker.html` | 25개 |
| `practice_adv.html` | `practice_adv_speaker.html` | 30개 |

세 파일 모두 CSS/JS 인프라는 거의 동일하고, **슬라이드 HTML 콘텐츠**와 **노트 데이터**만 다르다. 새 강의를 만들 때 기존 파일을 복사해서 내용을 교체하는 방식이 현재 워크플로우다.

---

## 변경 범위

`templates/` 폴더 신규 생성, 3개 파일 작성:

```
templates/
├── slides.html        ← 슬라이드 프레젠테이션 템플릿
├── speaker.html       ← 강사 노트 템플릿
└── README.md          ← 새 강의 만들기 가이드
```

---

## `templates/slides.html` 상세

### 슬라이드 구성 (총 18개)

| 인덱스 | 슬라이드 타입 | 포함 CSS 클래스 |
|--------|-------------|--------------|
| 0 | 커버 (`slide-cover`) | — |
| 1 | 전체 흐름 TOC | `toc-slide-grid` |
| 2 | 섹션1 divider | `slide-section-divider` |
| 3 | 1부 슬라이드 A | `compare-grid` |
| 4 | 1부 슬라이드 B | `workflow` |
| 5 | 섹션2 divider | `slide-section-divider` |
| 6 | 2부 슬라이드 A | `principle-grid` |
| 7 | 2부 슬라이드 B | `code-block` + `warn-box` |
| 8 | 섹션3 divider | `slide-section-divider` |
| 9 | 3부 슬라이드 A | `stat-grid` |
| 10 | 3부 슬라이드 B | `strategy-list` |
| 11 | 섹션4 divider | `slide-section-divider` |
| 12 | 4부 슬라이드 A | `workflow` + `quote-box` |
| 13 | 4부 슬라이드 B | `compare-grid` |
| 14 | 섹션5 divider | `slide-section-divider` |
| 15 | 5부 슬라이드 A | `strategy-list` |
| 16 | 5부 슬라이드 B | `stat-grid` + `quote-box` |
| 17 | 마무리 (`slide-closing`) | — |

### 교체 마커

교체해야 할 모든 위치에 `<!-- CUSTOMIZE: 설명 -->` 주석 삽입:

- `<!-- CUSTOMIZE: 강의 제목 -->` — `<title>` 및 커버 슬라이드 제목
- `<!-- CUSTOMIZE: 1부 제목 및 설명 -->` — 각 섹션 divider
- `<!-- CUSTOMIZE: 슬라이드 내용 -->` — 각 콘텐츠 슬라이드
- `<!-- CUSTOMIZE: simpleToc -->` — JS의 TOC 배열

### 샘플 내용 방침

각 슬라이드에 실제 쓸 수 있는 한국어 샘플 콘텐츠 포함. "Lorem ipsum" 대신 구체적인 예시 텍스트를 사용해서 슬라이드 레이아웃이 어떻게 보이는지 즉시 확인 가능.

### CSS/JS 인프라

기존 `practice_adv.html`의 CSS/JS와 동일하게 유지:
- 다크 사이드바 + 흰 콘텐츠 카드 레이아웃
- `simpleToc` 배열 기반 사이드바 TOC
- 키보드 네비게이션 (← →)
- `?embed=1` iframe 모드
- `postMessage` / `localStorage` 동기화

---

## `templates/speaker.html` 상세

### 구조

기존 `practice_adv_speaker.html`과 동일한 CSS/JS 인프라.

**변경 사항:**
- `<iframe src="slides.html?embed=1">` — 상대 경로 (폴더 복사 시 자동 연결)
- `const slides = [...]` — 18개 슬라이드 메타데이터 샘플
- `const notesData = [...]` — 18개 슬라이드 요약·스크립트 샘플
- 하단 카운터: `1 / 18`

### iframe 상대 경로

`slides.html?embed=1`로 고정. `templates/` 폴더를 다른 이름으로 복사해도 같은 폴더 안에 있으면 자동으로 연결된다.

---

## `templates/README.md` 상세

### 새 강의 만들기 체크리스트

```markdown
## 새 강의 만들기

1. `templates/` 폴더 전체를 복사 → 새 폴더명으로 저장
   예: `cp -r templates/ 02-my-lecture/`

2. `slides.html` 수정
   □ <title> 강의 제목 변경
   □ 커버 슬라이드 제목·부제·날짜 변경
   □ TOC 슬라이드 파트명 변경
   □ 섹션 divider 제목·설명 변경 (5개)
   □ 각 슬라이드 내용 교체 (<!-- CUSTOMIZE --> 검색)
   □ simpleToc 배열 슬라이드 제목·인덱스 업데이트

3. `speaker.html` 수정
   □ <title> 강의 제목 변경
   □ slides 배열 제목·섹션 업데이트 (슬라이드 수 맞게)
   □ notesData 요약·스크립트 작성
   □ 하단 카운터 슬라이드 수 업데이트 (`1 / N`)

4. 확인
   □ slides.html 브라우저로 열기 — 사이드바 TOC 동작 확인
   □ speaker.html 열기 — iframe 동기화 확인
```

### 슬라이드 타입 참조표

사용 가능한 모든 CSS 클래스와 용도를 README에 명시:

| 클래스 | 용도 |
|-------|-----|
| `compare-grid` | 2칸 비교 (Before/After, A vs B) |
| `workflow` | 단계별 흐름 (Step 1→2→3) |
| `principle-grid` | 카드 그리드 (개념 4개 이상) |
| `stat-grid` | 통계/수치 강조 |
| `strategy-list` | 번호 목록 (전략, 단계) |
| `code-block` | 코드·명령어 블록 |
| `quote-box` | 인용구 강조 |
| `warn-box` | 주의사항 |
| `slide-section-badge` | 섹션 배지 (1부, 2부 ...) |

---

## 구현 시 주의사항

1. **CSS 중복 없음**: 기존 `practice_adv.html`의 CSS를 그대로 복사. 신규 CSS 클래스 추가 금지.
2. **샘플 내용**: "강의 주제", "슬라이드 제목" 같은 추상적 플레이스홀더 대신 실제 교육 맥락의 샘플 텍스트 사용.
3. **`simpleToc` 정확성**: 인덱스 0-17이 실제 슬라이드 순서와 일치하도록 작성.
4. **speaker.html 슬라이드 수**: `slides` 배열 길이 = `notesData` 배열 길이 = 18.
5. **iframe 상대 경로**: `speaker.html`의 iframe src는 `slides.html?embed=1` (절대 경로 사용 금지).
