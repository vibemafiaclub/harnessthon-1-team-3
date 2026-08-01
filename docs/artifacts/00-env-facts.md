# 00 — 환경 실측 사실 (오케스트레이터 확인)

> 이 문서는 **오케스트레이터가 Penpot을 직접 읽어 확인한 값**이다. 추측 없음.
> 뒤 단계는 이 값을 재탐색 없이 신뢰해도 된다. 단, 값이 달라 보이면 즉시 보고할 것.

## 파일 / Page

| 항목 | 값 |
|---|---|
| 연결 파일 | `최종제출_3팀` (id `4875cd16-210c-80e8-8008-6a4ed3494781`) |
| Page 총계 | **2개뿐** |
| 읽기 전용 | `3-toss` (id `3d4ec4b9-b483-80f9-8008-699ae0c12c36`) |
| **저작 대상** | **`3-toss-result`** (id `cf8cfb09-3416-4c32-a2eb-38e95e5c2be9`) — 시작 시 자식 0 |

AGENTS.md에 적힌 팀원별 Page(`김주철` 등)·`중간공유`·`최종제출`은 **이 파일에 없다**
(다른 파일 `작업`의 구조). 이 과제에는 적용되지 않는다. 저작 Page는 PRD 7절이 지정한
`3-toss-result`이며, 이는 기본값으로 첫 Page를 고른 것이 아니라 PRD가 명시한 값이다.

## `3-toss` 기존 board 4개 (전부 390×844)

| 이름 | id |
|---|---|
| `홈` | `c6c5510d-9d2c-5557-9548-c893b1456936` |
| `혜택` | `b7801f70-e5a5-50a5-a0ba-0360947a9df4` |
| `전체` | `7bf6b687-5b3d-58e5-a789-837949c1c77b` |
| `설정` | `acb5c0c3-c9d4-5ac6-a958-a0c261c46793` |

⚠️ PRD 2절은 4번째를 "상세"라고 적었으나 **실제 파일에는 `설정`이다.** 파일이 정답이다.

## 🔴 폰트 — 기존 폰트가 서버에 없다 (조용한 대체 위험)

`3-toss`의 텍스트 노드 94개에서 쓰인 폰트:

| 기존 폰트 | 서버 존재 여부 |
|---|---|
| `Spoqa Han Sans Neo` (지배적) | ❌ **없음** |
| `SF Pro` | ❌ **없음** |
| `mixed` | (혼합 표기) |

AGENTS.md 경고 그대로 — **없으면 에러 없이 조용히 대체된다.** 따라서 신규 저작에서
이 이름을 그대로 쓰면 결과가 어긋난다.

### 확정 대체 폰트 → **`Noto Sans KR`**

서버에서 실측 확인(1911개 폰트 중):

| 후보 | 존재 | 사용 가능 weight |
|---|---|---|
| **`Noto Sans KR`** | ✅ | **100~900 전부** ← 채택 |
| `Gothic A1` | ✅ | 100~900 (차선) |
| `IBM Plex Sans KR` | ✅ | 100~700 |
| `Nanum Gothic` | ✅ | 400·700 만 |
| `Pretendard` | ❌ 없음 | — |

기존 디자인이 쓰는 weight는 **400 · 500 · 700**이고 `Noto Sans KR`이 전부 커버한다.
⑤⑥은 텍스트 생성 시 `penpot.fonts.findByName("Noto Sans KR")` 후
`font.applyToText(textNode, variant)` 로 적용한다. `fontFamily` 문자열 직접 대입은 피한다.

### 기존 타이포 조합 실측 (빈도순, 16종)

| family | size | weight | 빈도 |
|---|---|---|---|
| Spoqa Han Sans Neo | 15 | 400 | 20 |
| Spoqa Han Sans Neo | 12 | 400 | 16 |
| Spoqa Han Sans Neo | 10 | 400 | 15 |
| Spoqa Han Sans Neo | 13 | 400 | 8 |
| Spoqa Han Sans Neo | 15 | 500 | 8 |
| Spoqa Han Sans Neo | 16 | 700 | 7 |
| SF Pro | 17 | 400 | 4 |
| Spoqa Han Sans Neo | 11 | 500 | 4 |
| Spoqa Han Sans Neo | 16 | 500 | 3 |
| Spoqa Han Sans Neo | 20 | 700 | 2 |
| Spoqa Han Sans Neo | 18 | 500 | 2 |
| Spoqa Han Sans Neo | 18 | 700 | 1 |

②단계가 이 표를 근거로 위계를 확정하고, ④가 토큰으로 굳힌다.

## 🔴 기존 컴포넌트 36개는 전부 죽어 있다 — 재사용 불가

로컬 라이브러리에 이름은 남아 있다:
`FlightDealCard` `TripSearchWidget` `Row-Direct` `Row-Stopover` `Row-Compared`
`Option-Saver` `Option-Standard` `Option-NonRefundable` `FilterChip-*` `PriceDay-*`
`Tray-Empty` `Tray-Filled` `TabBar` `TopBar` `StatusBar` `EmptyState` `ErrorBanner`
`SkeletonFlightRow` `PriceRefreshBar` `UpcomingTripCard` `ExperienceCard` `ThemeTile`
`DestinationRow` `SectionHeader` `Button-Primary` `Button-Secondary` `Deadline`
`Discount` `Direct` `Lowest` `DirectBar` `StopoverBar` 외 — 총 36개.

**그러나 실측 결과:**
- 36개 전부 `mainInstance()` → **`null`**
- `instance()` 를 호출하면 **id가 빈 문자열인 껍데기**가 나오고 자식이 없다

즉 메인 보드가 삭제된 **고아 등록물**이다. 인스턴스화해도 쓸 수 없다.

### ⑤단계 지침
- 위 36개 이름을 **그대로 재사용하지 마라.** 살아나지 않는다.
- AGENTS.md 규칙대로 **새 이름으로 새로 만든다.**
- 컴포넌트 이름은 **파일 전역**이므로 위 이름과 충돌하지 않도록
  **접두사를 붙여 고유하게** 만든다 (예: `TR/FlightRow` 처럼).
- 만든 뒤 **이름 변경·자식 remove 금지** (플러그인이 멈춘다). 처음에 확정할 것.

## 🔴 톤앤매너 — 기존 4개 화면 PNG 판독 (오케스트레이터 육안 확인)

PRD 6절 "**기존 디자인의 톤앤매너를 유지해주세요. 다른 제품처럼 보이면 안 됩니다.**"
는 이 항목으로 판정된다. 4개 board를 전부 `export_shape`로 뽑아 확인한 결과:

| 관찰 | 값 |
|---|---|
| **테마** | **다크 테마.** 배경은 거의 검정에 가까운 짙은 회색 |
| 표면(카드) | 배경보다 살짝 밝은 짙은 회색 **라운드 카드**를 배경 위에 얹는 구조 |
| 주요 텍스트 | 흰색/밝은 회색 |
| 보조·액션 텍스트 | **파란색 링크성 텍스트**가 행마다 반복 (예: "잔액보기", "포인트 받기") |
| 강조색 | 파랑 계열 (브랜드) |
| 하단 | **5칸 탭바** 고정, 현재 탭만 밝게 |
| 상단 | 9:41 + 신호·와이파이·배터리 **상태바**가 모든 화면에 존재 |
| 반복 구조 | ① 원형 아이콘 + 제목 + 파란 보조링크 **리스트 행** ② 섹션 헤더(굵은 제목) + 목록 ③ 라운드 카드 ④ 우측 `>` 셰브론 ⑤ 작은 배지/칩 |

### ⑤⑥에 대한 구속력 있는 지시

- **절대 라이트 테마로 만들지 마라.** 흰 배경 위 검은 글씨로 저작하면
  PRD 6절 위반이며 "다른 제품처럼 보이면 안 된다"에 정면으로 걸린다.
- 신규 여행 화면도 **어두운 배경 + 어두운 라운드 카드 + 흰 제목 + 파란 액션 텍스트**
  구조를 그대로 계승한다.
- 모든 화면 최상단에 **상태바**, 주요 화면 최하단에 **탭바**를 둔다.
- 정확한 HEX·간격·라운드 실측치는 ②가 남긴 `02-design-audit.md`를 따른다.
  이 절은 방향을 못박는 용도이고, 수치의 출처는 ②다.

## 🔴 `export_shape` 함정 — 메인 인스턴스만 실패한다 (⑤ 이후 오케스트레이터가 직접 분리 실험)

⑤단계가 "`export_shape`가 9회 이상 전부 실패했다 → 익스포트 서비스 장애"라고 보고했으나,
오케스트레이터가 변수를 하나씩 분리해 실험한 결과 **서비스 장애가 아니다.**

| 실험 | 대상 | 결과 |
|---|---|---|
| 기존 board (`홈`, `3-toss`) | 일반 board | ✅ 성공 |
| **컴포넌트 메인 인스턴스** (`TR / Badge / Deadline`) | main instance | ❌ **실패** (`http error`) |
| 새로 만든 일반 board (`3-toss-result`에 생성) | 일반 board | ✅ 성공 |
| **컴포넌트 인스턴스** (`.instance()` 결과) | instance | ✅ **성공** |

### 결론 — ⑥·⑦에 중요

- **Page·익스포트 서비스는 정상이다.** `3-toss-result`에서도 일반 board는 잘 export된다.
- 실패하는 것은 **컴포넌트의 메인 인스턴스(라이브러리 원본 보드)** 뿐이다.
- **⑥이 만드는 화면은 일반 board이고, 그 안의 부품은 `.instance()` 결과다.
  둘 다 export가 된다.** 따라서 **⑦의 시각 검증은 정상적으로 수행 가능하다.**
- ⑦은 "export가 안 된다"는 이유로 시각 검증을 건너뛰면 안 된다.
  화면 board를 대상으로 뽑으면 된다. 컴포넌트 원본만 PNG로 확인하려 들지 마라.

## 🔴 컴포넌트 조회 — `path` + `name`으로 좁혀라 (⑤ 발견, 오케스트레이터 재확인)

Penpot은 `TR/Badge/Deadline` 같은 이름을 **`path`("TR / Badge") + `name`("Deadline")**
으로 쪼개 저장한다(구분자 주위에 공백이 들어간다).
그리고 **죽은 고아 컴포넌트 36개 중 `Discount`·`Deadline` 등 동명이 존재**하므로
**이름만으로 찾으면 죽은 쪽이 잡힌다.**

재확인한 정상 조회 방식:
```js
const comps = penpot.library.local.components.filter(c => (c.path || "").startsWith("TR"));
const target = comps.find(c => c.name === "Deadline");
const inst = target.instance();   // → 정상 인스턴스 (76×22, 자식 1)
```
이름만으로 찾은 것은 `mainInstance()`가 `null`이고, 위 방식으로 찾은 것은 살아 있다.
**⑥은 반드시 `05-components.md` §6의 `findComp(path, name)` 헬퍼를 써라.**

## 이전 실행 산출물 격리

`docs/artifacts/` 에 있던 `01`~`07`·`99` 는 **증권/주식 앱 PRD**의 산출물이었다
(`New/Watchlist`·`New/StockDetail`·`New/Discover`, 검증 Page `김주철`).
현재 `docs/PRD.md`(종합 여행 예약)와 무관하므로
`docs/artifacts/_stale-stock-run/` 으로 옮겼다. **어떤 단계도 이 폴더를 읽지 마라.**
