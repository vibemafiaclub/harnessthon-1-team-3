---
name: start
description: PRD를 입력받아 단계별 sub agent를 순서대로 호출해 Penpot 디자인을 완성하는 하네스 진입점. "/start", "시작해줘", "디자인 만들어줘", "PRD 실행", "하네스 돌려줘" 등에 트리거된다.
---

# start — 하네스 진입점

> 🔒 **공용 파일입니다. 수정하려면 조장 승인이 필요합니다.**
>
> 3조 8단계 설계가 반영되어 있습니다. 각 단계 agent는 `.claude/agents/stage-*.md`에 있고,
> **담당자만 자기 단계 파일을 수정합니다.** 단계 추가·삭제는 조장 승인이 필요합니다.

## 입력

- `docs/PRD.md` — 만들어야 할 것의 명세
- 작업 Page 이름 — **매 실행마다 확인한다.** 없으면 묻고, 답을 받기 전엔 시작하지 않는다

## 실행 원칙

1. **각 단계는 반드시 sub agent에게 위임한다.** 오케스트레이터가 직접 저작하지 않는다.
2. 각 sub agent에게 **입력(읽을 파일)·출력(쓸 파일)·작업 Page 이름**을 명시적으로 넘긴다.
3. **의존관계가 없는 단계는 병렬로** 호출한다.
4. 중간 산출물은 전부 `docs/artifacts/`에 남긴다. 남지 않으면 다음 단계가 읽을 게 없다.
5. 한 단계가 출력 파일을 남기지 못했으면 **다음 단계로 넘어가지 않는다.** 멈추고 보고한다.

## 단계 정의

| # | 단계 | sub agent | 입력 | 출력 | 담당자 | 병렬 가능 |
|---|---|---|---|---|---|---|
| 1 | PRD 해석 | `stage-1-prd-parse` | `docs/PRD.md` | `01-prd-spec.md` | A조(조장) | — |
| 2 | 기존 파일 실측 | `stage-2-audit-existing` | `01-prd-spec.md` + Penpot 기존 Page(읽기전용) | `02-design-audit.md` | B조 | ✅ ③과 |
| 3 | 화면 목록 도출 | `stage-3-screen-plan` | `01-prd-spec.md` | `03-screen-list.md` | A조 | ✅ ②와 |
| 4 | 디자인 토큰 | `stage-4-tokens` | `02` + `03` | `04-tokens.md` | B조 | — |
| 5 | 컴포넌트 저작 | `stage-5-components` | `03` + `04` | `05-components.md` + **Penpot 컴포넌트** | C조 | — |
| 6 | 화면 저작 | `stage-6-author-screens` | `03` + `04` + `05` | `06-screens.md` + **Penpot 화면** | C조 | ✅ 화면별 |
| 7 | 시각 검증 | `stage-7-visual-qa` | `03` + `06` + Penpot | `07-qa.md` | 전원 순환(교차) | — |
| 8 | 최종 검증 | `stage-verify-penpot` | `docs/artifacts/` 전체 + Penpot | `99-verify.md` | A조 | — (고정) |

**의존 구조**

```
                  ┌─ ② 실측 ─┐
      ① PRD해석 ──┤          ├─→ ④ 토큰 → ⑤ 컴포넌트 → ⑥ 화면 → ⑦ QA → ⑧ 검증
                  └─ ③ 화면 ─┘
```

## 실행 순서

0. **작업 Page 이름을 확인한다.** 없으면 묻고, 답을 받기 전에는 시작하지 않는다.
   무인 실행이면 인자로 받는다. **기본값으로 첫 Page를 쓰지 않는다.**
1. `stage-1-prd-parse` 호출 → `docs/artifacts/01-prd-spec.md` 생성 확인
2. **`stage-2-audit-existing` + `stage-3-screen-plan` 병렬 호출**
   → `02-design-audit.md`, `03-screen-list.md` 둘 다 생성 확인
   (②에 작업 Page 이름과 "읽기 전용"임을 명시해 넘긴다)
3. `stage-4-tokens` 호출 → `04-tokens.md` 생성 확인
4. `stage-5-components` 호출 (작업 Page 이름 전달) → `05-components.md` + Penpot 컴포넌트 확인
5. `stage-6-author-screens` 호출 (작업 Page 이름 전달) → `06-screens.md` + Penpot 화면 확인
   - `03`의 저작 순서를 따른다. **P0를 전부 끝낸 뒤** P1·P2로 간다
   - 화면 간 의존이 없으면 병렬로 진행해도 된다
6. `stage-7-visual-qa` 호출 (작업 Page 이름 전달) → `07-qa.md` 생성 확인
   - **저작자가 아닌 사람이 검토한다** (교차 검토)
   - `BLOCK`이 있으면 ⑥으로 되돌려 수정 후 재검토
7. `stage-verify-penpot` 호출 → `99-verify.md`

## 마지막 단계 — 검증 (고정, 삭제 금지)

모든 단계가 끝나면 **항상** `stage-verify-penpot` 을 호출한다.

- 지정 Page에 board/frame이 1개 이상 있는가
- PRD가 요구한 화면이 전부 있는가
- 각 단계 산출물이 `docs/artifacts/`에 남아 있는가
- 컴포넌트를 실제 인스턴스로 썼는가 (복붙이 아닌가)
- ⑦의 `BLOCK`이 남아 있지 않은가
- agent 지침에 특정 PRD 전용 고유명사가 박혀 있지 않은가

결과는 `docs/artifacts/99-verify.md`. **실패 항목이 있으면 완료를 선언하지 않는다.**
해당 단계를 다시 호출하고, 재실행 후에도 실패하면 무엇이 왜 비었는지 사용자에게 보고한다.

### 실패 → 되돌릴 단계

| 실패 항목 | 되돌릴 단계 |
|---|---|
| Page에 board/frame 0개 | ⑥ |
| P0 화면 누락 | ⑥ (없으면 ③이 목록에서 빠뜨린 것) |
| 프레임 이름 규칙 위반 | ⑥ |
| 컴포넌트 인스턴스 0 (복붙) | ⑤ → ⑥ |
| 산출물 파일 없음/빈 내용 | 해당 단계 |
| QA `BLOCK` | ⑥ 수정 후 ⑦ 재검토 |
| 고유명사 하드코딩 | 해당 agent 담당자 |

## 완료 조건

- Penpot 파일의 **지정된 Page**에 화면이 실제로 만들어져 있다
- 각 단계의 중간 산출물이 `docs/artifacts/`에 남아 있다
- `docs/artifacts/99-verify.md` 가 전 항목 통과다

## 🔴 오케스트레이터가 지키는 것

- **직접 저작하지 않는다.** Penpot 호출은 ⑤⑥⑦⑧ agent만 한다.
- **직접 산출물을 쓰지 않는다.** `docs/artifacts/`는 각 단계 agent가 쓴다.
- 각 agent를 부를 때 **입력 파일 경로 · 출력 파일 경로 · 작업 Page 이름**을 명시해 넘긴다.
- 한 단계가 출력 파일을 남기지 못했으면 **다음 단계로 넘어가지 않는다.** 멈추고 보고한다.
- 앞 단계 산출물이 없는데 추측해서 채우게 하지 않는다.
