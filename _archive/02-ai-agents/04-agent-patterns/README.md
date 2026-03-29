# 04. Agent 설계 패턴

> **심화 (선택)** — AI 비서의 작동 방식을 더 깊이 이해하고 싶은 분을 위한 내용입니다.
> 비개발자라면 이 단원을 건너뛰어도 됩니다.

---

실무에서 자주 쓰이는 Agent 아키텍처 패턴들입니다.

---

## 패턴 1: Orchestrator-Worker

가장 기본적이고 범용적인 패턴.

```
[Orchestrator]
  - 전체 계획 수립
  - 작업 분배
  - 결과 통합
  - 품질 관리

      ↓ ↓ ↓
[Worker] [Worker] [Worker]
  - 단순 실행
  - 결과 반환
```

**언제 사용**: 크고 복잡한 작업을 여러 전문 Agent에게 나눌 때

**Claude Code 예시**:
```
claude
> 이 프로젝트를 분석해줘. 필요하면 병렬 subagent를 사용해도 돼.
```

---

## 패턴 2: Chain of Thought + Action

각 단계의 추론을 명시적으로 기록하며 진행.

```
[Input]
  ↓
[Step 1 Agent]
  - 생각: "..."
  - 행동: ...
  - 결과: ...
  ↓
[Step 2 Agent]
  - 생각: "Step 1 결과를 보니..."
  - 행동: ...
  - 결과: ...
  ↓
[Final Output]
```

**언제 사용**: 복잡한 추론이 필요한 분석 작업

---

## 패턴 3: Reflection (자기 검토)

Agent가 자신의 출력을 스스로 검토하고 개선.

```
[Generator]
  → 초안 작성
      ↓
[Critic] (= Reflection Agent)
  → "이 부분이 부족해: ..."
      ↓
[Generator]
  → 비판 반영하여 개선
      ↓
  반복 (기준 충족까지)
      ↓
[Final Output]
```

**언제 사용**: 문서 작성, 코드 생성 품질이 중요할 때

---

## 패턴 4: Tool-Use Loop

도구를 반복 사용하며 목표 달성.

```
[목표]
  ↓
루프 시작:
  [추론] "다음엔 어떤 도구를 써야 하지?"
    ↓
  [도구 선택] search / read / execute / write
    ↓
  [도구 실행]
    ↓
  [결과 관찰]
    ↓
  [목표 달성?] → 아니오 → 루프 반복
               → 예 → 완료
```

**언제 사용**: 정보 수집, 환경과 상호작용이 필요한 작업

---

## 패턴 5: Plan-and-Execute

먼저 완전한 계획을 세우고, 계획대로 실행.

```
[Phase 1: Planning]
  - 목표 분석
  - 전체 계획 수립 (단계 1, 2, 3...)
  - 계획 검증

[Phase 2: Execution]
  - 계획대로 순차 실행
  - 각 단계 결과 기록

[Phase 3: Review]
  - 목표 달성 여부 확인
  - 편차 분석
```

**언제 사용**: 예측 가능하고 구조적인 작업

---

## 패턴 비교

| 패턴 | 강점 | 약점 | 적합한 작업 |
|------|------|------|-------------|
| Orchestrator-Worker | 확장성, 전문화 | 복잡한 조율 | 대규모 분석 |
| Chain of Thought | 추론 품질 | 속도 | 복잡한 문제 해결 |
| Reflection | 품질 보장 | 시간/비용 | 문서, 코드 생성 |
| Tool-Use Loop | 유연성 | 예측 어려움 | 탐색적 작업 |
| Plan-and-Execute | 일관성 | 적응성 부족 | 구조화된 작업 |

---

## 실무 조합 예시

**기술 문서 자동화 시스템**:

```
[Plan-and-Execute]
  ↓
Plan:
  1. 코드 스캔 (병렬 Workers)
  2. 함수 문서화 (Reflection 패턴으로 품질 보장)
  3. 전체 문서 통합 (Orchestrator)
  4. 검증 (Evaluator)
```

---

## 다음 단원

[05. 멀티 에이전트 시스템 →](../05-multi-agent-systems/README.md)
