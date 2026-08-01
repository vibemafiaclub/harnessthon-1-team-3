# 03 — 화면 목록

> 입력: `docs/artifacts/01-prd-spec.md` (C·D·E·F절) + 필요 시 `docs/PRD.md` 원문 인용.
> 이 문서는 **문서만** 다룬다. Penpot을 호출하지 않았고 Page를 전환하지 않았다.
> 색·폰트·간격 값은 **④의 소관**이다. 여기서는 화면 목록과 **내용 구조**만 정한다.
>
> 도메인: **종합 여행 예약 서비스(항공권 중심 + 목적지 투어·체험·입장권)**.
> 증권·금융 상품 용어가 이 문서에 등장하면 폐기 대상이다.

---

## 0. 계산 근거 — 왜 이 개수인가

"최소 2개"는 **하한선**이다(PRD 5절 "최소 2개를 만들어주세요. 여유가 있다면 더 만드셔도 좋지만").
아래 3단 계산의 결과를 그대로 따랐다. 개수를 먼저 정하지 않았다.

| 출처 | 계산 | 산출 화면 수 |
|---|---|---|
| C절 (PRD 5절 명시 필수) | `New/Home`, `New/Results` | 2 (P0) |
| D절 (유저 스토리가 "확인하려는 것"으로 요구) | S1-b·S1-c·S2·S3 + C-2의 R4/R5/R6 진입점의 **목적지** | 7 (P1) |
| E절 (사용자 상황 = 상태 화면) | E2·E4·E5·E6·E7 | 5 (P2) |
| **합계** | | **14** |

**진입점 → 목적지 판정 규칙 적용 내역**

| ①의 재료 | 진입점 | 요구되는 목적지 | 화면 번호 |
|---|---|---|---|
| C-2 R5 "담긴 것들을 **나란히 보는 진입점**" | 비교함 버튼 | 나란히 비교 결과 | #7 |
| C-2 R4 "**조건 좁히기**" | 필터 진입점 | 조건 시트 | #5 |
| C-2 R6 "이 화면 **위에 올라오는** 형태" | 운임 버튼 | 운임 시트(오버레이) | #6 |
| C-2 R1 항공편 목록 → "결정까지 간다" | 항공편 행 | 항공편 상세 | #4 |
| C-1 H2 "그 목적지에서 살 수 있는 **투어·체험·입장권**" | 여정 카드 | 목적지 상품 목록 | #9 |
| C-1 H3 "특가 항공권과 여행 상품을 여러 갈래로 소개" | 둘러보기 묶음 | 특가 묶음 전체보기 | #8 |
| C-1 H4 "값이 떨어지면 **알림을 받기** 위해 담아두는 곳" | 담아둔 목적지 | 담아둔 목록 + 가격 하락 확인 | #10 |
| C-1 H5 "하단 주요 이동 수단" | 탭바 | (Home/Results 계열이 목적지를 겸함) | — |

---

## 1. 요약

| 등급 | 개수 | 정의 |
|---|---|---|
| P0 | 2 | PRD 5절이 이름까지 지정한 필수 화면. 없으면 실패 |
| P1 | 7 | 유저 스토리(D절)·필수 요소의 진입점이 직접 요구하는 목적지 화면 |
| P2 | 5 | 사용자 상황(E절)이 요구하는 상태 화면. 완성도 가점 |
| **합계** | **14** | |

전 화면 공통 제약 (PRD 7절):
- 최상위 프레임 이름 **`New/` 접두 필수**
- **폭 390 고정.** 세로는 내용에 맞게
- 저작 Page: **`3-toss-result`** (`3-toss`는 읽기 전용)

---

## 2. 화면 목록

### #1 `New/Home` — P0

| 항목 | 값 |
|---|---|
| 등급 | **P0** |
| 크기 | 390 × **1680** |
| base | — (원본) |
| 목적 | "서로 다른 이유로 들어온 사용자가 각자 자기 다음 행동을 바로 찾는다." (PRD 5-1) |
| 근거 | PRD 5-1 전문 / ① C-1 (H1~H5) |

**섹션 구조 (위 → 아래)**

| 순서 | 블록 이름 | 내용 | 근거 |
|---|---|---|---|
| 1 | `AppBar` | 로고 텍스트 + 알림 아이콘(뱃지 1) | 톤앤매너 유지(6절) |
| 2 | `FlightSearchCard` (H1) | 출발지 `서울(SEL)` ⇄ 목적지 `도쿄(TYO)` / 날짜 `8월 12일 – 8월 16일` / 인원 `성인 1명 · 일반석` / 전체폭 `항공권 검색` 버튼 | "항공권 검색 진입 — 출발지·목적지·날짜·인원" |
| 3 | `UpcomingTripSection` (H2) | `TripCountdownCard`(D-9 · 도쿄 · 8월 12일 출발 · NH862) + 그 아래 가로 스크롤 `ActivityCard` ×3 (도쿄 · 투어/체험/입장권) + `자세히 보기` 진입점 | "예정된 여정 — 출발까지 남은 기간, 그리고 그 목적지에서 살 수 있는 투어·체험·입장권 제안" / E3 "D-14부터" |
| 4 | `ExploreSection` (H3) | 갈래 탭 4개 `마감 임박 / 할인율 / 테마 / 땡처리` + 선택된 갈래의 `DealCard` ×4 (2열 그리드) + `전체보기` 진입점 | "둘러보기 묶음 … 갈래는 직접 정해주세요 (테마 · 할인율 · 마감 임박 · 땡처리 등)" — ①이 "PRD가 위임한 자유 항목"이라 명시(C-1 주석). **③이 위 4갈래로 확정한다** |
| 5 | `WatchlistSection` (H4) | 섹션 헤더 `담아둔 목적지 3` + `WatchRow` ×3 (목적지 · 최저가 · 가격 변동 화살표) + `가격 알림 켜짐` 표기 | "담아둔 목적지 — 값이 떨어지면 알림을 받기 위해 담아두는 곳" |
| 6 | `BottomTabBar` (H5) | `홈 / 검색 / 담아둠 / 내 여정 / 전체` 5탭, `홈` 활성 | "하단 주요 이동 수단" |

**필요한 컴포넌트**: `AppBar` · `FlightSearchCard` · `SectionHeader` · `TripCountdownCard` · `ActivityCard` · `SegmentedTabs` · `DealCard` · `Badge` · `WatchRow` · `PriceDelta` · `BottomTabBar` · `PrimaryButton`

**더미 데이터**

- 여정: `도쿄 나리타 · D-9 · 8월 12일(화) 09:20 출발 · NH862`
- 투어·체험·입장권: `시부야 스카이 전망대 입장권 ₩14,000` / `도쿄 디즈니랜드 1일권 ₩82,400` / `츠키지 새벽 미식 투어 ₩46,000`
- 둘러보기(마감 임박): `오사카 ₩112,000 · 오늘 자정 마감` / `다낭 ₩198,000 · 70% 할인` / `타이베이 ₩139,000 · 오늘 자정 마감` / `방콕 ₩241,000 · 58% 할인`
  - 근거 E8 "특가는 **오늘 자정까지**처럼 마감이 걸린 것이 많고, 어떤 상품은 **정가 대비 70% 할인**입니다."
- 담아둔 목적지: `후쿠오카 ₩98,000 ▼12,000` / `치앙마이 ₩176,000 ▼4,000` / `삿포로 ₩154,000 ▲8,000`

---

### #2 `New/Results` — P0

| 항목 | 값 |
|---|---|
| 등급 | **P0** |
| 크기 | 390 × **1560** |
| base | — (원본. #5·#6·#11·#12·#13이 이 화면의 clone 기반) |
| 목적 | "수십 건 중에서 나에게 맞는 한 편을 골라 결정까지 간다." (PRD 5-2) |
| 근거 | PRD 5-2 전문 / ① C-2 (R1~R6) |

**섹션 구조 (위 → 아래)**

| 순서 | 블록 이름 | 내용 | 근거 |
|---|---|---|---|
| 1 | `ResultsHeader` | 뒤로가기 + `서울 → 도쿄` + `8월 12일 · 성인 1명 · 일반석` + 편집 아이콘 | 검색 조건 유지 |
| 2 | `DateStripRow` (R3) | 가로 스크롤 날짜 칩 7개, 각 칩에 날짜 + 그날 최저가. 선택일 강조, 최저가 칩 별도 표기 | "출발일 앞뒤 가격 비교 — 며칠 전후로 옮기면 얼마인지" |
| 3 | `FilterBar` (R4) | 칩 `조건 좁히기(필터)` `직항만` `오전 출발` `항공사` `가격순 ▾` — **가로 스크롤. `조건 좁히기` 칩이 #5의 진입점** | "조건 좁히기 — 직항 여부·시간대·항공사 등" |
| 4 | `ResultCountRow` | `총 52건` + 정렬 표기 `추천순` | E1 "보통 40~60건" |
| 5 | `FlightList` (R1·R2) | `FlightRow` ×6. 각 행: 항공사 로고+명 / 출발–도착 시각 / 소요 시간 / **경유 표기** / 가격 / 비교함 담기 체크박스. 경유 편은 행 안에 `LayoverNote`(경유지 + 대기 시간) | "항공편 목록 — 출발·도착 시각, 소요 시간, 경유 여부, 항공사, 가격" + "경유 구간 표현 — 경유가 있는 편은 어디서 얼마나 기다리는지" |
| 6 | `PriceChangeNotice` | `요금은 실시간이며 조회 시점에 따라 달라질 수 있어요` 한 줄 | E6 "실시간이라 … 그 사이 값이 바뀌기도 합니다" |
| 7 | `CompareTrayBar` (R5) | **하단 고정 바.** `비교함 2/3` + 담긴 항공편 썸네일 + `나란히 비교` 버튼 — **#7의 진입점** | "비교함 — 항공편을 담고, 담긴 것들을 나란히 보는 진입점" / E2 "최대 3개" |

**필요한 컴포넌트**: `ResultsHeader` · `DateChip` · `FilterChip` · `FlightRow` · `AirlineMark` · `LayoverNote` · `PriceText` · `CompareTrayBar` · `PrimaryButton` · `Badge`

**더미 데이터**

- 날짜 칩: `8/9 ₩241,000` `8/10 ₩228,000` `8/11 ₩219,000` `**8/12 ₩232,000(선택)**` `8/13 ₩209,000(최저)` `8/14 ₩246,000` `8/15 ₩288,000`
- 항공편 6건 (총 `52건` 중 표시):
  1. `대한항공 KE703 · 09:20→11:45 · 2시간 25분 · 직항 · ₩232,000`
  2. `아시아나 OZ102 · 07:40→10:05 · 2시간 25분 · 직항 · ₩228,600`
  3. `진에어 LJ201 · 13:10→15:35 · 2시간 25분 · 직항 · ₩176,400`
  4. `중국동방 MU5052 · 08:00→17:40 · 11시간 40분 · 1회 경유 · ₩154,000` — `상하이 푸둥에서 5시간 20분 대기`
  5. `피치항공 MM802 · 19:55→22:20 · 2시간 25분 · 직항 · ₩168,900`
  6. `캐세이퍼시픽 CX411 · 10:15→21:05 · 12시간 50분 · 1회 경유 · ₩198,000` — `홍콩에서 6시간 05분 대기`
- 비교함: `2/3`

---

### #3 `New/Results-Loading` — P2

| 항목 | 값 |
|---|---|
| 등급 | **P2** |
| 크기 | 390 × **1560** (base와 동일) |
| base | **`New/Results`** (clone) |
| 목적 | 실시간 요금 조회 중 상태 |
| 근거 | E6 / PRD 4절 "항공 요금은 실시간이라 **불러오는 데 몇 초**가 걸리고, 그 사이 값이 바뀌기도 합니다." |

**저작 방식**: `New/Results`를 `clone()` → `FlightList`의 `FlightRow` 인스턴스를 `SkeletonRow` ×6으로 교체, `ResultCountRow`를 진행 표기로 교체.

**섹션 구조**: `ResultsHeader`(그대로) → `DateStripRow`(그대로) → `FilterBar`(비활성) → `LoadingStatusRow` → `SkeletonRow` ×6 → (하단 `CompareTrayBar` 숨김)

**필요한 컴포넌트**: `SkeletonRow` · `LoadingStatusRow`(신규) + base 컴포넌트 재사용

**더미 데이터**: `52개 항공사 요금을 실시간으로 불러오는 중` / `보통 3~5초 걸려요` / 진행 게이지 60%

---

### #4 `New/FlightDetail` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1480** |
| base | — (원본) |
| 목적 | 목록에서 고른 한 편의 여정 구간·경유·요금 조건을 확인하고 결정으로 간다 |
| 근거 | PRD 5-2 목적 "수십 건 중에서 나에게 맞는 한 편을 골라 **결정까지 간다**" — 목록만으로는 "결정까지" 닫히지 않는다. R2 "경유가 있는 편은 **어디서 얼마나 기다리는지 알 수 있게**"의 완전한 표현 목적지 |

**섹션 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `DetailHeader` | 뒤로가기 + `MU5052` + 담기(하트) 아이콘 |
| 2 | `RouteSummaryCard` | `서울(ICN) → 도쿄(NRT)` · `8월 12일(화)` · `총 11시간 40분 · 1회 경유` |
| 3 | `SegmentTimeline` | 세로 타임라인. 구간1 `ICN 08:00 → PVG 09:20 (2시간 20분)` → **`LayoverBlock` `상하이 푸둥 환승 5시간 20분 · 공항 밖 이동 불가`** → 구간2 `PVG 14:40 → NRT 17:40 (3시간)` |
| 4 | `BaggageRow` | `위탁 수하물 23kg · 기내 7kg` |
| 5 | `FareConditionList` | `환불 수수료 ₩120,000` / `날짜 변경 불가` / `좌석 지정 유료` |
| 6 | `RelatedActivityStrip` | 도쿄 투어·체험 `ActivityCard` ×2 (교차 판매 — PRD 1절 "목적지에서 즐길 투어·체험·입장권까지 한 곳에서 팝니다") |
| 7 | `DetailBottomBar` | 하단 고정. `₩154,000` + `운임 선택` 버튼 → #6 진입점 |

**필요한 컴포넌트**: `DetailHeader` · `RouteSummaryCard` · `SegmentTimeline`(내부 `SegmentRow`·`LayoverBlock`) · `InfoRow` · `ActivityCard`(재사용) · `DetailBottomBar` · `PrimaryButton`

---

### #5 `New/Results-FilterSheet` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1560** (base와 동일) |
| base | **`New/Results`** (clone + 오버레이) |
| 목적 | 필터 진입점을 눌렀을 때 실제로 조건을 좁히는 시트 |
| 근거 | ① C-2 R4 "조건 좁히기 — 직항 여부·시간대·항공사 등" + C-2 주석 "R4 '조건 좁히기'는 **진입점이 눌렸을 때의 결과가 필요하다**" |

**🔴 저작 방식 (⑥ 지시)**
1. `New/Results`를 `clone()` 한다.
2. **뒤 콘텐츠 보드(`ResultsBody`)의 `opacity`를 0.35로 낮춘다.**
   반투명 스크림 사각형을 **덮지 않는다** (AGENTS.md 함정: `fillOpacity 0.4` 오버레이가 렌더링에서 사라짐).
3. 클론 프레임 최상단에 `FilterSheet` 보드를 얹는다. 하단 정렬, 폭 390, 높이 620.
4. 시트가 화면 하단에 붙도록 `Spacer` 높이를 **계산해 명시**한다 (`layoutGrow` Spacer가 폭 1로 되돌아가는 함정 회피).

**시트 내부 구조 (위 → 아래)**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `SheetGrabber` | 핸들 바 |
| 2 | `SheetHeader` | `조건 좁히기` + 닫기 |
| 3 | `FilterGroup` 경유 | `직항만 / 1회 경유까지 / 전체` 토글 3 |
| 4 | `FilterGroup` 출발 시간대 | `새벽 00–06 / 오전 06–12 / 오후 12–18 / 저녁 18–24` 칩 4 |
| 5 | `FilterGroup` 항공사 | 체크 리스트 5: `대한항공 · 아시아나 · 진에어 · 피치항공 · 중국동방` |
| 6 | `FilterGroup` 가격 | 범위 표기 `₩150,000 – ₩300,000` |
| 7 | `SheetFooter` | `초기화` + `52건 보기` |

**필요한 컴포넌트**: `SheetGrabber` · `SheetHeader` · `FilterGroup` · `FilterChip`(재사용) · `CheckRow` · `SheetFooter`

---

### #6 `New/Results-FareSheet` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1560** (base와 동일) |
| base | **`New/Results`** (clone + 오버레이) |
| 목적 | 같은 항공편의 환불·변경·수하물 조건이 다른 운임을 고른다 |
| 근거 | PRD 5-2 "**운임 등급 선택** — 같은 항공편이라도 환불·변경·수하물 조건이 다른 여러 운임 **(별도 화면이 아니라 이 화면 위에 올라오는 형태로 만들어주세요)**" |

**🔴🔴 C-3 제약 — 절대 위반 금지**

- **최상위 독립 프레임으로 만들지 않는다.** 운임 등급만 들어 있는 빈 배경 프레임은 **금지**다.
- **반드시 `New/Results`를 `clone()` 하여 뒤에 Results 콘텐츠가 보이는 상태에서** 그 위에 시트를 얹는다.
- 뒤를 어둡게 할 때 **스크림 사각형을 덮지 말고 뒤 콘텐츠 보드의 `opacity`를 0.35로 낮춘다.**
- ⑦ 시각 QA 체크: PNG에서 **시트 위/좌우로 Results의 항공편 목록이 흐릿하게 보여야 통과.**

**시트 내부 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `SheetGrabber` | 핸들 바 |
| 2 | `SheetHeader` | `운임 선택` + `대한항공 KE703 · 8월 12일` 서브 |
| 3 | `FareOptionCard` ×3 | 각 카드: 등급명 / 가격 / 환불·변경·수하물 3줄 조건 / 선택 라디오 |
| 4 | `FareNote` | `운임 조건은 항공사 규정에 따라 달라질 수 있어요` |
| 5 | `SheetFooter` | `₩232,000` + `선택 완료` |

**더미 데이터 (운임 3종)**

| 등급 | 가격 | 환불 | 변경 | 수하물 |
|---|---|---|---|---|
| `스탠다드` | ₩232,000 | 수수료 ₩120,000 | 불가 | 위탁 23kg |
| `플렉스` | ₩286,000 | 수수료 ₩50,000 | 1회 무료 | 위탁 23kg |
| `프리미엄 플렉스` | ₩341,000 | 무료 환불 | 무제한 | 위탁 32kg + 좌석 지정 |

**필요한 컴포넌트**: `FareOptionCard`(신규, 3회 반복) · `SheetGrabber`·`SheetHeader`·`SheetFooter`(#5와 공유) · `ConditionRow`

---

### #7 `New/Compare` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1180** |
| base | — (원본. #14가 이 화면의 clone 기반) |
| 목적 | 담아둔 항공편을 **나란히** 놓고 결정한다 |
| 근거 | PRD 5-2 "비교함 — 항공편을 담고, 담긴 것들을 **나란히 보는 진입점**" + ① C-2 주석 "진입점이므로 **목적지가 존재해야 한다**" + D절 S3 "조건이 비슷한 항공권 몇 개를 담아 **나란히 비교하고 싶다**" |

**섹션 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `CompareHeader` | 뒤로가기 + `비교함` + `2/3` 카운터 |
| 2 | `CompareColumnHeaderRow` | 좌측 라벨 열(96) + 항공편 열 ×2 (각 137). 열 상단에 항공사·편명·담기 해제 |
| 3 | `CompareMatrix` | `CompareRow` ×7 — 가격 / 출발 / 도착 / 소요 시간 / 경유 / 수하물 / 환불. **더 나은 값에 강조 뱃지** |
| 4 | `CompareAddSlot` | 세 번째 열 자리에 점선 `+ 항공편 추가 (1자리 남음)` |
| 5 | `CompareBottomBar` | `선택한 항공편 예약` 버튼 |

**근거 수치**: 열 최대 3 — E2 "비교함에는 **최대 3개**까지 담을 수 있습니다."

**더미 데이터**

| 항목 | KE703 | MU5052 |
|---|---|---|
| 가격 | **₩232,000** | ₩154,000 ✅최저 |
| 출발 | 09:20 | 08:00 |
| 도착 | 11:45 | 17:40 |
| 소요 | **2시간 25분** ✅최단 | 11시간 40분 |
| 경유 | 직항 ✅ | 1회 (상하이 5시간 20분) |
| 수하물 | 23kg | 23kg |
| 환불 | 수수료 ₩120,000 | 불가 |

**필요한 컴포넌트**: `CompareHeader` · `CompareColumnHeader` · `CompareRow` · `Badge`(재사용) · `CompareAddSlot` · `PrimaryButton`

---

### #8 `New/DealCollection` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1420** |
| base | — (원본) |
| 목적 | 목적지 미정 사용자가 갈래별 특가를 끝까지 훑는다 |
| 근거 | D절 S1-b "어디로 갈지 못 정한 채 싼 표를 구경하러 오는 사용자" → 확인하려는 것 "**특가/할인 묶음, 그 안의 개별 상품**" + PRD 1절 "목적지를 못 정한 사람은 검색창 앞에서 멈추고" + C-1 H3 `전체보기` 진입점의 목적지 |

**섹션 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `CollectionHeader` | 뒤로가기 + `둘러보기` |
| 2 | `SegmentedTabs` (재사용) | `마감 임박 / 할인율 / 테마 / 땡처리` — 홈 H3와 동일 갈래 |
| 3 | `DeadlineBanner` | `오늘 자정 마감 · 남은 시간 05:41:22` 카운트다운 |
| 4 | `DealGrid` | `DealCard` ×8 (2열 × 4행). 각 카드: 사진 / 도시 / 정가 취소선 / 특가 / 할인율 뱃지 / 마감 뱃지 |
| 5 | `DealListSection` | `DealRow` ×3 — 여행 상품(투어·체험·입장권) 리스트형 |
| 6 | `BottomTabBar` (재사용) | `검색` 활성 |

**더미 데이터**: `다낭 ₩660,000 → ₩198,000 · 70% 할인` (E8 원문 수치) / `오사카 ₩112,000 · 오늘 자정 마감` / `타이베이 ₩139,000` / `방콕 ₩241,000 · 58%` / `세부 ₩289,000 · 44%` / `코타키나발루 ₩312,000 · 39%` / `괌 ₩358,000 · 31%` / `싱가포르 ₩412,000 · 27%`

**필요한 컴포넌트**: `CollectionHeader` · `SegmentedTabs`(재사용) · `DealCard`(재사용, 8회) · `DealRow` · `Badge`(재사용) · `CountdownStrip` · `BottomTabBar`(재사용)

---

### #9 `New/DestinationActivities` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1360** |
| base | — (원본) |
| 목적 | 이미 표를 끊은 사용자가 그 목적지에서 살 투어·체험·입장권을 고른다 |
| 근거 | PRD 5-1 "예정된 여정 — … 그 목적지에서 살 수 있는 **투어·체험·입장권 제안**" + D절 S1-c "이미 표를 끊어두고 현지에서 할 것을 찾으러 오는 사용자" / 확인하려는 것 "남은 기간 + 그 목적지의 투어·체험·입장권" + PRD 1절 "목적지에서 즐길 투어·체험·입장권까지 한 곳에서 팝니다" |

**섹션 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `DestinationHeroHeader` | 도쿄 사진 배경 + `도쿄` + `8월 12일 – 16일 · D-9` |
| 2 | `TripSummaryStrip` | `NH862 · 나리타 도착 11:45` + `여정 상세` 진입점 |
| 3 | `CategoryChipRow` | `전체 / 입장권 / 투어 / 체험 / 교통패스` 칩 5 |
| 4 | `ActivityList` | `ActivityCard` ×6 (사진 / 상품명 / 별점·후기 수 / 가격 / `즉시 확정` 뱃지) |
| 5 | `ActivityBundleCard` | `도쿄 3일 자유이용 묶음 ₩121,000 (15% 할인)` |
| 6 | `BottomTabBar` (재사용) | `내 여정` 활성 |

**더미 데이터**: `시부야 스카이 전망대 입장권 ₩14,000 ★4.8 (2,341)` / `도쿄 디즈니랜드 1일권 ₩82,400 ★4.9 (8,120)` / `츠키지 새벽 미식 투어 ₩46,000 ★4.7 (612)` / `팀랩 플래닛 입장권 ₩38,500 ★4.6 (4,077)` / `기모노 착용 체험 ₩29,000 ★4.5 (983)` / `스이카 교통패스 ₩23,000 ★4.4 (1,556)`

**필요한 컴포넌트**: `DestinationHeroHeader` · `TripSummaryStrip` · `FilterChip`(재사용) · `ActivityCard`(재사용, 6회) · `RatingRow` · `Badge`(재사용) · `BottomTabBar`(재사용)

---

### #10 `New/Watchlist` — P1

| 항목 | 값 |
|---|---|
| 등급 | **P1** |
| 크기 | 390 × **1240** |
| base | — (원본. #13이 이 화면의 clone 기반) |
| 목적 | 담아둔 목적지·항공편의 **가격 변동 결과를 확인**한다 |
| 근거 | D절 S2 "마음에 둔 목적지를 담아두고 **값이 떨어지면 알림을 받고 싶다**" / 확인하려는 것 "①담아둔 목록 ②**값이 떨어졌다는 알림·가격 변동 결과**" + ① D-1 "담는 UI만으로는 스토리가 닫히지 않는다. 가격 하락을 **확인**하는 표현이 어딘가에 있어야 한다" + C-1 H4 |

**섹션 구조**

| 순서 | 블록 | 내용 |
|---|---|---|
| 1 | `WatchlistHeader` | `담아둔 목적지` + 알림 설정 아이콘 |
| 2 | `PriceAlertBanner` | **가격 하락 알림** — `후쿠오카가 12,000원 내렸어요 · 2시간 전` + `보러가기` |
| 3 | `WatchTabs` | `목적지 3 / 항공편 2` 세그먼트 |
| 4 | `WatchDestinationList` | `WatchRow` ×3 — 도시 사진 / 도시명 / 현재 최저가 / `PriceDelta`(▼12,000 · 12% / ▼4,000 / ▲8,000) / 알림 토글 |
| 5 | `PriceHistoryCard` | 후쿠오카 30일 가격 추이 미니 차트 + `최근 30일 최저 ₩92,000` |
| 6 | `WatchFlightList` | 담아둔 항공편 2건 — `LJ201 ₩176,400 · 알림 켜짐`, `MM802 ₩168,900 · 알림 켜짐` |
| 7 | `BottomTabBar` (재사용) | `담아둠` 활성 |

**필요한 컴포넌트**: `WatchlistHeader` · `AlertBanner` · `SegmentedTabs`(재사용) · `WatchRow`(재사용) · `PriceDelta`(재사용) · `PriceHistoryCard` · `BottomTabBar`(재사용)

---

### #11 `New/Results-Empty` — P2

| 항목 | 값 |
|---|---|
| 등급 | **P2** |
| 크기 | 390 × **1100** |
| base | **`New/Results`** (clone) |
| 목적 | 조건을 너무 좁혔을 때 0건 상태에서 빠져나올 경로 제공 |
| 근거 | E5 / PRD 4절 "조건을 까다롭게 좁히면 **맞는 항공편이 한 건도 없는** 경우가 나옵니다." |

**저작 방식**: `New/Results` clone → `FlightList` 자식(`FlightRow` 인스턴스)을 전부 `EmptyState`로 교체. `FilterBar`의 적용 칩을 활성 상태로 남긴다(왜 0건인지 보이게). `CompareTrayBar`는 유지.

**섹션 구조**: `ResultsHeader` → `DateStripRow`(그대로 — 다른 날엔 있다는 탈출구) → `FilterBar`(활성 칩 4개 강조) → `ResultCountRow` `총 0건` → `EmptyState`(일러스트 + `조건에 맞는 항공편이 없어요` + `필터를 조금만 풀어보세요`) → `SuggestionList`(`직항 조건 해제하면 18건` / `시간대 조건 해제하면 31건` / `8월 13일로 옮기면 47건`) → `SecondaryButton` `조건 초기화`

**필요한 컴포넌트**: `EmptyState`(신규) · `SuggestionRow`(신규) · `SecondaryButton` + base 재사용

---

### #12 `New/Home-FirstRun` — P2

| 항목 | 값 |
|---|---|
| 등급 | **P2** |
| 크기 | 390 × **1420** |
| base | **`New/Home`** (clone) |
| 목적 | 신규 설치 사용자에게도 홈이 비어 보이지 않게 한다 |
| 근거 | E4 / PRD 4절 "앱을 처음 깐 사용자에게는 **예정된 여정도, 담아둔 목적지도 하나도 없습니다.**" |

**저작 방식**: `New/Home` clone → `UpcomingTripSection`의 `TripCountdownCard`+`ActivityCard` 묶음을 `EmptyState`(작은 버전)로 교체, `WatchlistSection`의 `WatchRow` ×3을 `EmptyState`로 교체. `FlightSearchCard`·`ExploreSection`·`BottomTabBar`는 **그대로 유지**(목적지 미정 사용자 경로가 살아 있어야 한다).

**섹션 구조**: `AppBar` → `FlightSearchCard`(출발지만 `서울(SEL)`, 목적지 `어디든지`) → `UpcomingTripEmpty`(`아직 예정된 여정이 없어요` / `출발 14일 전부터 여기에 표시돼요` ← E3 D-14 근거) → `ExploreSection`(그대로, 갈래 탭 + `DealCard` ×4) → `WatchlistEmpty`(`마음에 둔 목적지를 담아보세요` / `값이 떨어지면 알려드려요` + `목적지 둘러보기` 버튼) → `BottomTabBar`

**필요한 컴포넌트**: `EmptyState`(재사용, 2회) · `SecondaryButton` + base 재사용

---

### #13 `New/Watchlist-SoldOut` — P2

| 항목 | 값 |
|---|---|
| 등급 | **P2** |
| 크기 | 390 × **1240** (base와 동일) |
| base | **`New/Watchlist`** (clone + 오버레이) |
| 목적 | 담아둔 항공편이 결제 전에 마감됐을 때의 실패 상태 |
| 근거 | E7 / PRD 4절 "담아둔 항공편이 **결제 전에 마감**되는 일이 하루에도 여러 번 있습니다." |

**저작 방식**: `New/Watchlist` clone → 뒤 콘텐츠 보드 `opacity` 0.35 (스크림 금지) → `SoldOutDialog` 모달을 중앙에 얹는다. 동시에 뒤쪽 `WatchFlightList`의 첫 행을 마감 상태(취소선 가격 + `마감` 뱃지)로 바꿔 모달을 닫아도 상태가 남게 한다.

**모달 구조**: `DialogIcon` → `제목: 담아둔 항공편이 마감됐어요` → `본문: LJ201 8월 12일 ₩176,400 좌석이 모두 판매됐어요. 비슷한 조건의 항공편을 찾아봤어요.` → `AlternativeRow` ×2 (`MM802 ₩168,900` / `LJ203 ₩181,000`) → 버튼 2개 `닫기` · `대체 항공편 보기`

**필요한 컴포넌트**: `Dialog`(신규) · `AlternativeRow`(신규) · `SecondaryButton`·`PrimaryButton`(재사용)

---

### #14 `New/Compare-Empty` — P2

| 항목 | 값 |
|---|---|
| 등급 | **P2** |
| 크기 | 390 × **900** |
| base | **`New/Compare`** (clone) |
| 목적 | 비교함이 0개인 기본 상태 |
| 근거 | E2 / PRD 4절 "비교함에는 최대 3개까지 담을 수 있습니다. **하나도 안 담고 나가는 사용자가 대부분입니다.**" — ① E2 함의 "**대부분이 0개** → 비교함 빈 상태가 기본값" |

**저작 방식**: `New/Compare` clone → `CompareMatrix`·`CompareColumnHeaderRow` 제거 대신 `EmptyState`로 교체(자식 remove가 위험하므로 **가시성 있는 교체**로 처리), 카운터를 `0/3`으로.

**섹션 구조**: `CompareHeader`(`0/3`) → `EmptyState`(`아직 담은 항공편이 없어요` / `검색 결과에서 최대 3개까지 담아 나란히 볼 수 있어요`) → `HowToRow` ×3 (`1. 검색 결과에서 담기` / `2. 최대 3개까지` / `3. 나란히 비교`) → `PrimaryButton` `항공편 검색하러 가기` → `RecentSearchList`(`서울 → 도쿄 8/12` / `서울 → 오사카 9/3`)

**필요한 컴포넌트**: `EmptyState`(재사용) · `HowToRow`(신규) · `RecentSearchRow`(신규) + base 재사용

---

## 3. 상태 변형 (clone 대상)

⑥은 아래 화면을 **처음부터 짓지 않는다.** base를 `clone()` 한 뒤 덮을 것만 얹는다.

| base 화면 | 변형 | 무엇이 달라지나 | 오버레이 여부 |
|---|---|---|---|
| `New/Results` | `New/Results-Loading` | `FlightRow`×6 → `SkeletonRow`×6, 카운트 → 진행 표기, `CompareTrayBar` 숨김, `FilterBar` 비활성 | 아니오 |
| `New/Results` | `New/Results-FilterSheet` | 뒤 보드 `opacity` 0.35 + 하단 `FilterSheet`(h 620) 얹기 | **예 (opacity 방식)** |
| `New/Results` | `New/Results-FareSheet` | 뒤 보드 `opacity` 0.35 + 하단 `FareSheet`(h 560) 얹기. **C-3 준수 필수** | **예 (opacity 방식)** |
| `New/Results` | `New/Results-Empty` | `FlightList` → `EmptyState` + `SuggestionList`, 카운트 `0건`, 필터 칩 활성 강조 | 아니오 |
| `New/Home` | `New/Home-FirstRun` | 여정 섹션·담아둔 섹션 → `EmptyState`. 검색·둘러보기·탭바는 유지 | 아니오 |
| `New/Watchlist` | `New/Watchlist-SoldOut` | 뒤 보드 `opacity` 0.35 + `SoldOutDialog` 중앙 모달, 뒤 첫 행 마감 처리 | **예 (opacity 방식)** |
| `New/Compare` | `New/Compare-Empty` | 매트릭스 → `EmptyState` + `HowToRow`, 카운터 `0/3` | 아니오 |

**🔴 오버레이 공통 규칙 (⑥ 필독)**
- 반투명 스크림 사각형(`fillOpacity: 0.4`)을 **덮지 않는다.** 렌더링에서 사라지는 사례가 확인됐다.
- 대신 **뒤 콘텐츠 보드의 `opacity`를 0.35로 낮춘다.**
- 시트 높이를 명시하고, 하단 정렬용 `Spacer` 높이는 **계산해서 고정값으로** 넣는다.
- clone 후 **자식을 `remove` 하지 않는다.** 교체가 필요하면 새 노드를 만들어 `insertChild(index, node)` 로 넣는다.

---

## 4. 화면 의존 관계 (저작 순서 제약)

| 화면 | 선행되어야 하는 화면 | 이유 |
|---|---|---|
| `New/Results-Loading` | `New/Results` | clone 원본 |
| `New/Results-FilterSheet` | `New/Results` | clone 원본 |
| `New/Results-FareSheet` | `New/Results` | clone 원본 (C-3) |
| `New/Results-Empty` | `New/Results` | clone 원본 |
| `New/Home-FirstRun` | `New/Home` | clone 원본 |
| `New/Watchlist-SoldOut` | `New/Watchlist` | clone 원본 |
| `New/Compare-Empty` | `New/Compare` | clone 원본 |
| `New/FlightDetail` | (없음) | 독립. 단 `ActivityCard`가 `New/Home`과 공유 |
| `New/DealCollection` | (없음) | 독립. `DealCard`·`SegmentedTabs`가 `New/Home`과 공유 |
| `New/DestinationActivities` | (없음) | 독립. `ActivityCard` 공유 |
| `New/Watchlist` | (없음) | 독립. `WatchRow`·`PriceDelta`가 `New/Home`과 공유 |

---

## 5. 화면별 필요 컴포넌트 (⑤단계 입력)

**컴포넌트 후보 판정 기준: 2개 이상 화면에 등장하거나, 한 화면에서 3회 이상 반복.**
아래는 그 기준을 통과한 것만 올렸다. ⑤가 실제 목록·치수를 확정한다.

| 컴포넌트 이름 | 쓰이는 화면 | 반복 횟수(최대) | 가변 요소 |
|---|---|---|---|
| `BottomTabBar` | Home, Home-FirstRun, DealCollection, DestinationActivities, Watchlist | 1 | 활성 탭 인덱스 |
| `PrimaryButton` | Home, FlightDetail, FilterSheet, FareSheet, Compare, Compare-Empty, Watchlist-SoldOut | 1 | 라벨 |
| `SecondaryButton` | Results-Empty, Home-FirstRun, Compare-Empty, Watchlist-SoldOut | 1 | 라벨 |
| `SectionHeader` | Home, DealCollection, DestinationActivities, Watchlist | 4 | 제목, 우측 `전체보기` 유무 |
| `Badge` | Home, Results, DealCollection, DestinationActivities, Compare, Watchlist-SoldOut | 8 | 텍스트, 톤(할인/마감/최저/상태) |
| `DealCard` | Home(4), DealCollection(8) | 8 | 사진, 도시, 정가, 특가, 할인율, 마감 문구 |
| `ActivityCard` | Home(3), FlightDetail(2), DestinationActivities(6) | 6 | 사진, 상품명, 별점, 가격 |
| `FlightRow` | Results(6), Results-Empty(0), Results-Loading(→Skeleton) | 6 | 항공사, 편명, 시각, 소요, 경유, 가격, 담김 여부 |
| `LayoverNote` | Results(2), FlightDetail(1) | 2 | 경유지, 대기 시간 |
| `AirlineMark` | Results, FlightDetail, Compare, Watchlist | 6 | 항공사 로고·명 |
| `PriceText` | Results, FlightDetail, Compare, DealCollection, Watchlist | 8 | 금액, 취소선 여부, 강조 여부 |
| `DateChip` | Results, Results-Loading, Results-Empty, FilterSheet, FareSheet | 7 | 날짜, 가격, 선택/최저 상태 |
| `FilterChip` | Results(5), FilterSheet(4), DestinationActivities(5) | 5 | 라벨, 선택 여부 |
| `SegmentedTabs` | Home, DealCollection, Watchlist | 1 | 탭 라벨 배열, 활성 인덱스 |
| `WatchRow` | Home(3), Watchlist(3), Watchlist-SoldOut(3) | 3 | 도시, 가격, 변동, 알림 토글 |
| `PriceDelta` | Home, Watchlist, Watchlist-SoldOut | 3 | 방향(▲▼), 금액, 퍼센트 |
| `CompareTrayBar` | Results, Results-Loading, Results-Empty, FilterSheet, FareSheet | 1 | n/3 카운트, 썸네일 수 |
| `SheetGrabber` | FilterSheet, FareSheet | 1 | — |
| `SheetHeader` | FilterSheet, FareSheet | 1 | 제목, 서브 |
| `SheetFooter` | FilterSheet, FareSheet | 1 | 좌측 라벨, 우측 버튼 라벨 |
| `EmptyState` | Results-Empty, Home-FirstRun(2), Compare-Empty | 2 | 아이콘, 제목, 설명 |
| `SkeletonRow` | Results-Loading | 6 | — |
| `FareOptionCard` | FareSheet | 3 | 등급명, 가격, 조건 3줄, 선택 여부 |
| `CompareRow` | Compare | 7 | 항목명, 값 ×2~3, 강조 열 |
| `InfoRow` / `ConditionRow` | FlightDetail, FareSheet, Compare | 7 | 라벨, 값 |
| `SuggestionRow` | Results-Empty | 3 | 조건 문구, 결과 건수 |
| `RatingRow` | DestinationActivities | 6 | 별점, 후기 수 |

**단일 사용이라 컴포넌트가 아닌 것 (⑥이 화면 안에서 직접 조립)**:
`FlightSearchCard`(Home 전용이나 크기가 커 ⑤ 판단에 위임) · `TripCountdownCard` · `PriceHistoryCard` · `SegmentTimeline` · `DestinationHeroHeader` · `AlertBanner` · `Dialog` · `CompareAddSlot` · `HowToRow` · `RecentSearchRow`
→ ⑤가 비용 대비 판단해 일부를 컴포넌트로 승격해도 된다. **강제하지 않는다.**

---

## 6. 저작 순서 (⑥단계 입력)

**원칙: P0를 전부 끝내고 검증한 뒤 P1로 간다. clone 기반 화면은 원본 완성 후.**
각 화면을 저작한 뒤 **`export_shape`로 PNG를 확인하고 다음으로 넘어간다.** 몰아 만들지 않는다.

| 순서 | 화면 | 등급 | 방식 | 게이트 |
|---|---|---|---|---|
| 1 | `New/Home` | P0 | 컴포넌트 인스턴스 조립 | PNG 확인 후 진행. H1~H5 5개 요소 전부 존재 확인 |
| 2 | `New/Results` | P0 | 컴포넌트 인스턴스 조립 | PNG 확인. R1~R5 존재 확인 (R6은 #5에서) |
| — | **P0 게이트** | | | **위 2개가 PNG로 검증되기 전에는 아래로 내려가지 않는다** |
| 3 | `New/Results-FareSheet` | P1 | `New/Results` clone + opacity 0.35 + 시트 | **C-3 준수 확인 — 뒤 목록이 보여야 통과** |
| 4 | `New/Results-FilterSheet` | P1 | `New/Results` clone + opacity 0.35 + 시트 | PNG 확인 |
| 5 | `New/Compare` | P1 | 신규 조립 | 열 2 + 빈 슬롯 1 = 최대 3 확인 |
| 6 | `New/FlightDetail` | P1 | 신규 조립 | 경유 대기 시간 표기 확인 |
| 7 | `New/Watchlist` | P1 | 신규 조립 | **가격 하락 확인 표현 존재 여부** (S2 마감 조건) |
| 8 | `New/DealCollection` | P1 | 신규 조립 | 70% 할인 · 오늘 자정 수치 반영 확인 |
| 9 | `New/DestinationActivities` | P1 | 신규 조립 | 투어·체험·입장권 3종이 모두 등장하는지 확인 |
| 10 | `New/Results-Empty` | P2 | `New/Results` clone | 0건 + 탈출 경로 확인 |
| 11 | `New/Home-FirstRun` | P2 | `New/Home` clone | 여정·담아둠 둘 다 빈 상태인지 확인 |
| 12 | `New/Results-Loading` | P2 | `New/Results` clone | 스켈레톤 6행 확인 |
| 13 | `New/Compare-Empty` | P2 | `New/Compare` clone | `0/3` 확인 |
| 14 | `New/Watchlist-SoldOut` | P2 | `New/Watchlist` clone + 모달 | 뒤 화면이 흐리게 보이는지 확인 |

**보드 배치 (Page `3-toss-result` 캔버스 좌표 가이드)**
- 가로 간격 **490** (390 + 여백 100), 세로 간격 **높이 + 120**.
- 1행: #1 `New/Home` → #12 `New/Home-FirstRun` (base와 변형을 같은 행에)
- 2행: #2 `New/Results` → #6 FareSheet → #5 FilterSheet → #11 Empty → #3 Loading
- 3행: #7 `New/Compare` → #14 Compare-Empty → #4 `New/FlightDetail`
- 4행: #10 `New/Watchlist` → #13 Watchlist-SoldOut → #8 `New/DealCollection` → #9 `New/DestinationActivities`

---

## 7. ⑦ 시각 QA 체크리스트 (필수 요소 커버리지)

| PRD 필수 요소 | 담당 화면 | 확인 항목 |
|---|---|---|
| H1 항공권 검색 진입 | #1 | 출발지·목적지·날짜·인원 4개 필드 모두 보이는가 |
| H2 예정된 여정 | #1, #9 | D-n 표기 + 투어·체험·입장권 제안이 함께 있는가 |
| H3 둘러보기 묶음 | #1, #8 | 갈래가 **여러 개**(4)로 나뉘어 있는가 |
| H4 담아둔 목적지 | #1, #10 | 값 하락을 **확인**하는 표현이 있는가 |
| H5 하단 이동 수단 | #1 외 4화면 | 탭바가 같은 컴포넌트로 일관된가 |
| R1 항공편 목록 | #2 | 출발·도착 시각/소요/경유/항공사/가격 6개 항목 전부 |
| R2 경유 구간 표현 | #2, #4 | **어디서 얼마나** 기다리는지 문자로 있는가 |
| R3 출발일 앞뒤 가격 | #2 | 날짜별 가격이 붙어 있는가, 최저가가 구분되는가 |
| R4 조건 좁히기 | #2, #5 | 진입점 + 시트 둘 다 있는가 |
| R5 비교함 | #2, #7, #14 | 진입점 + **나란히 보는 목적지** 둘 다 있는가 |
| R6 운임 등급 선택 | #6 | **독립 프레임이 아니라** 뒤 Results가 보이는 오버레이인가 |
| E1 40~60건 | #2 | 총 건수가 이 범위인가 (`52건`) |
| E2 최대 3개 | #2, #7, #14 | `n/3` 표기가 일관된가 |
| E3 D-14 | #1, #12 | D-n 형식 + 첫 실행 안내에 14일 근거가 있는가 |
| E4 첫 실행 0/0 | #12 | 여정·담아둠 둘 다 빈 상태인가 |
| E5 0건 | #11 | 0건 + 탈출 경로가 있는가 |
| E6 수 초 로딩 | #3, #2 | 스켈레톤 + 가격 변동 고지 |
| E7 결제 전 마감 | #13 | 마감 표기 + 대체 제안 |
| E8 오늘 자정 / 70% | #1, #8 | 두 수치가 실제 문구로 들어갔는가 |

---

## 8. 이 문서가 확정하지 않은 것 (의도적)

- **색·폰트·간격·라운드 값** — ④의 소관. ②의 실측 결과가 유일한 원천이다.
- **컴포넌트의 실제 치수·내부 오토레이아웃 설정** — ⑤의 소관. 5절은 후보 목록일 뿐이다.
- **사진 자산의 실제 URL** — ⑥이 `penpot.uploadMediaUrl`로 조달한다.
- 위 §2의 높이 값은 **산정치**다. ⑥이 오토레이아웃 결과에 맞게 조정해도 된다.
  **폭 390만은 조정 불가**(PRD 7절).
