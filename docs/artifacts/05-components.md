# 05 — 컴포넌트 라이브러리

> 입력: `03-screen-list.md`(화면별 필요 컴포넌트 23종) + `04-tokens.md`(B절 JS 상수)
> 이 단계는 **부품만** 만든다. 화면은 ⑥의 일이다.
> 23종 전부 Penpot에 실제 생성·등록 완료. 전 컴포넌트 PNG 육안 검증 완료.

## 저작 정보

| 항목 | 값 |
|---|---|
| 작업 Page | `김주철` (id `ffc095db-aa26-4198-a59e-1726c8f15b3e`) |
| id 프리픽스 | `KJC/` |
| 등록 컴포넌트 수 | **23 / 23** |
| 저작 영역 | `y = -1400 ~ -1000` (화면 영역과 겹치지 않게 위쪽 음수 y) |
| 폰트 | `Noto Sans KR` (`fontId: "gfont-noto-sans-kr"`) — 400·700 확인 |
| Auto Layout | **23개 보드 + 전 중첩 보드 100% flex** (절대좌표 0개) |

---

## 🔴 ⑥이 먼저 읽어야 할 것 — ⑤가 실제로 부딪힌 API 사실 5가지

이 절은 추측이 아니다. 전부 이 단계에서 실행하며 확인했다.

### 1. `04-tokens.md`의 `applyText()`는 그대로 쓰면 폰트가 안 잡힌다

`04`의 B절 헬퍼는 `f.id` / `v.weight` / `v.id`를 참조하는데 **실제 Penpot API에 그런 필드가 없다.**
실제 필드는 `f.fontId` / `v.fontWeight` / `v.fontVariantId`다.
`04`의 B-2 검증 스니펫이 `has400:false`를 반환한 것이 이 때문이다(폰트는 정상 존재).

```js
// 실측한 Font 객체
{ name:"Noto Sans KR", fontId:"gfont-noto-sans-kr",
  variants:[{ name:"400", fontVariantId:"regular", fontWeight:"400", fontStyle:"normal" }, ...] }
```

**⑥은 아래 D절의 교정된 `applyText()`를 쓴다.** `04` B절 원본을 그대로 붙이면 안 된다.

### 2. 컴포넌트 이름의 `/`는 **name이 아니라 path로 흡수된다**

`KJC/StockRow`로 지으면 저장 결과는 `name:"StockRow"`, `path:"KJC"`다.
따라서 **`c.name === "KJC/StockRow"` 로 찾으면 절대 못 찾는다.**
그리고 프리픽스는 **보드 이름**에 넣어야 path로 남는다 — 컴포넌트 등록 **후** 이름을 바꾸면 path가 날아간다(실제로 겪음).

```js
// ✅ 프리픽스로 좁혀 찾는 유일하게 맞는 방법
const findComp = (short) =>
  penpot.library.local.components.find(
    (c) => c.name === short && String(c.path || "").indexOf("KJC") === 0
  );
```

> 🔴 이 파일에는 이미 **다른 팀원의 `Button` 컴포넌트**가 올라와 있다(path 없음).
> 프리픽스로 안 좁히면 남의 컴포넌트를 인스턴스화한다.

### 3. flex 자식 좌표는 **같은 호출 안에서 읽으면 거짓말을 한다**

`appendChild` 직후 `await`로 아무리 기다려도 같은 tool 호출 안에서는 자식이
`parentX/Y = 0,0`으로 보고된다. **다음 tool 호출에서 읽으면 정상값이 나온다.**

이것 때문에 `AppBar`를 "깨졌다"고 오판하고 한 번 지웠다가 다시 만들었다.
**⑥은 자식 좌표가 0,0으로 보여도 즉시 지우지 말고 다음 호출에서 다시 읽어라.**

### 4. 보드를 옮기기 **전에** 자식을 append 해야 한다

자식은 절대좌표 `(0,0)`에 태어난다.
보드를 먼저 `x/y`로 옮겨두고 그 다음에 append 하면 **flex가 자식을 안 잡고 원점에 남긴다.**

```
✅ 보드 생성(원점) → 자식 append → (대기) → 보드 이동 → 컴포넌트 등록
❌ 보드 생성 → 보드 이동 → 자식 append     // 자식이 원점에 남는다
```

### 5. `export_shape`는 자주 `http error`를 뱉고, 첫 장은 미정착 상태로 찍힌다

- `http error`는 **일시적**이다. 같은 id로 재시도하면 성공한다 (여러 번 겪음).
- 레이아웃 정착 전에 찍히면 요소가 좌상단에 뭉쳐 나온다 → **없다고 판단하기 전에 재-export 1회.**
  `TabBar`가 실제로 첫 장은 뭉쳐 나왔고 두 번째 장은 정상이었다.
- `shapeId:"page"`(전체 페이지) export는 **30초 타임아웃으로 실패한다.** 컴포넌트 단위로 찍어라.

---

## A. 컴포넌트 목록 (23종)

크기 단위는 px. `오버라이드`는 ⑥이 인스턴스에서 바꿔도 되는 자식 **이름**이다.

### 원자

| 컴포넌트 | 크기 | 내부 구조 (자식 이름) | 오버라이드 가능 | PNG |
|---|---|---|---|---|
| `KJC/ChangeBadge` | 64×24 | `Value` | `characters` / 보드 `fills`(틴트) / `Value.fills` | ✅ |
| `KJC/ChipToggle` | 96×32 | `Label` | `characters` / 보드 `fills`·`strokes` / `Label.fills` | ✅ |
| `KJC/SectionHeader` | 358×28 | `Title`, `More` | 둘 다 `characters` / `More.hidden`으로 더보기 제거 | ✅ |
| `KJC/SkeletonRow` | 358×72 | `BarWide`, `BarNarrow` | 각 바 `resize()`로 폭 변주 | ✅ |
| `KJC/DividerBlock` | 390×4 | (없음) | 없음 — 섹션 구분 블록 | ✅ |

### 기본

| 컴포넌트 | 크기 | 내부 구조 | 오버라이드 가능 | PNG |
|---|---|---|---|---|
| `KJC/PrimaryButton` | 358×48 | `Label` | `characters` / 보드 `fills`(매수 red·매도 blue·비활성) | ✅ |
| `KJC/SearchField` | 358×44 | `SearchIcon`, `Placeholder` | `Placeholder.characters`·`fills`(입력값 있으면 primary) | ✅ |
| `KJC/InfoKeyValue` | 358×40 | `Key`, `Value` | 둘 다 `characters` / `Value.fills`(강조) | ✅ |
| `KJC/AppBar` | 390×52 | `BackIcon`, `Title`, `ActionIcon` | `Title.characters` / 아이콘 `hidden`으로 좌우 슬롯 제거 | ✅ |
| `KJC/TabBar` | 390×58 | `Tab-관심`·`Tab-발견`·`Tab-검색`·`Tab-내정보` (각 `Icon`+`Label`) | 각 탭 `Icon.fills`·`Label.fills`로 활성 인덱스 이동 | ✅ |

### 복합

| 컴포넌트 | 크기 | 내부 구조 | 오버라이드 가능 | PNG |
|---|---|---|---|---|
| `KJC/StockRow` | 358×72 | `Info`(`Name`,`Code`) · `Metrics`(`Price`,`Change`) | 4개 전부 `characters` / `Change.fills` | ✅ |
| `KJC/RecommendCard` | 358×92 | `Head`(`Name`,`PriceChange`) · `Reason` | 3개 `characters` / `PriceChange.fills` | ✅ |
| `KJC/IssueCard` | 358×96 | `Head`(`Tag`>`TagLabel`, `Title`) · `RelatedStocks` | `TagLabel`·`Title`·`RelatedStocks` `characters` / `Tag.fills`(호재↔악재) | ✅ |
| `KJC/ConsensusBar` | 358×76 | `Head`(`Label`,`TargetPrice`) · `Bar`(`SegBuy`,`SegHold`,`SegSell`) · `Legend`(`BuyCount`,`HoldCount`,`SellCount`) | 텍스트 전부 / 세그먼트는 `resize(w,12)`로 비율 조정 | ✅ |
| `KJC/EarningsRow` | 358×44 | `Name` · `Meta`(`Date`, `SurpriseBadge`>`SurpriseLabel`) | 텍스트 `characters` / `SurpriseBadge.hidden` | ✅ |
| `KJC/ThemeCard` | 172×88 | `ThemeName`, `ThemeChange`, `TopStocks` | 3개 `characters` / `ThemeChange.fills` | ✅ |
| `KJC/PeriodTabs` | 358×32 | `Seg-1일`~`Seg-1년` (각 `Label`) | 각 `Seg-*.fills` + `Label.fills`로 활성 이동 | ✅ |
| `KJC/ListRowSelectable` | 358×44 | `Text`(`Label`,`Description`) · `Check` | 텍스트 `characters` / `Check.fills`·`hidden` | ✅ |
| `KJC/StatusBanner` | 358×44 | `Icon`, `Message`, `Action` | `characters` / 보드·`Icon`·`Message` `fills`(error↔info) | ✅ |
| `KJC/EmptyState` | 358×220 | `Illustration`, `Title`, `Description` | 텍스트 `characters` | ✅ |
| `KJC/QuantityStepper` | 358×44 | `Minus`, `Value`, `Plus` | `Value.characters` / `Minus`·`Plus` `fills`(활성 여부) | ✅ |
| `KJC/BottomSheet` | 390×280 | `Handle`, `Title`, `ContentSlot` | `Title.characters` / `ContentSlot`에 자식 append / 보드 `resize`로 높이 | ✅ |
| `KJC/StyleSetupPromptCard` | 358×108 | `Title`, `Description`, `CTA`>`CTALabel` | 3개 `characters` | ✅ |

> `BottomSheet`의 `ContentSlot`은 **일부러 빈 column flex 보드**다.
> ⑥이 여기에 `ListRowSelectable`·`QuantityStepper` 인스턴스를 append 하면 자동 정렬된다.

---

## B. 오버라이드 시험 결과 (실제로 인스턴스 만들어서 시험함)

| 컴포넌트 | 바꾼 것 | 됐나 | 비고 |
|---|---|---|---|
| `ChangeBadge` | `Value.characters` `+2.45%`→`−1.08%` | ✅ | |
| `ChangeBadge` | `Value.fills` red→blue, 보드 `fills` 틴트 교체 | ✅ | penpot 형식이라 통과 |
| `StockRow` | `Name`·`Code`·`Price`·`Change` 4개 `characters` 동시 | ✅ | 중첩 2단계 자식도 오버라이드됨 |
| `StockRow` | `Change.fills` → `changeColor(-1.32)` | ✅ | 하락 파랑 정상 적용 |
| `ChipToggle` | 보드 `fills`+`strokes`+`Label.fills` 3개 동시 (off→on) | ✅ | 선택 상태를 인스턴스로 표현 가능 |
| `PrimaryButton` | 보드 `fills` red→blue + `Label.characters` | ✅ | 매수/매도 변형이 인스턴스로 해결 |
| **원본 무결성** | 위 전부 수행 후 main 컴포넌트 재확인 | ✅ | `삼성전자`/`+2.45%`/`#e72336` 그대로 |

**결론: ⑥은 새 도형을 그릴 필요가 없다.** 23종 인스턴스 + `characters`/`fills` 오버라이드로 조립된다.

> ⚠️ 중첩 자식(`Info > Name`)을 찾을 땐 `inst.children[0].children[0]` 같은 인덱스 접근 대신
> **이름으로 찾아라.** 인덱스는 flex 정착 타이밍에 따라 흔들린다.
> ```js
> const byName = (root, n) => penpotUtils.findShape(s => s.name === n, root);
> ```

---

## C. 인스턴스 생성 방법 (⑥이 그대로 쓰는 코드)

```js
// ───────── 모든 스크립트 첫 줄에서 Page 재고정 (openPage는 다음 호출까지 유지되지 않는다)
penpot.openPage(penpotUtils.getPageByName("김주철"));

// ───────── 프리픽스로 좁혀 찾기 (남의 컴포넌트가 잡히는 것을 막는다)
const findComp = (short) =>
  penpot.library.local.components.find(
    (c) => c.name === short && String(c.path || "").indexOf("KJC") === 0
  );

// ───────── 이름으로 자식 찾기 (인덱스 접근 금지)
const byName = (root, n) => penpotUtils.findShape((s) => s.name === n, root);

// ───────── 인스턴스 1개 만들고 데이터 얹기
const row = findComp("StockRow").instance();
byName(row, "Name").characters  = "SK하이닉스";
byName(row, "Code").characters  = "000660";
byName(row, "Price").characters = "184,500";
const ch = byName(row, "Change");
ch.characters = changeLabel(-1.32);       // "−1.32%"
ch.fills      = fill(changeColor(-1.32)); // 하락 → #236ae7
// 부모 보드(화면)에 붙인다. 부모가 flex면 위치는 자동.
screenBoard.appendChild(row);
```

### 리스트를 채우는 표준 패턴 (Watchlist·ThemeDetail·StockSearch 공용)

```js
const STOCKS = [
  { name: "삼성전자",     code: "005930", price: "71,200",  chg:  2.45 },
  { name: "SK하이닉스",   code: "000660", price: "184,500", chg: -1.32 },
  { name: "한미반도체",   code: "042700", price: "98,400",  chg:  5.12 },
  { name: "LG에너지솔루션", code: "373220", price: "412,000", chg:  0    },
];
const comp = findComp("StockRow");
STOCKS.forEach((s) => {
  const r = comp.instance();
  byName(r, "Name").characters  = s.name;
  byName(r, "Code").characters  = s.code;
  byName(r, "Price").characters = s.price;
  const c = byName(r, "Change");
  c.characters = changeLabel(s.chg);
  c.fills      = fill(changeColor(s.chg));
  listBoard.appendChild(r);   // listBoard = column flex, rowGap = T.space.xl(32) 권장
});
```

### 상태 변형 오버라이드 치트시트

```js
// 칩 선택(on)
chip.fills   = fill(T.color.brand.primary);
chip.strokes = stroke(T.color.brand.primary, 1);
byName(chip, "Label").fills = fill(T.color.text.inverse);

// 버튼 매도(파랑) / 비활성
btn.fills = fill(T.color.state.down);
btn.fills = fill(T.color.border.strong);   // disabled

// 탭바 활성 인덱스 이동 (i번째만 브랜드색)
["관심","발견","검색","내정보"].forEach((l, i) => {
  const on = i === activeIndex;
  const tab = byName(bar, "Tab-" + l);
  byName(tab, "Icon").fills  = fill(on ? T.color.brand.primary : T.color.text.secondary);
  byName(tab, "Label").fills = fill(on ? T.color.brand.primary : T.color.text.secondary);
});

// 기간 탭 활성 이동
["1일","1주","1개월","3개월","1년"].forEach((l, i) => {
  const on = i === activePeriod;
  const seg = byName(tabs, "Seg-" + l);
  seg.fills = on ? fill(T.color.bg.surface) : [];
  byName(seg, "Label").fills = fill(on ? T.color.text.primary : T.color.text.secondary);
});

// StatusBanner 톤 전환 (error ↔ info)
banner.fills = fill(T.color.state.errorTint);          // 또는 brand.tint
byName(banner, "Icon").fills    = fill(T.color.state.error);
byName(banner, "Message").fills = fill(T.color.state.error);

// ConsensusBar 비율 조정 (합이 358이 되게)
byName(bar, "SegBuy").resize(200, 12);
byName(bar, "SegHold").resize(100, 12);
byName(bar, "SegSell").resize(58, 12);

// 로딩 변형: StockRow의 가격·등락만 스켈레톤처럼 (종목명 유지)
byName(row, "Price").characters  = "";
byName(row, "Change").characters = "";
```

---

## D. 저작 코드 맨 위에 붙일 전문 (⑥ 복붙용 · **교정판**)

> `04-tokens.md` B절 그대로 + **`applyText()`만 실제 API에 맞게 교정**했다.
> 토큰 값은 하나도 바꾸지 않았다.

```js
penpot.openPage(penpotUtils.getPageByName("김주철"));   // 🔴 항상 첫 줄

const T = { /* 04-tokens.md B절 T 객체 전체를 그대로 붙인다 */ };

const fill = (hex, opacity = 1) => [{ fillColor: hex, fillOpacity: opacity }];
const stroke = (hex = T.color.border.default, width = 1) => [
  { strokeColor: hex, strokeWidth: width, strokeAlignment: "inner", strokeOpacity: 1 },
];
const findFont = (name) => penpot.fonts.all.find((f) => f.name === name);

// 🔴 교정: f.id→f.fontId, v.weight→v.fontWeight, v.id→v.fontVariantId
const applyText = (node, o) => {
  const weight     = o.weight     === undefined ? T.font.weight.regular    : o.weight;
  const color      = o.color      === undefined ? T.color.text.primary     : o.color;
  const lineHeight = o.lineHeight === undefined ? T.font.lineHeight.normal : o.lineHeight;
  const f = findFont(T.font.family);
  if (f) {
    node.fontId = f.fontId;
    node.fontFamily = f.name;
    const v = f.variants.find((x) => String(x.fontWeight) === String(weight));
    if (v) { node.fontVariantId = v.fontVariantId; node.fontWeight = String(weight); }
  }
  node.fontSize      = String(o.size);
  node.lineHeight    = String(lineHeight);
  node.letterSpacing = String(T.font.letterSpacing);
  node.fills         = fill(color);
  node.growType      = "auto-height";
  if (o.align) node.align = o.align;
  return node;
};

const changeColor = (v) => v > 0 ? T.color.state.up     : v < 0 ? T.color.state.down     : T.color.state.flat;
const changeTint  = (v) => v > 0 ? T.color.state.upTint : v < 0 ? T.color.state.downTint : T.color.bg.avatar;
const changeLabel = (v) => (v > 0 ? "+" : v < 0 ? "−" : "") + Math.abs(v).toFixed(2) + "%";

const findComp = (short) =>
  penpot.library.local.components.find(
    (c) => c.name === short && String(c.path || "").indexOf("KJC") === 0
  );
const byName = (root, n) => penpotUtils.findShape((s) => s.name === n, root);

// 🔴 고정 폭 텍스트: resize 후 반드시 auto-height로 되돌린다(안 그러면 글자가 잘린다)
const mkText = (chars, o) => {
  const t = penpot.createText(chars);
  applyText(t, o);
  if (o.width !== undefined) {
    t.growType = "fixed";
    t.resize(o.width, o.height || Math.ceil(o.size * 1.34));
    t.growType = "auto-height";
  }
  if (o.name) t.name = o.name;
  return t;
};
```

---

## E. ⑥에게 넘기는 조립 규칙

1. **새 도형을 그리지 않는다.** 23종 인스턴스로 조립한다. 없는 부품이 필요하면 ⑤로 돌아온다.
2. 화면 보드는 `390` 폭 · **column flex** · `horizontalPadding = 16`.
   단 `AppBar`·`TabBar`·`DividerBlock`은 폭이 390이므로 **패딩 밖(전폭)** 에 둔다.
   → 화면 보드 패딩을 0으로 두고, 콘텐츠만 358 폭 내부 보드로 감싸는 편이 안전하다.
3. 리스트 행 사이는 `T.space.xl(32)`이 아니라 **`rowGap = 0` + 행 자체 높이 72**를 쓴다.
   (`StockRow`가 이미 상하 16 패딩을 품고 있다.)
4. 하단 고정 액션의 Spacer 높이는 **`657`** (`04` A-8 계산값). `layoutGrow`를 쓰지 않는다.
5. 스크림을 만들지 않는다. **뒤 화면 보드의 `opacity`를 낮춘다.**
6. 자식 좌표가 `0,0`으로 보여도 **다음 호출에서 다시 읽기 전에는 깨졌다고 판단하지 않는다.**
7. `export_shape`가 `http error`면 **재시도**한다. 첫 장이 뭉쳐 나오면 **재-export 1회.**
8. 마감 처리: 전 화면의 `growType === "auto-height"` 텍스트를 `resize`로 재계산시킨다.

---

## F. 실패·보류

| 항목 | 무슨 일이 있었나 |
|---|---|
| `04-tokens.md` B절 `applyText()` | `f.id`/`v.weight`/`v.id`가 실제 API에 없어 **폰트가 안 잡혔다.** D절에서 교정. `04`의 B-2 스니펫이 `has400:false`를 낸 것도 같은 원인이며, **폰트 자체는 정상 존재**한다 |
| `ChangeBadge` 1차 시도 | 등록 후 컴포넌트 이름을 바꿨더니 `path`가 날아가 프리픽스 조회가 실패. **지우고 새 이름으로 다시** 만들었다(이름 변경 금지 규칙대로) |
| `ChipToggle`·`SectionHeader`·`SkeletonRow` 1차 시도 | 보드를 먼저 이동시킨 뒤 자식을 append 해 자식이 원점에 남았다. **지우고 순서를 바꿔 재작성** |
| `AppBar` 1차 시도 | 실제로는 정상이었는데 **같은 호출 안에서 읽은 0,0 보고를 믿고** 지웠다. 재작성 후 정상 확인. ⑥은 이 실수를 반복하지 말 것 |
| 한 호출에 3개 컴포넌트 저작 | `await` 누적으로 **30초 타임아웃.** 이후 **1~2개씩** 쪼개 실행 |
| 전체 페이지 `export_shape` | `shapeId:"page"`는 30초 타임아웃. **컴포넌트 단위로만** 검증했다 |
| 아이콘 | 실제 아이콘 패스가 없어 **`T.size.icon` 사각형 placeholder**로 뒀다(`BackIcon`·`ActionIcon`·`Tab-*/Icon`·`SearchIcon`·`Check`). ⑦이 아이콘 부재를 지적하면 ⑥이 `penpot.createPath` 또는 `uploadMediaUrl`로 교체 |
| `PriceChart` | **23종 중 유일하게 만들지 않았다.** 폴리라인은 데이터 의존이라 컴포넌트화 이득이 없고 `StockDetail` 1곳에서만 쓰인다 → **⑥이 `penpot.createPath`로 직접 그린다**(`PeriodTabs`는 만들어 뒀다) |
| 남의 컴포넌트 | 이 파일에 path 없는 `Button` 컴포넌트가 이미 존재. **프리픽스 조회 필수** |

> 미룬 것은 `PriceChart` 하나뿐이다. ③이 요구한 나머지 22종 + `DividerBlock`(②G절 구획 규칙)까지 **23종 등록 완료.**
