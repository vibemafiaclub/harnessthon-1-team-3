# 04 — 디자인 토큰

> 입력: `02-design-audit.md` (실측) + `03-screen-list.md` (14화면 · 컴포넌트 23종)
> 이 문서의 값은 ②의 빈도순 상위값을 승격하거나, ③이 요구하는데 ②에 없어 **기존 팔레트에서 파생**한 것이다.
> ②의 **H절(예외)** 값은 하나도 승격하지 않았다.
> **B절 JS 상수 객체가 이 단계의 산출물이다.** ⑤⑥은 B절을 저작 코드 맨 위에 그대로 붙여 쓴다.

## 출처 요약

| 항목 | 개수 | 비고 |
|---|---|---|
| ②에서 승격 | **26** | 색 9 · 간격 5 · 반경 2 · 타이포 7 · 화면규격 3 |
| ③ 요구로 파생 | **8** | 등락 색 3 + 등락 틴트 2 + 성공/실패 2 + 성공 틴트 1 |
| 미결 판단 확정 | **2** | 한글 폰트 · SF Pro Text 대체 (아래 C절) |
| 확인 필요 | **3** | D절 |

---

## A. 토큰 표 (사람이 읽는 용)

### A-1. 색 — 브랜드

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.brand.primary` | `#ff7e36` | ② 빈도 16회 | **액센트 전용.** 가격·주 CTA·FAB·브랜드 배너에만. **면으로 깔지 않는다** (②G절) |
| `color.brand.tint` | `#ffebe0` | ② 빈도 5회 | 원형 아이콘 칩 배경. 브랜드 연한 배경 |

> 🔴 `brand.primary`는 813노드 중 16회뿐이다. ⑥이 헤더·섹션 배경에 오렌지를 깔면 이 제품으로 안 보인다.

### A-2. 색 — 텍스트 / 배경 / 선

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.text.primary` | `#000000` | ② 빈도 175회 (1위) | 제목·본문·주요 숫자 |
| `color.text.secondary` | `#8c8c8c` | ② 빈도 80회 (2위) | 위치·시간·메타·비활성 |
| `color.text.tertiary` | `#5e5e5e` | ② 빈도 12회 | 보조 텍스트(진한 회색). 2단계로 부족할 때만 |
| `color.text.inverse` | `#ffffff` | ② 빈도 72회 중 반전 텍스트 | 컬러 버튼 위 라벨 |
| `color.bg.surface` | `#ffffff` | ② 빈도 72회 | 화면·카드 배경 |
| `color.bg.placeholder` | `#d9d9d9` | ② 빈도 33회 | 썸네일·아바타 이미지 자리 |
| `color.bg.avatar` | `#f4f4f4` | ② 빈도 6회 | 아바타 배경 |
| `color.border.default` | `#eeeeee` | ② stroke 빈도 28회 (1위) | **1px 구분선·칩 테두리 — 이 제품의 경계 규칙** |
| `color.border.strong` | `#d9d9d9` | ② stroke 빈도 10회 | 보조 구분선 |
| `color.divider.block` | `#eeeeee` | ② 빈도 10회 (rectangle) | **높이 4px 섹션 구분 블록** (②G절: 이 제품의 구획 방식) |

> 텍스트 위계는 `#000000` → `#8c8c8c` **2색이 압도적**이다(175:80). `text.tertiary`는 남용하지 않는다.

### A-3. 색 — 등락 (③ 요구 · ②에 없음 → **파생**)

③의 `ChangeBadge`(5화면·화면당 5~20회)·`StockRow`가 상승/하락 구분을 요구한다. ②의 팔레트에 대응물이 없다.

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.state.up` | `#e72336` | **③ 요구 · `#ff7e36`에서 파생** | 상승 (+). 가격·등락률·매수 |
| `color.state.down` | `#236ae7` | **③ 요구 · `up`의 보색 대칭 파생** | 하락 (−). 가격·등락률·매도 |
| `color.state.flat` | `#8c8c8c` | ② `text.secondary` 재사용 | 보합 (0). 새 색을 만들지 않았다 |
| `color.state.upTint` | `#ffe0e3` | **파생 · `#ffebe0`의 S/L 복제** | 상승 배지 배경 |
| `color.state.downTint` | `#e0ebff` | **파생 · `#ffebe0`의 S/L 복제** | 하락 배지 배경 |

**파생 근거 (숫자로 검산함):**

| 기준색 | HSL | 파생색 | HSL | 무엇을 맞췄나 |
|---|---|---|---|---|
| `#ff7e36` (브랜드) | H 21.5 / S 100 / L 60.6 | — | — | 기준 |
| — | — | `#e72336` (up) | H **354.2** / S 80.3 / L 52.2 | 한국 증권 관례 = 상승 red. 브랜드 H21.5에서 **332° 떨어뜨려** 오렌지와 혼동되지 않게 했다 |
| `#e72336` (up) | H 354.2 / S 80.3 / L 52.2 | `#236ae7` (down) | H **218.3** / S **80.3** / L **52.2** | **S·L을 소수점까지 동일하게** 고정. 상승/하락이 같은 시각 무게로 읽혀야 한다 |
| `#ffebe0` (브랜드 틴트) | H 21.3 / S 100 / L 93.9 | `#ffe0e3` / `#e0ebff` | S 100 / L 93.9 | 기존 틴트의 **S·L을 그대로 복제**하고 색상만 up/down 각각으로 회전 |

**명도 대비 검산 (WCAG, 흰 배경 기준):**

| 조합 | 대비 | 판정 |
|---|---|---|
| `up` `#e72336` on `#ffffff` | **4.48:1** | 가격 텍스트 통과 |
| `down` `#236ae7` on `#ffffff` | **4.90:1** | 가격 텍스트 통과 |
| `#ffffff` on `up` | **4.48:1** | 매수 버튼 라벨 통과 |
| `#ffffff` on `down` | **4.90:1** | 매도 버튼 라벨 통과 |
| (참고) `brand` `#ff7e36` on `#ffffff` | 2.53:1 | **브랜드색은 큰 텍스트·면에만.** 작은 본문에 쓰지 않는다 |

> 🔴 왜 ②의 `#4ac1db`를 쓰지 않았나 — H절(예외)에 있다. `_5`의 "매너온도" 전용이고 증권 도메인에 대응물이 없다.

### A-4. 색 — 주문 결과 (③ 요구 · ②에 없음 → **파생**)

③ #5 `OrderComplete`(체결/접수) · #13 `OrderFailed`(잔고부족·장마감) · `StatusBanner`가 요구한다.

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.state.success` | `#1c9c5c` | **③ 요구 · 파생** | 주문 체결 완료 |
| `color.state.successTint` | `#e0ffef` | **파생 · `#ffebe0`의 S/L 복제** | 완료 배너 배경 |
| `color.state.error` | `#e72336` | **`state.up` 재사용** | 주문 실패·경고 |
| `color.state.errorTint` | `#ffe0e3` | **`state.upTint` 재사용** | 실패 배너 배경 |

**파생 근거:** `success`는 up/down이 차지하지 않은 녹색대(H150)에 두되, **L을 36.1까지 낮췄다.** up/down(L52.2)과 같은 L로 두면 녹색이 화면에서 가장 밝게 튄다 — 등락이 주인공인 화면에서 성공색이 시선을 뺏으면 안 된다.

> 🔴 `error`에 새 색을 만들지 않고 `state.up`을 재사용했다. 새 빨강을 발명하면 한 화면에 빨강이 2종 생겨 등락 신호가 무너진다. **주문 실패 화면에는 등락 표시가 없으므로 충돌하지 않는다.**

### A-5. 간격 (②의 4의 배수 스케일)

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `space.xs` | `4` | ② 빈도 47회 | 텍스트 줄 사이 (제목↔메타) |
| `space.sm` | `8` | ② 빈도 20회 | 요소 간 · 칩 상하 padding · 칩 사이 gap |
| `space.md` | `12` | ② 빈도 11회 | 칩 좌우 padding · 배너 내부 padding |
| `space.lg` | `16` | ② 빈도 23회 gap + **좌우여백 160회** | **화면 좌우 여백(고정) · 블록 간 여백 · 썸네일↔텍스트 gap** |
| `space.xl` | `32` | ② 실측 (행 피치 142 − 행 높이 110) | 리스트 행 사이 · 섹션 사이 |

**정규화 내역:** ②의 예외값 `2`(4회) → `4`로, `24`(2회) → `32`로 흡수. `27`·`17.5`는 StatusBar 내부 좌표라 레이아웃 여백이 아니므로 스케일에 넣지 않았다(②H절).

> 🔴 ②G절: 기존 파일은 **오토레이아웃 프레임이 0개**다. ⑤⑥은 기존을 흉내내면 안 되고 이 스케일을
> **`padding`·`gap`으로 옮겨 담아야** 평가 기준 "Auto Layout"을 만족한다. 절대좌표로 그리면 감점이다.

### A-6. 모서리 반경

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `radius.default` | `4` | ② 빈도 30회 (1위) | **썸네일·버튼·카드 — 기본값** |
| `radius.pill` | `100` | ② 빈도 17회 | 칩·원형 아이콘·아바타·FAB |

**정규화 내역:** ②의 `96`(6회)은 원형 의도의 변형 → `100`으로 통일. `8`(2회)·`24`(5회, OS자산)는 H절 → 승격 안 함.

> 🔴 ②G절: **이 제품은 라운드가 작다(4px).** ⑤⑥은 8·12·16 라운드를 발명하면 안 된다.

### A-7. 타이포 스케일

| 토큰 이름 | size / weight | 출처 | 역할 |
|---|---|---|---|
| `font.size.caption` + `weight.regular` | 12 / 400 | ② 빈도 **92회 (1위)** | 메타·보조 텍스트·칩 라벨 |
| `font.size.tabLabel` + `weight.regular` | 10 / 400 | ② 빈도 20회 | 탭바 라벨 |
| `font.size.body` + `weight.regular` | 14 / 400 | ② 빈도 24회 | 본문 |
| `font.size.body` + `weight.bold` | 14 / 700 | ② 빈도 23회 | 버튼 라벨 · 강조 본문 |
| `font.size.title` + `weight.regular` | 16 / 400 | ② 빈도 16회 | 리스트 아이템 제목(종목명) |
| `font.size.title` + `weight.bold` | 16 / 700 | ② 빈도 3회 | 섹션 헤더 |
| `font.size.price` + `weight.bold` | 15 / 700 | ② 빈도 5회 | **가격 (강조)** |
| `font.size.header` + `weight.bold` | 18 / 700 | ② 빈도 5회 | 화면 헤더 타이틀 |

**위계:** 헤더 18/700 → 섹션 16/700 → 아이템 제목 16/400 → 가격 15/700 → 본문 14/400 → 캡션 12/400 → 탭 10/400.

**weight는 400·700 두 값만 있다.** ②B절 — 중간 웨이트(500/600)는 기존 파일에서 **한 번도 쓰이지 않았다.** 발명하지 않는다.
**letterSpacing은 전부 0.** 제품 텍스트 205개 전수 0이었다.
**lineHeight**는 ②의 본문 대역 1.25~1.33을 따른다. `1.8`·`1.5`는 H절(1회성) → 승격 안 함.

### A-8. 화면 규격

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `screen.width` | `390` | ② 5개 화면 전부 | 프레임 폭 |
| `screen.height` | `844` | ② `_1`,`_4` | 기본 화면 높이 (롱스크롤은 콘텐츠만큼 늘림) |
| `screen.padding` | `16` | ② 빈도 160회 | 좌우 여백 |
| `screen.contentWidth` | `358` | 390 − 16×2 | 콘텐츠 폭 |
| `size.statusBar` | `47` | ② 5개 화면 전부 | 상태바 높이 |
| `size.appBar` | `52` | ② `Frame 3` | 화면 헤더 높이 |
| `size.tabBar` | `58` | ② `Frame 19` | 탭바 높이 |
| `size.homeIndicator` | `34` | ② 5개 화면 전부 | 홈 인디케이터 |
| `size.bottomAction` | `54` | ② `_5` `Frame 20` | 하단 고정 액션바 (StockDetail 매수/매도) |
| `size.icon` | `24` | ② 빈도 **48회 (1위)** | 아이콘 기본 |
| `size.fab` | `48` | ② `Frame 21` | FAB · 원형 아이콘 칩 |
| `size.chipHeight` | `32` | ② `Frame 26~30` | 칩 최소 터치 높이 |
| `size.rowMenu` | `44` | ② `_3` 13회 | 메뉴 행 |
| `size.rowList` | `72` | ② `_4` 10회 (72.01 반올림) | 리스트 행 (StockRow 기준) |
| `size.dividerBlock` | `4` | ② `Rectangle 3/4` | 섹션 구분 블록 높이 |

> 🔴 ③ #2 `StockDetail`의 하단 고정 액션 — ②AGENTS 함정: `layoutGrow` Spacer가 폭 1로 되돌아간다.
> **Spacer 높이를 계산해서 명시**한다: `844 − 47(status) − 52(appBar) − 54(action) − 34(home) = 657`.

### A-9. 그림자

| 토큰 이름 | 값 | 출처 | 역할 |
|---|---|---|---|
| `shadow.fab` | offset(0,4) blur 12 spread 0 `#000000` @0.12 | ② 빈도 2회 (FAB 전용) | **FAB에만.** 카드·시트·바에는 쓰지 않는다 |

> ②F-2: 그림자는 파일 전체에 **1종·2회뿐**이다. 깊이는 `#eeeeee` 1px 선과 4px 블록으로 낸다.
> ③의 `BottomSheet`도 그림자 대신 상단 1px `border.default`로 경계를 낸다.

---

## B. 저작용 JS 상수 (⑤⑥이 그대로 복붙한다)

```js
// ===== 04-tokens :: 디자인 토큰 =====
// 출처: 02-design-audit(실측) + 03-screen-list(요구). 임의값 없음.
// figma.variables.* 는 쓰지 않는다 — 성공 응답만 오고 토큰이 남지 않는다.
const T = {
  color: {
    brand: {
      primary: "#ff7e36",   // ② 16회. 액센트 전용 — 면으로 깔지 말 것
      tint:    "#ffebe0",   // ② 5회
    },
    text: {
      primary:   "#000000", // ② 175회
      secondary: "#8c8c8c", // ② 80회
      tertiary:  "#5e5e5e", // ② 12회
      inverse:   "#ffffff",
    },
    bg: {
      surface:     "#ffffff", // ② 72회
      placeholder: "#d9d9d9", // ② 33회
      avatar:      "#f4f4f4", // ② 6회
    },
    border: {
      default: "#eeeeee",   // ② stroke 28회 — 1px 구분선 규칙
      strong:  "#d9d9d9",   // ② stroke 10회
    },
    divider: {
      block: "#eeeeee",     // 높이 4px 섹션 구분 블록
    },
    state: {
      up:          "#e72336", // 파생: 브랜드 H21.5→H354.2, S80.3/L52.2
      down:        "#236ae7", // 파생: up의 S·L 동일 고정, H218.3
      flat:        "#8c8c8c", // ② text.secondary 재사용
      upTint:      "#ffe0e3", // 파생: #ffebe0의 S100/L93.9 복제
      downTint:    "#e0ebff", // 파생: 동일
      success:     "#1c9c5c", // 파생: H150, L36.1로 낮춤(등락보다 덜 튀게)
      successTint: "#e0ffef",
      error:       "#e72336", // state.up 재사용 — 새 빨강 발명 금지
      errorTint:   "#ffe0e3",
    },
  },
  space: { xs: 4, sm: 8, md: 12, lg: 16, xl: 32 },
  radius: { default: 4, pill: 100 },
  font: {
    family: "Noto Sans KR",  // 한글 렌더 확정 (C절). 완전일치로 조회할 것
    size: {
      tabLabel: 10,
      caption:  12,
      body:     14,
      price:    15,
      title:    16,
      header:   18,
    },
    weight: { regular: 400, bold: 700 },  // ② 400·700 두 값만. 500/600 발명 금지
    lineHeight: { tight: 1.25, normal: 1.33 },
    letterSpacing: 0,
  },
  screen: {
    width: 390,
    height: 844,
    padding: 16,
    contentWidth: 358,   // 390 - 16*2
  },
  size: {
    statusBar: 47,
    appBar: 52,
    tabBar: 58,
    homeIndicator: 34,
    bottomAction: 54,
    icon: 24,
    fab: 48,
    chipHeight: 32,
    rowMenu: 44,
    rowList: 72,
    dividerBlock: 4,
  },
  shadow: {
    fab: { offsetX: 0, offsetY: 4, blur: 12, spread: 0, color: "#000000", opacity: 0.12 },
  },
};

// ===== 헬퍼 =====

// 🔴 fills는 반드시 penpot 형식으로.
// figma 형식 {type:"SOLID", color:{r,g,b}} 를 쓰면 인스턴스에서 오버라이드가 막힌다.
const fill = (hex, opacity = 1) => [{ fillColor: hex, fillOpacity: opacity }];

// stroke도 penpot 형식. 기본 구분선은 1px border.default.
const stroke = (hex = T.color.border.default, width = 1) => [
  { strokeColor: hex, strokeWidth: width, strokeAlignment: "inner", strokeOpacity: 1 },
];

// 🔴 폰트 조회는 완전일치로.
// penpot.fonts.findByName("Inter") 는 부분일치라 "Inter Tight"를 반환한다(② 함정).
const findFont = (name) => penpot.fonts.all.find((f) => f.name === name);

// 텍스트 노드에 타이포 토큰을 한 번에 적용한다.
// 🔴 growType: 고정 폭 텍스트를 "fixed"로 두면 글자가 잘린다 → "auto-height"
const applyText = (node, { size, weight = T.font.weight.regular, color = T.color.text.primary, lineHeight = T.font.lineHeight.normal }) => {
  const f = findFont(T.font.family);
  if (f) {
    node.fontId = f.id;
    node.fontFamily = f.name;
    const v = f.variants.find((x) => String(x.weight) === String(weight));
    if (v) { node.fontVariantId = v.id; node.fontWeight = String(weight); }
  }
  node.fontSize = String(size);
  node.lineHeight = String(lineHeight);
  node.letterSpacing = String(T.font.letterSpacing);
  node.fills = fill(color);
  node.growType = "auto-height";
  return node;
};

// 등락값 → 색 토큰. ③의 StockRow·ChangeBadge가 매 행 호출한다.
const changeColor = (v) =>
  v > 0 ? T.color.state.up : v < 0 ? T.color.state.down : T.color.state.flat;
const changeTint = (v) =>
  v > 0 ? T.color.state.upTint : v < 0 ? T.color.state.downTint : T.color.bg.avatar;
// 부호 표기: 보합은 부호 없이 0.00%
const changeLabel = (v) =>
  (v > 0 ? "+" : v < 0 ? "−" : "") + Math.abs(v).toFixed(2) + "%";

// 🔴 figma 사이징 프로퍼티(primaryAxisSizingMode 등)는 안 먹는다 → penpot 쪽을 쓴다.
const sizing = (node, h = "fix", v = "fix") => {
  node.horizontalSizing = h;
  node.verticalSizing = v;
  return node;
};
```

### B-2. ⑤⑥이 저작 직전 1회만 실행할 검증 스니펫

토큰을 붙여 쓰기 전에 **폰트가 실제로 잡히는지** 확인한다. 조용히 대체되면 에러가 없다(②).

```js
const f = penpot.fonts.all.find((x) => x.name === "Noto Sans KR");
return {
  found: !!f,
  id: f && f.id,
  name: f && f.name,                               // "Noto Sans KR" 정확히 나와야 한다
  has400: !!(f && f.variants.find((v) => String(v.weight) === "400")),
  has700: !!(f && f.variants.find((v) => String(v.weight) === "700")),
  // 함정 확인용 — findByName은 부분일치라 다른 이름이 나올 수 있다
  byNameReturns: penpot.fonts.findByName && penpot.fonts.findByName("Noto Sans KR")?.name,
};
```

`found: false`면 저작을 시작하지 말고 `T.font.family`를 `"Pretendard"`로 바꾼 뒤 다시 검증한다(C절 대체 순위).

---

## C. 대체된 폰트 — ②가 넘긴 미결 판단 2건, 여기서 확정

| 원래 폰트 | 대체 폰트 | 이유 |
|---|---|---|
| **Inter** (제품 폰트, ② 201회) | **`Noto Sans KR`** | ②B절: 기존 파일은 한글을 Inter로 그렸으나 **Inter에는 한글 글리프가 없어 폴백 렌더 중**이다. 즉 기존 파일의 한글은 *이미 Inter가 아니다* — Inter를 유지해도 "기존 톤 유지"가 되지 않는다. ③이 저작할 14화면은 종목명·추천 이유·주문 문구까지 **한글이 절대다수**다. 서버에 `Noto Sans KR`이 400–900 전부 있고(② 가용성 표), 라틴 자소가 Inter와 같은 **네오그로테스크 계열**이라 숫자·퍼센트(`+2.45%`)의 인상이 유지된다. **폴백 렌더를 방치하는 것이 톤을 더 크게 해친다**고 판단했다 |
| **SF Pro Text** (OS 상태바 "9:41", ② 5회) | **`Noto Sans KR`** (제품 폰트로 통일) | ② 가용성 표: **서버에 없다.** `fontId`가 빈 문자열이고 **에러 없이 조용히 대체 렌더링**된다. 제품 타이포가 아니라 OS 자산 5개 노드뿐이므로 별도 폰트를 도입할 이유가 없다. ②가 권고한 "상태바를 재현한다면 통일이 안전하다"를 따르되, Inter가 아니라 **확정된 제품 폰트로 통일**한다. `letterSpacing -0.408`도 함께 버리고 `0`으로 통일한다(제품 텍스트 205개 전수 0) |

**대체 우선순위 (검증 스니펫이 `found: false`를 반환할 때만):**
`Noto Sans KR` → `Pretendard` → `Inter`

> `Pretendard`도 400–900이 서버에 있다(②). 한글 렌더 품질은 대등하며 라틴이 약간 더 좁다.
> `Inter`는 **최후 수단**이다 — 한글이 폴백으로 떨어진다.

### 🔴 ⑤⑥에 전달하는 폰트 함정 (② 기록)

```
penpot.fonts.findByName("Inter")  →  "Inter Tight" 를 반환한다 (부분일치)
```

**반드시 완전일치로 조회한다.** B절 `findFont()`가 이미 이 형태다.

```js
penpot.fonts.all.find(f => f.name === "Noto Sans KR")   // ✅ 완전일치
penpot.fonts.findByName("Noto Sans KR")                  // ❌ 부분일치 — 다른 폰트가 잡힐 수 있다
```

폰트를 잘못 잡아도 **에러가 나지 않는다.** 저작 전 B-2 스니펫으로 `name`이 정확히 일치하는지 눈으로 확인한다.

---

## D. 확인 필요

| 항목 | 왜 판단이 어려웠나 |
|---|---|
| **상승=red / 하락=blue 방향** | 한국 증권 관례를 따랐다(상승 red). 미국식은 정반대(상승 green)다. ①의 PRD 명세에 색 방향을 지정한 문장이 없어 도메인 관례로 결정했다. ⑦이 PRD 원문에 방향 지시가 있는지 재확인하고, 있으면 `T.color.state.up`/`down` 값만 맞바꾸면 된다 — **다른 토큰은 건드릴 필요가 없다** |
| **`state.error`와 `state.up`이 같은 HEX** | 의도적 재사용이다(새 빨강 발명 방지). ③ #13 `OrderFailed`는 주문 시트 위 실패 배너라 등락 표시와 같은 화면에 없다고 판단했다. ⑦이 PNG에서 **한 화면에 실패 배너와 등락 배지가 함께 보이면** 신호가 섞인 것이니 보고할 것 |
| **`size.rowList = 72`를 StockRow 기준으로 쓸지** | ②의 실측 리스트 행은 채팅 72 / 상품 110 / 메뉴 44 세 종류다. ③의 `StockRow`는 종목명+현재가+등락률 2줄 구조라 썸네일이 없는 채팅형(72)에 가깝다고 보고 72로 잡았다. ⑤가 실제로 조립해 보고 2줄이 안 들어가면 `space.xs`(4) 단위로 올린다 — **스케일 밖의 값을 쓰지 말 것** |

---

## E. 다음 단계로의 인계

| 단계 | 이 문서에서 가져갈 것 |
|---|---|
| ⑤ 컴포넌트 | **B절 전체를 저작 코드 맨 위에 복붙.** `fill()`·`stroke()`·`applyText()`·`changeColor()`가 23종 컴포넌트의 공통 기반이다. ②F절 14패턴의 실측 구조 + 이 토큰의 space를 **padding/gap으로** 옮긴다 |
| ⑥ 화면 저작 | **B절 복붙 + A-8 화면 규격.** 하단 고정 액션 Spacer = `657` 계산값. 스크림은 만들지 말고 뒤 보드 `opacity`를 낮춘다 |
| ⑦ 시각 QA | **A-1 경고**(오렌지를 면으로 깔았나) · **A-6 경고**(라운드가 4를 넘나) · **D절 3건** |

### ⑤⑥이 어기면 안 되는 것 (한 줄 요약)

1. `fills`는 **penpot 형식** `{fillColor, fillOpacity}` — figma 형식은 인스턴스 오버라이드가 막힌다
2. 폰트는 **완전일치** 조회 — `findByName`은 부분일치다
3. 오렌지는 **액센트만** — 면으로 깔지 않는다
4. 라운드는 **4 아니면 100** — 8·12·16을 발명하지 않는다
5. weight는 **400 아니면 700** — 500·600을 발명하지 않는다
6. 간격은 **4·8·12·16·32** — 스케일 밖의 값을 쓰지 않는다
7. 절대좌표로 그리지 않는다 — **오토레이아웃**으로 저작한다
