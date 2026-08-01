# 05 — 컴포넌트 라이브러리

> 입력: `00-env-facts.md` · `02-design-audit.md` · `03-screen-list.md` · `04-tokens.md`
> 저작 대상: Penpot Page **`3-toss-result`** (id `cf8cfb09-3416-4c32-a2eb-38e95e5c2be9`)
> `3-toss` 는 읽기 전용 — **이 단계에서 열지도, 쓰지도 않았다.**
>
> **화면은 만들지 않았다.** 부품만 만들었다. 화면은 ⑥의 일이다.
> 도메인: **종합 여행 예약**. 증권·금융 용어 없음.

---

## 0. 이 단계의 결론 4줄

1. **`TR/` 접두 컴포넌트 32개**를 저작했다. 전부 `mainInstance()` 살아 있고 감사 이슈 0건.
2. 기존 죽은 36개와 **이름이 겹쳐도 안전**하다 — `path` 로 좁혀 찾기 때문. (§6)
3. **저작 중 함정 3개를 실측으로 발견해 교정했다.** ④의 지침 2개가 실제로는 틀렸다. (§8)
4. **`export_shape` 가 서비스 장애로 전 시도 실패.** PNG 대신 **속성 감사 + SVG 렌더 검증**으로 대체했다. (§9)

---

## 1. 저작 정보

| 항목 | 값 |
|---|---|
| 작업 Page | **`3-toss-result`** |
| Page id | `cf8cfb09-3416-4c32-a2eb-38e95e5c2be9` |
| id 프리픽스 | **`TR/`** (Travel) |
| 컴포넌트 수 | **32** |
| 감사 이슈 | **0** |
| 배치 영역 | **y ≤ -635** (음수 선반). ⑥은 `y >= 0` 에서 저작 |

**Page 게이트 준수**: 모든 저작 호출의 첫 줄에서 `getPageById` 로 Page 를 재고정하고
`name !== "3-toss-result"` 이면 즉시 throw 했다. Page 전환(`openPage`)은 **별도 호출**로
먼저 수행하고 그 다음 호출부터 저작했다.

---

## 2. 컴포넌트 전체 목록 (32개)

**실제 등록 이름은 `path` + `name` 으로 분리 저장된다.** (§6 필독)

| # | path | name | 크기 | 내부 구조 | 오버라이드 |
|---|---|---|---|---|---|
| 1 | `TR / Badge` | `Discount` | 56×22 | Label(11/500) | `characters`, `fills` |
| 2 | `TR / Badge` | `Deadline` | 76×22 | Label(11/500) | `characters`, `fills` |
| 3 | `TR / Badge` | `Lowest` | 43×22 | Label(11/500) | `characters`, `fills` |
| 4 | `TR / Badge` | `Direct` | 34×22 | Label(11/500) | `characters`, `fills` |
| 5 | `TR / Badge` | `Instant` | 55×22 | Label(11/500) | `characters`, `fills` |
| 6 | `TR / Button` | `Primary` | 360×50 | Label(16/700) | `characters`, `fills` |
| 7 | `TR / Button` | `Secondary` | 360×50 | Label(16/700) | `characters`, `fills` |
| 8 | `TR / Chip` | `Default` | 70×30 | Label(12/400) | `characters`, `fills` |
| 9 | `TR / Chip` | `Selected` | 58×30 | Label(12/400) | `characters`, `fills` |
| 10 | `TR / Shell` | `StatusBar` | 390×36 | Time(16/400) + Indicators | `characters` |
| 11 | `TR / Shell` | `TopBar` | 390×60 | BackIcon + Title(16/500, 고정폭 200) + ActionIcon | `characters`, `fills` |
| 12 | `TR / Shell` | `TabBar` | 390×80 | TabItem ×5 (Icon 20 + Label 10/400) | `characters`, `fills` |
| 13 | `TR / Shell` | `HomeIndicator` | 390×34 | Bar 144×5 r12 | — |
| 14 | `TR / FlightRow` | `Direct` | 390×55 | AirlineBlock(Mark 38 + Name/No) + TimeCol(Times 16/700 + Meta) + Price(16/700) | `characters`, `fills` |
| 15 | `TR / FlightRow` | `Stopover` | 390×55 | 동상 (Meta 색 `stopover`) | `characters`, `fills` |
| 16 | `TR / Flight` | `StopoverBar` | 390×27 | Dot + LayoverNote(12/400, 고정폭 300) | `characters` |
| 17 | `TR / PriceDayCell` | `Default` | 76×48 | Day(12) + Price(11/500) | `characters`, `fills` |
| 18 | `TR / PriceDayCell` | `Lowest` | 76×48 | 동상 (틴트 배경) | `characters`, `fills` |
| 19 | `TR / PriceDayCell` | `Selected` | 76×48 | 동상 (brand 배경) | `characters`, `fills` |
| 20 | `TR / PriceDelta` | `Down` | 46×15 | Delta(12/400, priceDown) | `characters`, `fills` |
| 21 | `TR / PriceDelta` | `Up` | 40×15 | Delta(12/400, priceUp) | `characters`, `fills` |
| 22 | `TR / Card` | `DealCard` | 172×196 | Photo 172×108 + Body(City/WasPrice 취소선/NowPrice) | `characters`, `fills`, `fillImage` |
| 23 | `TR / Card` | `ActivityCard` | 390×77 | Photo 57 + Body(Title/RatingRow/Price) | `characters`, `fills`, `fillImage` |
| 24 | `TR / Section` | `SectionHeader` | 390×42 | Title(18/500, 고정폭 240) + MoreLink(13/400) | `characters` |
| 25 | `TR / Watch` | `WatchRow` | 390×58 | CityBlock(Photo 38 + City/Price) + Delta | `characters`, `fills` |
| 26 | `TR / Compare` | `CompareRow` | 390×34 | RowLabel(96) + ValueA(110) + ValueB(110) | `characters`, `fills` |
| 27 | `TR / Compare` | `CompareTray` | 390×68 | Counter(140) + CompareButton | `characters`, `fills` |
| 28 | `TR / Fare` | `FareOption` | 360×153 | Body(Grade/Price/Condition ×3) + Radio 24 | `characters`, `fills` |
| 29 | `TR / State` | `EmptyState` | 390×212 | Icon 57 + Title(고정폭 300) + Description | `characters` |
| 30 | `TR / State` | `SkeletonRow` | 390×72 | Bar ×3 (skeleton 색, r6) | — |
| 31 | `TR / State` | `SuggestionRow` | 390×34 | Label(220) + Count(80, link색) | `characters` |
| 32 | `TR / Common` | `InfoRow` | 390×32 | Label(160) + Value(160) | `characters` |

---

## 3. Variant 위계 (⑥이 이걸 보고 고른다)

같은 역할은 **개별 컴포넌트로 흩지 않고 variant 로 묶었다.** ⑥은 아래 위계로 고른다.

| 역할 | variant (강조 높은 순) | 언제 쓰나 | 한 화면 허용 | ② 근거 |
|---|---|---|---|---|
| **Button** | `Primary` → `Secondary` | Primary = 화면의 주 액션 | **Primary 1개** | ② A-3 "`#4880ee` 유일한 주 액션색" |
| **Chip** | `Selected` → `Default` | 필터·카테고리 | Selected 복수 가능 | ② G8 (47×30, r6) |
| **Badge** | `Deadline` → `Discount` → `Lowest`/`Instant` → `Direct` | 마감>할인>최저>속성 | **유채색 화면당 1~2개** | ② G9 (53×22, r20) |
| **PriceDayCell** | `Selected` → `Lowest` → `Default` | 날짜 스트립 | Selected 1, Lowest 1 | ③ R3 |
| **FlightRow** | `Direct` → `Stopover` | 직항/경유 | 혼재 | ③ R1·R2 |
| **PriceDelta** | `Down`(이득) / `Up`(불리) | 가격 변동 | 혼재 | ④ A-4 |

> **`Direct` 뱃지와 `FlightRow/Direct` 는 다른 것이다.** 전자는 라벨 뱃지, 후자는 행 전체다.
> 뱃지는 `TR / Badge`, 행은 `TR / FlightRow` 로 path 가 갈린다.

---

## 4. 치수 출처 (전부 `02-design-audit.md` 실측)

**M3 규격서(`m3-components_v2.md`)는 이 저장소에 없다.** 따라서 치수는 지시대로
**② 실측값**을 기준으로 삼았다. (오케스트레이터 지시: "치수는 `02`의 실측값을 따르라")

| 컴포넌트 | 높이 | 모서리 | 좌우 패딩 | ② 출처 |
|---|---|---|---|---|
| Badge | **22** | 20 | 7 | G9 (53×22, r20, pad 4/7) |
| Chip | **30** | 6 | 13 | G8 (47×30, r6, pad 8/13/7/13) |
| Button | 50 | 6 | 20 | G8 라운드 + 터치 44 이상 확보 |
| FlightRow | **55** | 20 | 22 | G3 (360×55, pad 7/22) — **주 리스트 행 표준** |
| WatchRow | 58 | 20 | 22 | G3 계열 |
| ActivityCard | 77 | 20 | 22 | G4 (390×69, 아바타 57) 계열 |
| SectionHeader | **42** | — | 22 | G11 (390×42, pad 10/22, 18/500) |
| TabBar | **80** | 20 | 18 | G1 (390×80, r20, gap 50, hairline) |
| StatusBar | **36** | — | 14/16 | G12 (360×36) |
| TopBar | **60** | — | 22 | G15 (390×60, 16/500) |
| HomeIndicator | 34 | 12(bar) | — | G13 (144×5, r12) |

**좌측 정렬선 22 · 아이콘↔텍스트 gap 15 · 카드 r20 / 칩 r6** — ② H절의 형태 시그니처를 전부 지켰다.

---

## 5. ② 실측과 어긋난 항목

| 항목 | ② 실측 | 적용값 | 왜 / 화면에서 어떻게 보이나 |
|---|---|---|---|
| 상태바 폰트 | `SF Pro` 17/400 | **`Noto Sans KR` 16/400** | SF Pro 서버에 없음(`00`). 16은 ④ 스케일 값(17은 미등장 크기라 제외). 시각 차이 미미 |
| Button 높이 | 실측 없음 | **50** | ② F-1 "주 행은 55 이상" 권고와 터치 44 사이에서 결정. 버튼은 행이 아니라 액션이므로 50 |
| WatchRow 높이 | G3 = 55 | **58** | 오토레이아웃 hug 결과. 아바타 38 + pad 7×2 + 2줄 텍스트로 자연 산출 |
| ActivityCard 높이 | G4 = 69 | **77** | 3줄(제목/별점/가격)이라 G4(2줄)보다 큼. 아바타 57·pad 6은 G4 준수 |
| HomeIndicator `#d9d9d9` | OS chrome (② I절 제외) | **그대로 사용** | OS 요소라 토큰 팔레트 밖. 감사기에 명시적 예외로 등록 |

---

## 6. 🔴 인스턴스 생성 방법 (⑥이 쓸 정확한 코드)

### 6-1. 이름 충돌 — 반드시 `path` 로 좁혀라

**Penpot 은 `"TR/Badge/Discount"` 를 `path="TR / Badge"` + `name="Discount"` 로 쪼갠다.**
(슬래시 주변에 공백이 삽입된다.)

기존 죽은 36개 중 **`Discount`(path `Badge`) 가 이미 존재한다.**
→ **`name` 만으로 찾으면 죽은 것이 잡힌다.** 실측으로 확인했다:

| 조회 | path | `mainInstance()` |
|---|---|---|
| `name === "Discount"` 첫 번째 | `Badge` | **`null` (죽음)** |
| `path === "TR / Badge" && name === "Discount"` | `TR / Badge` | **살아 있음** |

```js
// ⑥ 저작 스크립트 맨 위 — Page 재고정
const PAGE = penpotUtils.getPageById("cf8cfb09-3416-4c32-a2eb-38e95e5c2be9");
if (PAGE.name !== "3-toss-result") throw new Error("Page mismatch");

// 🔴 컴포넌트 조회는 반드시 이 함수로. 이름만으로 찾으면 죽은 컴포넌트가 잡힌다.
const findComp = (path, name) => {
  const c = penpot.library.local.components.filter(
    x => x.path === "TR / " + path && x.name === name);
  if (c.length !== 1) throw new Error("조회 실패: TR / " + path + " / " + name);
  return c[0];
};

// 인스턴스 생성 + 오버라이드
const row = findComp("FlightRow", "Direct").instance();
row.x = 0; row.y = 200;
penpotUtils.findShape(s => s.name === "AirlineName", row).characters = "진에어";
penpotUtils.findShape(s => s.name === "Price", row).characters = "₩176,400";
```

### 6-2. 자식 노드 이름 (오버라이드 대상)

`penpotUtils.findShape(s => s.name === "...", instance)` 로 찾는다.

| 컴포넌트 | 자식 이름 |
|---|---|
| `Badge/*` | `Label` |
| `Button/*` | `Label` |
| `Chip/*` | `Label` |
| `FlightRow/*` | `AirlineName` `FlightNo` `Times` `Meta` `Price` `AirlineMark` |
| `Flight/StopoverBar` | `LayoverNote` |
| `PriceDayCell/*` | `Day` `Price` |
| `PriceDelta/*` | `Delta` |
| `Card/DealCard` | `Photo` `City` `WasPrice` `NowPrice` |
| `Card/ActivityCard` | `Photo` `Title` `RatingRow` `Price` |
| `Section/SectionHeader` | `Title` `MoreLink` |
| `Watch/WatchRow` | `CityPhoto` `City` `Price` `Delta` |
| `Compare/CompareRow` | `RowLabel` `ValueA` `ValueB` |
| `Compare/CompareTray` | `Counter` `Label`(버튼 안) |
| `Fare/FareOption` | `Grade` `Price` `Condition-1..3` `Radio` |
| `State/EmptyState` | `Icon` `Title` `Description` |
| `State/SuggestionRow` | `Label` `Count` |
| `Common/InfoRow` | `Label` `Value` |
| `Shell/TabBar` | `TabItem-1..5` → 각 `Icon` `Label` |
| `Shell/TopBar` | `BackIcon` `Title` `ActionIcon` |
| `Shell/StatusBar` | `Time` `Indicators` |

---

## 7. 오버라이드 시험 결과 (실제로 시험함)

| 항목 | 시험 내용 | 됐나 | 비고 |
|---|---|---|---|
| 텍스트 `characters` | `₩232,000` → `₩176,400`, `대한항공` → `진에어` | **✅** | ⑥이 데이터 다른 행을 인스턴스 재사용으로 처리 가능 |
| penpot 형식 `fills` (보드) | 카드 배경 `#17171b` → `#1f2026` | **✅** | `{fillColor, fillOpacity}` 형식이라 뚫린다 |
| penpot 형식 `fills` (자식 텍스트) | 라벨 색 교체 | **✅** | |
| `fontWeight` 유지 | 인스턴스에서 700 유지 | **✅** | |
| 크기 유지 | 390×55 유지 | **✅** | |

> **figma 형식 `fills`(`{type:"SOLID", color:{r,g,b}}`)는 쓰지 않았다.** 전부 penpot 형식이라
> 위 오버라이드가 성립한다. ⑥도 반드시 penpot 형식만 쓸 것.

---

## 8. 🔴 저작 중 실측으로 발견한 함정 3개 (⑥·⑦ 필독)

**④의 지침 중 2개가 실제 환경에서 틀렸다.** 그대로 따르면 조용히 깨진다.

### 8-1. `applyToText` 에 **문자열**을 주면 조용히 400 으로 떨어진다 🔴 가장 위험

`04-tokens.md` G절은 `NOTO.applyToText(node, "700")` 을 지시한다. **이건 작동하지 않는다.**

| 호출 | 결과 `fontWeight` |
|---|---|
| `applyToText(t, "700")` (문자열) | **`400`** ← 에러 없이 무성 실패 |
| `applyToText(t, variant700)` (**FontVariant 객체**) | **`700`** ✅ |
| `t.fontWeight = "700"` (직접 대입) | **throw** `Font weight '700' not supported` |

→ 이 때문에 32개 컴포넌트의 텍스트가 **전부 weight 400 으로 평평**해졌었고,
   **30개 텍스트 노드를 사후 복구**했다. 올바른 코드:

```js
const NOTO = penpot.fonts.findByName("Noto Sans KR");
const VARIANT = {
  "400": NOTO.variants.find(v => v.fontWeight === "400" && v.fontStyle !== "italic"),
  "500": NOTO.variants.find(v => v.fontWeight === "500" && v.fontStyle !== "italic"),
  "700": NOTO.variants.find(v => v.fontWeight === "700" && v.fontStyle !== "italic"),
};
NOTO.applyToText(textNode, VARIANT["700"]);   // 🔴 반드시 객체
```

**⑦ 체크 포인트**: 텍스트 위계가 안 보이면 `fontWeight` 가 전부 400인지 먼저 의심할 것.

### 8-2. hug 텍스트에 `growType="auto-height"` 를 쓰면 **폭이 1로 붕괴**한다

`04` G-1 은 "모든 텍스트 `growType = "auto-height"`" 를 지시하지만, 이건 **고정 폭 칸 전용**이다.
뱃지·버튼 라벨처럼 내용에 맞춰 줄어야 하는 칸에 쓰면 폭이 **1px** 이 되어 컨테이너가 패딩만 남는다
(실측: 뱃지가 15×48 로 붕괴).

| 용도 | growType | 결과 |
|---|---|---|
| hug 라벨 (뱃지·버튼·칩) | **`auto-width`** | 56×22 정상 |
| 고정 폭 칸 (행 제목·가격열) | **`auto-height`** | 폭 유지, 세로만 자람 |

→ 이 문서의 모든 컴포넌트는 이 규칙으로 만들었다. ⑥도 동일하게 적용할 것.

### 8-3. `resize()` 는 `growType` 을 `fixed` 로 되돌린다

고정 폭 칸을 만들 때 `resize()` 직후 **반드시 `growType`을 다시 `auto-height`로 되돌린다.**
안 그러면 Noto 가 Spoqa 보다 넓어 **글자가 잘린다**(② B-2 경고).

---

## 9. ⚠️ 검증 방법 — PNG 대신 무엇을 썼나

**`export_shape` 가 이 세션 내내 실패했다.** 서비스 장애로 판단한다.

| 시도 | 대상 | 결과 |
|---|---|---|
| 9회 이상 | 개별 shape / `page`, `png` / `svg` | `Failed to fetch` → `http error` |
| 대조군 | `use_figma` 코드 실행 | **정상 동작 내내 유지** |

플러그인 연결은 살아 있고 코드 실행은 전부 성공했으므로 **연결 문제가 아니라
export 서비스 자체의 문제**다. 따라서 "PNG 로 눈으로 본다"를 아래 **2중 대체 검증**으로 바꿨다.

### 9-1. 속성 감사기 (전 컴포넌트 32개 통과, 이슈 0)

```js
// 잘림 / 무성 폰트 대체 / 토큰 외 색 / 그림자를 기계적으로 잡는다
storage.audit(board) → string[]
```

검출 항목:
- 텍스트 `width <= 1` 또는 `height <= 1` (**잘림·붕괴**)
- `growType === "fixed"` (**잘림 위험**)
- `fontId` 빈 값 (**무성 폰트 대체**)
- `04` 팔레트 밖 `fillColor` / `strokeColor` (**토큰 이탈**)
- `shadows.length > 0` (**② 실측 0건 — 금지**)

**결과: 32개 전부 이슈 0건.**

### 9-2. SVG 렌더 검증 (실제 렌더 산출물 확인)

`penpot.generateMarkup([main], {type:"svg"})` 로 **실제 렌더 마크업**을 뽑아 확인했다.

| 컴포넌트 | 크기 | SVG 생성 | 텍스트 수 |
|---|---|---|---|
| `Shell/TabBar` | 390×80 | ✅ 40,548 B | 5 |
| `FlightRow/Direct` | 390×55 | ✅ 32,325 B | 5 |
| `Card/DealCard` | 172×196 | ✅ 15,969 B | 3 |
| `Badge/Discount` | 56×22 | ✅ 3,676 B | 1 |
| `Compare/CompareTray` | 390×68 | ✅ 10,748 B | 2 |
| `State/EmptyState` | 390×212 | ✅ 7,123 B | 2 |

`FlightRow/Direct` SVG 안에 `대한항공` · `직항` · `₩232,000` 이 **실제 문자열로 존재**함을 확인했다
(한글 렌더 누락·두부 현상 없음).

> **⑦에게**: `export_shape` 가 복구되면 **가장 먼저 PNG 를 뽑아 육안 확인**할 것.
> 위 검증은 "치수·색·폰트·잘림"은 잡지만 **시각적 균형·정렬 인상**은 잡지 못한다.
> 특히 **8-1 의 weight 복구가 눈으로도 맞는지** 확인이 필요하다.

---

## 10. 배치 좌표 규칙 (⑥이 반드시 지킬 것)

| 영역 | y 범위 | 용도 |
|---|---|---|
| **컴포넌트 선반** | **y ≤ -635** | ⑤가 만든 main instance 32개. **⑥은 건드리지 않는다** |
| **화면 저작 영역** | **y ≥ 0** | ⑥이 `New/*` board 를 놓는 곳 |

컴포넌트 main instance 실측 범위: **x 0~920 / y -1880 ~ -650** (최하단 -635).
③ 6절의 화면 배치 가이드(가로 490 간격, 1행 y=0 시작)와 **겹치지 않는다.**

> main instance 를 옮기거나 이름을 바꾸면 **플러그인이 멈춘다.** ⑥은 `.instance()` 만 쓴다.

---

## 11. ③ 컴포넌트 후보 대비 커버리지

③ 5절 후보 27종 중 **컴포넌트로 승격한 것과 ⑥이 직접 조립할 것**을 구분했다.

| ③ 후보 | 처리 | ⑤ 컴포넌트 |
|---|---|---|
| `BottomTabBar` | ✅ | `Shell/TabBar` |
| `PrimaryButton` / `SecondaryButton` | ✅ | `Button/Primary` · `Button/Secondary` |
| `SectionHeader` | ✅ | `Section/SectionHeader` |
| `Badge` | ✅ 5변형 | `Badge/*` |
| `DealCard` | ✅ | `Card/DealCard` |
| `ActivityCard` | ✅ | `Card/ActivityCard` |
| `FlightRow` | ✅ 2변형 | `FlightRow/Direct` · `Stopover` |
| `LayoverNote` | ✅ | `Flight/StopoverBar` |
| `AirlineMark` | ✅ 내장 | `FlightRow/*` 의 `AirlineMark` |
| `PriceText` | ✅ 내장 | 각 행의 `Price` (16/700) |
| `DateChip` | ✅ 3변형 | `PriceDayCell/*` |
| `FilterChip` | ✅ 2변형 | `Chip/Default` · `Selected` |
| `WatchRow` | ✅ | `Watch/WatchRow` |
| `PriceDelta` | ✅ 2변형 | `PriceDelta/Down` · `Up` |
| `CompareTrayBar` | ✅ | `Compare/CompareTray` |
| `CompareRow` | ✅ | `Compare/CompareRow` |
| `EmptyState` | ✅ | `State/EmptyState` |
| `SkeletonRow` | ✅ | `State/SkeletonRow` |
| `FareOptionCard` | ✅ | `Fare/FareOption` |
| `InfoRow`/`ConditionRow` | ✅ | `Common/InfoRow` |
| `SuggestionRow` | ✅ | `State/SuggestionRow` |
| `RatingRow` | ✅ 내장 | `Card/ActivityCard` 의 `RatingRow` |
| `SegmentedTabs` | ⬜ ⑥ 조립 | `Chip/*` 을 가로로 배열 |
| `SheetGrabber`/`SheetHeader`/`SheetFooter` | ⬜ ⑥ 조립 | 시트 2개(#5·#6)에서만 사용 — 3절 clone 방식이라 컴포넌트 이득 적음 |
| `CheckRow` | ⬜ ⑥ 조립 | `Common/InfoRow` + Radio 응용 |

**미승격 사유**: ③ 5절 하단이 "⑤가 비용 대비 판단해 승격해도 된다. **강제하지 않는다**" 로
위임한 항목이거나, clone 기반이라 인스턴스 이득이 작은 것들이다.

---

## 12. 실패·보류

| 항목 | 무슨 일이 있었나 |
|---|---|
| **`export_shape` PNG 검증** | **전 시도 실패**(9회+, png/svg, shape/page 모두). 코드 실행은 정상이므로 export 서비스 장애로 판단. §9 의 속성 감사 + SVG 렌더 검증으로 대체. **⑦이 복구 후 육안 확인 필요** |
| `m3-components_v2.md` | **저장소에 없다.** 치수 기준을 오케스트레이터 지시대로 `02` 실측값으로 삼았다(§4) |
| 아이콘 SVG 파일 | 이번 실행에서는 **아이콘을 rect/ellipse 플레이스홀더**로 두었다. `TabBar`·`TopBar`의 `Icon`/`BackIcon` 은 이름이 잡혀 있어 ⑥·⑦이 `createShapeFromSvg` 로 교체 가능하다. 도형 조합으로 아이콘 모양을 흉내내지는 **않았다**(오탐 유발 회피) |
| `fontWeight` 사후 복구 | 8-1 함정으로 30개 텍스트가 400 으로 생성됨 → 전부 복구 완료. `StatusBar/Time` 은 과교정(700)되어 400 으로 재수정 |

---

## 13. ⑥으로의 인계 한 줄 요약

> `findComp(path, name)` **로만** 컴포넌트를 찾고(이름만 쓰면 죽은 36개가 잡힌다),
> `.instance()` 후 `characters` 와 **penpot 형식** `fills` 로 덮어라.
> 텍스트를 새로 만들 땐 `applyToText` 에 **FontVariant 객체**를 넘기고(문자열은 400으로 죽는다),
> hug 라벨은 `auto-width` · 고정 폭 칸은 `auto-height` 로 둬라.
> 화면은 **y ≥ 0** 에만 짓는다.
