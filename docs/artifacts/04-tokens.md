# 04 — 디자인 토큰

> 입력: `00-env-facts.md`(환경 실측) + `02-design-audit.md`(기존 디자인 실측) + `03-screen-list.md`(만들 화면 14개).
> **Penpot을 호출하지 않았다.** Page 전환 없음. 이 문서는 문서만 만든다.
>
> 도메인: **종합 여행 예약**. 증권·주식 용어는 이 문서에 존재하지 않는다.
> 이전 실행 산출물 `docs/artifacts/_stale-stock-run/` 은 읽지 않았다.

---

## 0. 이 단계의 결론 3줄

1. **다크 테마다.** 배경 `#101012` → 표면 `#17171b` → 2차 표면 `#1f2026`/`#2c2c34` 3단 명도 계단. **그림자 0건.**
2. **폰트는 `Noto Sans KR`로 확정.** 기존 `Spoqa Han Sans Neo`·`SF Pro`는 서버에 없어 **조용히 대체**된다.
3. **여행 도메인 의미색은 기존 팔레트에서 파생했다.** 새 브랜드 색을 발명하지 않았다.

---

## 1. 출처 요약

| 항목 | 개수 | 비고 |
|---|---|---|
| ②에서 그대로 승격 | **31** | 색 13 · 타이포 조합 8 · 간격 6 · 라운드 2 · 규격 2 |
| ③ 요구로 파생 (신규) | **9** | 여행 의미색 6 · 상태 레이어 3 |
| 예외 (승격하지 않음) | **19** | `02` I절 전부 |
| 확인 필요 | **2** | §7 참조 |

---

## A. 색 토큰

### A-1. 표면 / 배경 — ② 그대로 승격

| 토큰 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.bg.base` | `#101012` | ② A-1 빈도 2 (`홈`·`설정` board 자체 fill), ② F절 | **화면 배경.** 신규 board에 반드시 명시 |
| `color.surface.card` | `#17171b` | ② A-1 빈도 **17** (`홈/Frame 5`·`Frame 37`·`Frame 6`·`Frame 31`, 탭바 `Frame 40`, `설정/Frame 64`) | **카드·시트·탭바 표면** |
| `color.surface.raised` | `#1f2026` | ② A-1 빈도 8 (`혜택/Ellipse 1` ×8 아바타 원형 배경) | **표면 위 아바타·플레이스홀더** |
| `color.surface.chip` | `#2c2c34` | ② A-1 빈도 6 (`홈/Frame 10` 칩 ×6) | **칩·보조 버튼 배경** |
| `color.border.hairline` | `#4c4c57` | ② A-2 stroke 0.5 inner ×3 (`홈/Frame 31`, `혜택/Frame 40`, `전체/Frame 40`) | **하단 고정 영역 상단 구분선.** width 0.5 / align inner 고정 |

### A-2. 텍스트 — ② 그대로 승격

② H절: "텍스트 위계가 **색과 굵기**로 표현된다." 4단계 전부 실측값이다.

| 토큰 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.text.primary` | `#ffffff` | ② A-1 빈도 **36** (`홈/자산` 20/700, `혜택/혜택` 24/700, 활성 탭) | 최상위 제목 / 활성 상태 |
| `color.text.strong` | `#e4e4e5` | ② A-1 빈도 15 (`홈/잔액보기` 16/700, `전체/전체` 16/500, `설정/일반` 15) | 강조 텍스트 (본문보다 밝음) · 상단바 타이틀 |
| `color.text.body` | `#c3c3c6` | ② A-1 빈도 **33** (`홈/저금통` 12, `혜택/공동구매 구경하고` 15/500) | **본문 기본** |
| `color.text.secondary` | `#9e9ea3` | ② A-1 빈도 19 (비활성 탭 라벨 10, `설정/화면 테마` 12) | 보조 텍스트 / 비활성 |
| `color.text.link` | `#4880ee` | ② A-1 빈도 11 (`혜택/포인트 받기` 13, `홈/새 내역 9건` 12) | 인라인 액션 링크 |
| `color.icon.default` | `#62626c` | ② A-1 빈도 14 + A-2 stroke 1.8/2 (chevron 16건, 햄버거 8건) | **아이콘 선 기본색 (비활성)** |
| `color.icon.active` | `#ffffff` | ② A-2 stroke 2 center ×4 (`전체/Vector 6·7·8`, `설정/Vector 13`) | 활성 아이콘 선 |

> `#62626b`(4회)는 ② I절 판정대로 **오타**이므로 `#62626c`에 흡수했다. 토큰화하지 않는다.

### A-3. 브랜드 / 기존 의미색 — ② 그대로 승격

| 토큰 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.accent.brand` | `#4880ee` | ② A-1 빈도 **11** · A-3 "유일한 주 액션색" | **주 버튼 배경 · 링크 · 선택 상태.** 유일한 브랜드 색 |
| `color.accent.warning` | `#eda54b` | ② A-1 빈도 4 (`전체/업데이트` 11/500 뱃지 텍스트) | 주의 / 마감 임박 텍스트 |
| `color.accent.warningBg` | `#f4bb73` @ **0.2** | ② A-1 빈도 4 (`전체/Frame 55` 뱃지 배경, 불투명도 0.2 실측) | 주의 뱃지 배경. **fillOpacity 0.2를 반드시 함께 쓴다** |
| `color.accent.success` | `#59bd83` | ② A-2 stroke 3 inner ×1 (`혜택/Ellipse 1` 완료 링) | 성공 / 확정. ② I절이 "유일한 success 근거"로 남긴 값 |

### A-4. 🔴 여행 도메인 의미색 — ③ 요구로 **파생**

② A-3 판정: "**여행 도메인 전용 의미색은 기존 파일에 없다.** ④는 `#4880ee`/`#eda54b`/녹색 계열에서
**파생**시켜야 하며, 무관한 새 브랜드 색을 도입하면 톤앤매너 위반이다."

③이 요구하는 의미는 6종이다. 전부 **기존 3색에 역할을 배정**하는 방식으로 처리했고,
새로 만든 값은 `color.semantic.danger` **1개뿐**이다.

| 토큰 | 값 | 파생 근거 | ③의 어디가 요구하나 |
|---|---|---|---|
| `color.semantic.discount` | `#eda54b` | **② `#eda54b`(앰버, 4회) 재배정.** 새 색 아님 | ③ #1 "다낭 ₩198,000 · **70% 할인**", #8 `DealCard` 할인율 뱃지, E8 근거 |
| `color.semantic.discountBg` | `#f4bb73` @ 0.2 | **② 실측 뱃지 배경 그대로.** 할인율 뱃지 배경 | ③ #8 `DealGrid` 할인율 뱃지 |
| `color.semantic.deadline` | `#d64854` | **파생.** ② A-1 `#d64854`(2회, `전체/Vector 12` 아이콘 내부)를 **역할 승격.** ② A-3이 "danger는 근거 없음 — 앰버와 같은 채도 대역에서 파생하라"고 지시했고, `#d64854`는 HSL S≈63% / L≈56% 로 `#eda54b`(S≈81% / L≈61%)와 **같은 명도 대역**에 있다. 원색 적색(`#ff0000` S100/L50)이 아니다 | ③ #1 "**오늘 자정 마감**", #8 `DeadlineBanner` 카운트다운, #13 `마감` 뱃지 |
| `color.semantic.deadlineBg` | `#d64854` @ **0.2** | **파생.** ② 실측 뱃지 패턴(`#f4bb73@0.2`)의 **불투명도 규칙만 이식**. 색은 위 `deadline` 재사용 | ③ #8 `DeadlineBanner`, #13 마감 뱃지 배경 |
| `color.semantic.lowest` | `#59bd83` | **② `#59bd83`(완료 링) 재배정.** 새 색 아님 | ③ #2 "8/13 ₩209,000(**최저**)", #7 "₩154,000 ✅최저", #9 `즉시 확정` 뱃지 |
| `color.semantic.lowestBg` | `#59bd83` @ **0.2** | **파생.** 위와 동일하게 뱃지 배경 불투명도 규칙 이식 | ③ #2 최저가 날짜 칩, #7 비교 강조 뱃지 |
| `color.semantic.direct` | `#4880ee` | **② `#4880ee` 재배정.** 직항 = 선호/추천 = 브랜드 강조 | ③ #2 `FlightRow` "직항", #5 `직항만` 필터 |
| `color.semantic.stopover` | `#9e9ea3` | **② `#9e9ea3`(보조 텍스트, 19회) 재배정.** 경유 = 중립·부가 정보이므로 유채색을 쓰지 않는다. ② H절 "채도 높은 색을 화면당 1~2개로 제한" 준수 | ③ #2 `LayoverNote` "상하이 푸둥에서 5시간 20분 대기", #4 `LayoverBlock` |
| `color.semantic.priceDown` | `#59bd83` | **`lowest`와 동일 색 재사용.** 가격 하락 = 사용자에게 이득 = 최저가와 같은 의미장 | ③ #1 "후쿠오카 ₩98,000 **▼12,000**", #10 `PriceDelta` |
| `color.semantic.priceUp` | `#d64854` | **`deadline`과 동일 색 재사용.** 가격 상승 = 불리 = 마감과 같은 의미장 | ③ #1 "삿포로 ₩154,000 **▲8,000**", #10 `PriceDelta` |

> **🔴 여기서 만든 새 HEX는 0개다.** `#d64854`조차 ②에서 실측된 값이며, 아이콘 장식용이던 것을
> 의미색으로 **역할만 승격**했다. ② A-3의 "근거 없이 임의 적색을 쓰지 말라"를 만족한다.
>
> **priceDown/priceUp이 국내 증권 관례(적=상승)와 반대인 것은 의도적이다.** 이 제품은 증권 앱이 아니라
> **여행 예약**이고, 여기서 가격 하락은 **좋은 소식**이다(③ #10 "값이 떨어지면 알림"). 초록=이득으로 맞췄다.

### A-5. 스켈레톤 / 비활성

| 토큰 | 값 | 출처 | 역할 |
|---|---|---|---|
| `color.skeleton` | `#2c2c34` | **② `#2c2c34`(칩 배경, 6회) 재배정** | ③ #3 `SkeletonRow` ×6 바 색. 새 회색을 만들지 않고 기존 명도 계단 4단계 값을 쓴다 |

---

## B. 상태 레이어 — 색이 아니라 **불투명도**

②에 눌림·비활성 상태 표현은 **실측되지 않았다**(정적 목업이라 상태 변형이 없다).
③은 버튼·칩·리스트 행·토글·라디오를 다수 요구하므로(#5 필터 칩, #6 라디오, #10 알림 토글)
⑤⑥이 화면마다 즉흥으로 정하면 어긋난다. 따라서 **비율로만** 고정한다.

| 상태 | 불투명도 | 출처 |
|---|---|---|
| hover | **0.08** | ② 실측 없음 → 기본값 |
| focus | **0.12** | ② 실측 없음 → 기본값 |
| pressed | **0.12** | ② 실측 없음 → 기본값 |
| dragged | **0.16** | ② 실측 없음 → 기본값 |
| **선택/뱃지 틴트** | **0.2** | **🔴 ② 실측** (`#f4bb73` fillOpacity **0.2**, `전체/Frame 55` ×4) — 실측이 있으므로 기본값보다 우선 |

**disabled는 넣지 않았다.** ②에 근거 값이 없다. 비활성이 필요하면 `color.text.secondary`(`#9e9ea3`)와
`color.icon.default`(`#62626c`)를 쓴다 — ②에서 비활성 탭 라벨·비활성 아이콘으로 **실측된 방식**이다.

---

## C. 타이포

### C-1. 폰트 — 🔴 `Noto Sans KR` 확정

| 원래 폰트 | 대체 폰트 | 이유 |
|---|---|---|
| `Spoqa Han Sans Neo` (텍스트 90/94) | **`Noto Sans KR`** | `00` 실측: 서버 1,911종 중 **없음**. `findByName` → null. 에러 없이 조용히 대체됨. Noto Sans KR은 weight **100~900 전부** 지원 → 기존 400/500/700 3단계를 손실 없이 재현 |
| `SF Pro` (상태바 `9:41` ×4) | **`Noto Sans KR`** | 서버에 **없음**. OS chrome이라 시각 차이 미미. ② B-2 권고대로 통일 |

**적용 방법 — ⑤⑥은 반드시 이 방식을 쓴다.**

```js
const font = penpot.fonts.findByName("Noto Sans KR");
font.applyToText(textNode, "400");   // variant: "400" | "500" | "700"
```

🔴 **`node.fontFamily = "Noto Sans KR"` 문자열 직접 대입 금지.**
`fontId`가 채워지지 않아 ②가 발견한 무성 대체가 그대로 반복된다.
`applyToText`만이 `fontId`까지 채운다.

### C-2. 타이포 스케일 — ② B절 빈도 상위에서 위계 추출

**lineHeight는 전부 `1.2`, letterSpacing은 전부 `0`.**
(② B-1: 20종 중 19종이 1.2 / 0. 예외는 SF Pro 상태바뿐이며 그것도 Noto로 흡수한다.)

| 토큰 | size / weight | 기본 색 | ② 실측 출처 (빈도) | 역할 |
|---|---|---|---|---|
| `display` | **24 / 700** | `text.primary` | `혜택/혜택` (1) — ② I절이 "유일한 대제목, ④가 Display로 채택 권고" | 화면 최대 제목 |
| `titleL` | **20 / 700** | `text.primary` | `홈/자산`·`홈/소비` (2) | 섹션 카드 제목 |
| `titleM` | **18 / 700** | `text.primary` | `홈/토스뱅크` (1) | 카드 제목 |
| `sectionHeader` | **18 / 500** | `text.primary` | `전체/추천`·`전체/이벤트` (2) | 섹션 헤더 |
| `valueBold` | **16 / 700** | `text.strong` | `홈/잔액보기` ×5+1 (**6**) | 리스트 행 주요값 · **가격 강조** |
| `appBarTitle` | **16 / 500** | `text.strong` | `전체/전체`·`설정/설정`·`혜택/3,820 원` (3) | 상단바 중앙 타이틀 |
| `rowTitle` | **15 / 500** | `text.body` | `혜택/공동구매 구경하고`·`혜택/만보기` (**8**) | 리스트 행 제목 |
| `body` | **15 / 400** | `text.body` | `전체/송금`·`전체/만보기`·`설정/일반` (**16 — 최다**) | **본문 기본** |
| `link` | **13 / 400** | `text.link` | `혜택/결제지원금 받기`·`130원 받기` (**8**) | 인라인 액션 링크 |
| `caption` | **12 / 400** | `text.secondary` | `홈/송금`·`홈/저금통`·`설정/화면 테마` (**13**) | 캡션 / 보조 라벨 |
| `badge` | **11 / 500** | `accent.warning` | `전체/업데이트` ×4 (4) | 뱃지 라벨 |
| `tabLabel` | **10 / 400** | `text.secondary` | 탭바 라벨 ×20 (**15**) | 탭 라벨 (최소 크기) |

**크기 계단: 10 · 11 · 12 · 13 · 15 · 16 · 18 · 20 · 24 — 전부 ② 실측값이다.**
`14`는 ② I절이 프로모 전용 1회 예외로 판정해 제외했다. `17`·`19`·`22` 같은 미등장 값은 만들지 않았다.

> ③이 요구하는 새 크기는 없다. #7 `CompareRow`의 조밀한 표는 `caption`(12)/`body`(15)로,
> #2 `PriceText` 가격은 `valueBold`(16/700)로 전부 커버된다.

---

## D. 간격

### D-1. 🔴 좌우 정렬선 — 이 파일에서 가장 중요한 값

② C-1: **텍스트 좌측 정렬선은 두 가지다.**

| 패턴 | 값 | ② 실측 근거 | ③에서 쓰는 화면 |
|---|---|---|---|
| **풀블리드** (행이 폭 390) | 컨테이너 `left/right = 0`, **행 내부 `leftPadding 22`** | `혜택/Frame 44` left 0, `설정/Frame 64` left 0 → 행 `leftPadding 22` (20+회) | #2 Results, #8 DealCollection, #9 DestinationActivities, #10 Watchlist |
| **카드형** (카드 폭 360) | 화면 여백 **15**, 카드 내부 **22** → 콘텐츠 좌변에서 **37** | `홈/Frame 5`·`Frame 37`·`Frame 32` left 15 right 15 (w 360) → 카드 `leftPadding 22` | #1 Home, #4 FlightDetail, #12 Home-FirstRun |

> **⑥ 경고: 한 화면 안에서 두 패턴을 섞으면 정렬이 즉시 깨진다** (② C-1 결론).
> 화면 단위로 하나를 고른다. 우측은 카드형 `rightPadding 18`(화면 우변에서 33), 풀블리드 `17~23`(→ 22로 수렴).

### D-2. 간격 스케일 — 실측 빈도값 그대로

🔴 **② C-5 판정: 이 파일은 8배수 그리드를 따르지 않는다.**
`7`·`13`·`15`·`17`·`21`·`22`가 `8`·`16`·`24`보다 훨씬 많다. 손으로 그린 파일이다.
**8배수로 재정렬하면 기존 화면과 정렬선이 어긋나 "다른 제품"이 된다.**
따라서 **정규화하지 않고 실측 빈도값을 그대로 토큰화했다.** 산발적 값만 인접 표준값으로 흡수한다.

| 토큰 | 값 | ② 실측 근거 (빈도) | 역할 |
|---|---|---|---|
| `space.xs` | **4** | `홈/Frame 24`~`28` 탭 아이콘↔라벨 rowGap 4, `혜택/Frame 44` rowGap 4 (6) | 최소 간격 |
| `space.sm` | **6** | `홈/Frame 11` ×5, `혜택/Frame 11` ×8 rowGap 6 (**13**) | 행 내부 2줄 간격 |
| `space.md` | **10** | `홈/Frame 10` 칩 내부, `전체/Frame 49` 섹션헤더 columnGap 10 (4+) | 아이콘↔텍스트 (소) |
| `space.lg` | **13** | `설정/Frame 63`·`64`, `전체/Frame 54` columnGap 13 (4+) | 아이콘↔텍스트 (메뉴행) |
| `space.xl` | **15** | `홈/Frame 12` ×5, `혜택/Frame 12` ×8 columnGap 15 (**13**) | **🔴 리스트 행 아이콘↔텍스트 표준** |
| `space.xxl` | **20** | `홈/Frame 17` rowGap 20, `홈/Frame 35` (2) | 리스트 행 간 간격 |
| `space.gutter` | **22** | `leftPadding 22` — 계좌행 ×5, 혜택행 ×8, 설정행 ×11, `홈/Frame 6`, `전체/Frame 49` (**20+ — 최다**) | **좌측 정렬선. 절대 규칙** |
| `space.screenEdge` | **15** | `홈` 전 카드 left/right 15 (w 360) | 카드형 화면 좌우 여백 |
| `space.rowY` | **7** | `홈/Frame 13`~`19` 계좌행 top/bottom 7 (5) | 리스트 행 상하 padding (표준) |
| `space.rowYTight` | **6** | `혜택/Frame 16`~`24` 행 상하 6 (8) | 리스트 행 상하 (대형 아바타행) |
| `space.rowYLoose` | **17** | `설정/Frame 62`~`72` 상하 17 (**11**) | 리스트 행 상하 (2줄+chevron) |
| `space.cardY` | **21** | `홈/Frame 5`·`Frame 6`, `혜택/Frame 5` 상하 21 (3) | 카드 내부 상하 padding |
| `space.cardRight` | **18** | `홈/Frame 5`·`Frame 6`·`Frame 37` 우측 18 (5+) | 카드 우측 padding |
| `space.chipX` | **13** | `홈/Frame 10` 칩 좌우 13 (5) | 칩 좌우 padding |
| `space.chipY` | **8** / **7** | `홈/Frame 10` top 8 / bottom 7 (6) | 칩 상하 padding (비대칭 — 실측 그대로) |
| `space.badgeX` | **7** | `전체/Frame 55` 뱃지 좌우 7 (4) | 뱃지 좌우 padding |
| `space.badgeY` | **4** | `전체/Frame 55` 뱃지 상하 4 (4) | 뱃지 상하 padding |
| `space.tabGap` | **50** | `홈`·`혜택`·`전체` `Frame 29` columnGap 50 (3) | **탭바 전용** 5칸 간격 |
| `space.sectionGap` | **26** | ② C-4 `전체/Frame 57 → Frame 58` gap 26 | 섹션 간 세로 간격 (표준) |
| `space.sectionGapLg` | **33** | ② C-4 `전체/Frame 48 → Frame 57` gap 33 | 상단바 → 첫 섹션 |

**흡수 처리 (정규화한 것 — 원래 값 병기)**

| 실측 원래 값 | 흡수한 토큰 | 근거 |
|---|---|---|
| `21` / `23` (`전체/Frame 51`·`53`·`54` left/right) | `space.gutter` **22** | ② C-2가 "22 근사"로 판정 |
| `26` (`홈/Frame 37` leftPadding, 1회) | `space.gutter` **22** | ② I절 예외 |
| `37` (`홈/Frame 31` left/right, 1회) | `space.gutter` **22** | ② I절 예외 |
| `9` (`홈/Frame 10` 넓은 칩, 1회) | `space.chipX` **13** | ② I절 예외 |
| `11`·`18`·`25`·`204` columnGap (각 1회) | `space.md`/`space.xl` | ② I절 예외 |

### D-3. 세로 리듬 (③이 참고할 값)

② C-4 실측: 홈 카드 간 `12~13`, 혜택 헤더→리스트 `60`, 전체 섹션 간 `26`, 설정 헤더→리스트 `15`.
→ `space.sectionGap` **26** 을 신규 화면의 섹션 간 표준으로 삼는다. `60`은 `혜택` 1회 예외라 승격하지 않았다.

---

## E. 라운드

② D절: **"카드는 20, 칩은 6. 그 사이 값은 존재하지 않는다."** ② H절: "이 **20 vs 6의 대비**가 이 제품의 형태 시그니처다."

| 토큰 | 값 | ② 실측 근거 (빈도) | 역할 |
|---|---|---|---|
| `radius.card` | **20** | `홈/Frame 5`(360×66), `Frame 37`(360×81), `Frame 6`, `Frame 31`, `혜택/Frame 5`, `혜택/Frame 40`, `전체/Frame 55`(뱃지) (**11**) | **카드 · 시트 · 탭바 · 뱃지** |
| `radius.chip` | **6** | `홈/Frame 10` 47×30 ×5 + 75×30 ×1 (**6**) | **칩 · 소형 버튼** |
| `radius.full` | **999** | 파생 — ② D절 "원형 요소는 `ellipse` 타입" | 원형 아바타를 rect로 만들 때만. **가능하면 `ellipse` 도형을 쓴다** |

**`radius.10`은 만들지 않았다** (② I절: `혜택/Frame 45` 1회 예외).
**8·12·16 같은 중간값을 도입하지 않는다** (② J절 금지 항목).

---

## F. 규격 · 높이

| 토큰 | 값 | ② 실측 근거 |
|---|---|---|
| `size.screenW` | **390** | 4개 board 전부. **PRD 7절 제약 — 조정 불가** |
| `size.screenH` | **844** | 4개 board 전부 (기존). 신규는 ③이 화면별로 지정(1100~1680) |
| `size.cardW` | **360** | `홈` 전 카드 (= 390 − 15×2) |
| `size.statusBarH` | **36** | `Status Bar - iPhone` ×4 |
| `size.appBarH` | **60** | `전체/Frame 48`. (51/66 이형 존재 → 60으로 수렴) |
| `size.tabBarH` | **80** | `혜택`·`전체` `Frame 40` (77/80 → 80). 내부 `Frame 29`는 **360×56, x 15** |
| `size.tabBarInnerH` | **56** | `Frame 29` 고정 |
| `size.homeIndicatorW/H` | **144 / 5**, top **831** | `Rectangle 1` ×4, 좌우 각 123 |
| `size.rowH` | **55** | `홈/Frame 13`~`19` ×5 — **주 리스트 행 표준** |
| `size.rowHLarge` | **69** | `혜택/Frame 16`~`24` ×8 — 대형 아바타 행 |
| `size.rowHStacked` | **74** | `설정/Frame 62`~`72` ×11 — 2줄 + chevron |
| `size.rowHMenu` | **54** | `전체/Frame 51`·`53`·`54` — 아이콘 + 1줄 |
| `size.chipH` | **30** | `홈/Frame 10` 47×30 |
| `size.badgeH` | **22** | `전체/Frame 55` 53×22 |
| `size.cardH` | **66** | `홈/Frame 5`·`Frame 6`, `혜택/Frame 5` |
| `size.avatarSm` | **38** | `홈/Frame 9/Ellipse 1` |
| `size.avatarLg` | **57** | `혜택/Frame 9/Ellipse 1` |
| `size.iconXs` | **16** | chevron board |
| `size.iconSm` | **20** | 탭 아이콘 |
| `size.iconMd` | **24** | 상단바 아이콘 |
| `stroke.icon` | **1.8** | chevron ×16 (`#62626c`, align center) |
| `stroke.iconBold` | **2** | 햄버거 ×8, 활성 아이콘 ×4 |
| `stroke.hairline` | **0.5** | `#4c4c57`, align **inner** ×3 |

**🔴 그림자는 없다.** ② E절: 453개 노드 전체에서 **0건**.
깊이는 오직 명도 계단(`#101012` → `#17171b` → `#1f2026`/`#2c2c34`)으로만 만든다.
⑤⑥은 어떤 그림자도 도입하면 안 된다.

**🔴 divider 도형도 없다.** 리스트 행 사이는 선이 아니라 **여백(gap)** 으로 나눈다.
예외는 하단 고정 영역 상단의 hairline(`#4c4c57` / 0.5 / inner) 3건뿐.

---

## G. 🔴 저작용 JS 상수 — ⑤⑥은 코드 맨 위에 이것을 그대로 붙인다

> **왜 JS 상수인가:** `figma.variables.*`는 성공 응답만 오고 토큰이 거의 남지 않는다
> (AGENTS.md 실측 경고). Penpot 변수 기능에 의존하지 않는다. 점수는 변수가 아니라
> **컴포넌트 재사용**으로 받는다.

```js
// ============================================================
// T — 디자인 토큰 (04-tokens.md). 값 수정 금지. 출처: 02-design-audit.md 실측
// ⑤⑥ 저작 스크립트 맨 위에 그대로 복붙한다.
// ============================================================
const T = {
  color: {
    bg:      { base: "#101012" },
    surface: {
      card:  "#17171b",   // 카드·시트·탭바
      raised:"#1f2026",   // 아바타·플레이스홀더
      chip:  "#2c2c34",   // 칩·보조버튼·스켈레톤
    },
    border:  { hairline: "#4c4c57" },  // width 0.5 / align "inner"
    text: {
      primary:   "#ffffff",  // 최상위 제목·활성
      strong:    "#e4e4e5",  // 강조·상단바 타이틀
      body:      "#c3c3c6",  // 본문 기본
      secondary: "#9e9ea3",  // 보조·비활성
      link:      "#4880ee",  // 인라인 액션
    },
    icon: { default: "#62626c", active: "#ffffff" },
    accent: {
      brand:     "#4880ee",  // 유일한 브랜드 색
      warning:   "#eda54b",
      warningBg: "#f4bb73",  // + opacity 0.2
      success:   "#59bd83",
    },
    // 여행 도메인 의미색 — 전부 위 팔레트 재배정. 새 HEX 0개.
    semantic: {
      discount:   "#eda54b",  // 70% 할인
      discountBg: "#f4bb73",  // + 0.2
      deadline:   "#d64854",  // 오늘 자정 마감
      deadlineBg: "#d64854",  // + 0.2
      lowest:     "#59bd83",  // 최저가·즉시확정
      lowestBg:   "#59bd83",  // + 0.2
      direct:     "#4880ee",  // 직항
      stopover:   "#9e9ea3",  // 경유(중립)
      priceDown:  "#59bd83",  // 값 하락 = 이득
      priceUp:    "#d64854",  // 값 상승 = 불리
    },
    skeleton: "#2c2c34",
  },

  font: {
    family: "Noto Sans KR",           // 서버 가용성 확인 완료 (weight 100~900)
    weight: { regular: "400", medium: "500", bold: "700" },
    lineHeight: 1.2,                  // 전 텍스트 단일값
    letterSpacing: 0,                 // 전 텍스트 단일값
    size: {
      display: 24, titleL: 20, titleM: 18, sectionHeader: 18,
      valueBold: 16, appBarTitle: 16, rowTitle: 15, body: 15,
      link: 13, caption: 12, badge: 11, tabLabel: 10,
    },
  },

  space: {
    xs: 4, sm: 6, md: 10, lg: 13, xl: 15, xxl: 20,
    gutter: 22,        // 🔴 좌측 정렬선. 절대 규칙
    screenEdge: 15,    // 카드형 화면 좌우 여백 (카드 폭 360)
    rowY: 7, rowYTight: 6, rowYLoose: 17,
    cardY: 21, cardRight: 18,
    chipX: 13, chipYTop: 8, chipYBottom: 7,
    badgeX: 7, badgeY: 4,
    tabGap: 50,
    sectionGap: 26, sectionGapLg: 33,
  },

  radius: { card: 20, chip: 6, full: 999 },

  size: {
    screenW: 390, screenH: 844, cardW: 360,
    statusBarH: 36, appBarH: 60, tabBarH: 80, tabBarInnerH: 56,
    homeIndicatorW: 144, homeIndicatorH: 5, homeIndicatorTop: 831,
    rowH: 55, rowHLarge: 69, rowHStacked: 74, rowHMenu: 54,
    chipH: 30, badgeH: 22, cardH: 66,
    avatarSm: 38, avatarLg: 57,
    iconXs: 16, iconSm: 20, iconMd: 24,
  },

  stroke: { icon: 1.8, iconBold: 2, hairline: 0.5 },

  // 상태는 색이 아니라 비율. 어떤 브랜드 색 위에도 그대로 얹힌다.
  // tint 0.2 만 ② 실측값(#f4bb73 fillOpacity 0.2). 나머지는 기본값.
  state: { hover: 0.08, focus: 0.12, pressed: 0.12, dragged: 0.16, tint: 0.2 },

  // 그림자 없음(② 453노드 0건). divider 도형 없음. 깊이는 명도 계단으로만.
  shadow: null,
};

// ============================================================
// 헬퍼
// ============================================================

// 🔴 fills는 반드시 penpot 형식으로.
// figma 형식 {type:"SOLID", color:{r,g,b}} 은 인스턴스에서 오버라이드가 막힌다.
const fill = (hex, opacity = 1) => [{ fillColor: hex, fillOpacity: opacity }];

// 뱃지·선택 배경 틴트 (② 실측 0.2)
const tint = (hex) => fill(hex, T.state.tint);

// 상태 레이어: 바탕색은 그대로 두고 불투명도만 바꿔 얹는다.
// 새 색을 만들지 않으므로 브랜드 색이 바뀌어도 그대로 성립한다.
const stateFill = (hex, state) => fill(hex, T.state[state]);

// stroke도 penpot 형식
const strokeOf = (hex, width, align = "center") =>
  [{ strokeColor: hex, strokeWidth: width, strokeAlignment: align, strokeOpacity: 1 }];

const hairline = () => strokeOf(T.color.border.hairline, T.stroke.hairline, "inner");

// 🔴 폰트는 반드시 applyToText로. fontFamily 문자열 대입은 무성 대체된다.
const NOTO = penpot.fonts.findByName(T.font.family);
const applyFont = (node, sizeKey, weightKey = "regular") => {
  NOTO.applyToText(node, T.font.weight[weightKey]);
  node.fontSize      = String(T.font.size[sizeKey]);
  node.lineHeight    = String(T.font.lineHeight);
  node.letterSpacing = String(T.font.letterSpacing);
};

// 타이포 역할 프리셋 — 크기·굵기·색을 한 번에
const TYPE = {
  display:       { size: "display",       weight: "bold",    color: T.color.text.primary },
  titleL:        { size: "titleL",        weight: "bold",    color: T.color.text.primary },
  titleM:        { size: "titleM",        weight: "bold",    color: T.color.text.primary },
  sectionHeader: { size: "sectionHeader", weight: "medium",  color: T.color.text.primary },
  valueBold:     { size: "valueBold",     weight: "bold",    color: T.color.text.strong },
  appBarTitle:   { size: "appBarTitle",   weight: "medium",  color: T.color.text.strong },
  rowTitle:      { size: "rowTitle",      weight: "medium",  color: T.color.text.body },
  body:          { size: "body",          weight: "regular", color: T.color.text.body },
  link:          { size: "link",          weight: "regular", color: T.color.text.link },
  caption:       { size: "caption",       weight: "regular", color: T.color.text.secondary },
  badge:         { size: "badge",         weight: "medium",  color: T.color.accent.warning },
  tabLabel:      { size: "tabLabel",      weight: "regular", color: T.color.text.secondary },
};

// 텍스트 한 방에 만들기 — 역할명 + 문구 + 색 오버라이드(선택)
const text = (content, role, colorOverride) => {
  const t = penpot.createText(content);
  const p = TYPE[role];
  applyFont(t, p.size, p.weight);
  t.fills    = fill(colorOverride || p.color);
  t.growType = "auto-height";   // 🔴 fixed면 글자가 잘린다 (AGENTS.md 함정)
  return t;
};
```

### G-1. ⑤⑥에게 주는 사용 규칙

| 규칙 | 이유 |
|---|---|
| `fill()` 헬퍼만 쓴다. `{type:"SOLID", color:{r,g,b}}` 금지 | figma 형식 fills는 **인스턴스에서 오버라이드가 막힌다** |
| `applyFont()` / `text()` 만 쓴다. `node.fontFamily = "..."` 금지 | `fontId`가 안 채워져 **무성 대체**된다 (② B-2 실증) |
| 모든 텍스트 `growType = "auto-height"` | 고정폭 텍스트가 `fixed`면 잘린다 (AGENTS.md) |
| board 배경에 `fill(T.color.bg.base)` 명시 | 기존 `혜택`·`전체` board는 fill 미지정(투명) — 신규는 반드시 명시 (② F절) |
| `T.shadow`는 `null`이다. 그림자 코드를 쓰지 않는다 | 453노드 실측 0건 |
| 한 화면 안에서 `gutter 22`(풀블리드)와 `screenEdge 15 + 22`(카드형) 혼용 금지 | 정렬선이 즉시 깨진다 (② C-1) |
| 유채색은 **화면당 1~2개**로 제한 | ② H절 실측 규칙 |
| `horizontalSizing = "fix" \| "auto"` (penpot) 사용 | `primaryAxisSizingMode` 등 figma 사이징 프로퍼티는 안 먹는다 |

---

## H. 대체된 폰트

| 원래 폰트 | 대체 폰트 | 이유 |
|---|---|---|
| `Spoqa Han Sans Neo` | **`Noto Sans KR`** | 서버 1,911종에 없음(`findByName` → null). 400/500/700 전부 지원하는 한글 고딕 산세리프라 톤앤매너 유지 |
| `SF Pro` (상태바 `9:41`) | **`Noto Sans KR`** | 서버에 없음. OS chrome이라 시각 차이 미미. ② B-2 권고 |

⚠️ Noto Sans KR은 Spoqa보다 **글자폭이 약간 넓다.** 모든 텍스트를 `growType = "auto-height"`로 두어
잘림을 방지한다. 화면 완성 후 `growType === "auto-height"` 텍스트를 전부 `resize`로 재계산시킨다(AGENTS.md).

---

## I. 승격하지 않은 값 (② I절 준수)

| 값 | 왜 제외 |
|---|---|
| `#62626b` (4회) | `#62626c`의 1자 오타 → 흡수 |
| `#f9de86`·`#f4b64f`·`#f8df00`·`#dee9fd`·`#357a6c`·`#477eea`·`#64c790`·`#323237` (각 1) | 은행 브랜드 아바타 색. **금융 도메인 전용, 여행에 인계 불가** |
| `#f2be41` (2) | 아이콘 내부 장식 path. 의미색 아님 |
| `#d9d9d9` (4) | iOS 홈 인디케이터. OS chrome (단 `size.homeIndicator*`는 규격으로 승격) |
| `borderRadius 10` (1) | 20/6 체계에 없음 |
| `borderRadius 4.3 / 2.5` (각 4) | 배터리 아이콘. OS chrome |
| `letterSpacing 0.6 / 0.75 / -0.48 / -0.21 / mixed` | 90%가 0. 산발적 미세조정 |
| `lineHeight 1.294` (4) | SF Pro 상태바 전용 → Noto로 통일하며 1.2로 흡수 |
| `columnGap 204` (1) | space-between 대신 박은 고정값 |
| `padding 26 / 37 / 9` (각 1) | 22 / 18 / 13 체계 이탈 → 흡수 |
| `fontSize 14` (1) | 프로모 전용 1회. 위계에 자리 없음 |
| `fontWeight mixed` (2) | 토큰이 아니라 ⑥의 `getRange` 기법 |
| `gap 60` (1) | `혜택` 헤더→리스트 1회. `sectionGap 26`으로 수렴 |

---

## J. 확인 필요 (⑦ 시각 QA에서 검토)

| 항목 | 왜 판단이 어려웠나 | 잠정 처리 |
|---|---|---|
| `color.semantic.deadline` = `#d64854` 의 **가독성** | ② 실측에서 `#d64854`는 **아이콘 내부 path 색**으로만 2회 쓰였고 **텍스트로 쓰인 적이 없다.** `#101012` 배경 위 12px 텍스트에서 대비가 충분한지 실측 근거가 없다 | 일단 채택. ⑦이 PNG에서 마감 뱃지 문구가 읽히는지 확인하고, 안 읽히면 `#eda54b`(앰버, 텍스트 실측 있음)로 폴백 |
| `size.appBarH` = **60** | ② F절 실측이 화면마다 다르다 — `51`(홈) / `60`(전체) / `66`(혜택). 단일값 근거가 없다 | 빈도·중앙값 기준 `60` 채택. ③ #1·#2·#4의 헤더가 콘텐츠를 담지 못하면 ⑥이 화면별로 늘려도 된다 (폭 390만 불변) |

---

## K. ③ 14개 화면 대비 커버리지 점검

③이 요구하는 시각 요소가 이 토큰만으로 전부 표현되는지 확인했다.

| ③의 요구 | 커버 토큰 | 부족? |
|---|---|---|
| #1 `FlightSearchCard` 전체폭 버튼 | `accent.brand` + `radius.chip 6` + `valueBold` | 없음 |
| #1 `TripCountdownCard` D-9 | `accent.brand` + `titleL` | 없음 |
| #1/#8 할인율 `70%` 뱃지 | `semantic.discount` + `discountBg@0.2` + `badge 11/500` + `radius.card 20`(뱃지 실측 r20) | 없음 |
| #1/#8 `오늘 자정 마감` | `semantic.deadline` + `deadlineBg@0.2` | ⚠️ J절 |
| #1/#10 `▼12,000` / `▲8,000` | `semantic.priceDown` / `priceUp` | 없음 |
| #2 `직항` / `1회 경유` | `semantic.direct` / `semantic.stopover` | 없음 |
| #2 날짜칩 최저가 강조 | `semantic.lowest` + `lowestBg@0.2` + `radius.chip 6` | 없음 |
| #2 가격 텍스트 | `valueBold 16/700` + `text.strong` | 없음 |
| #3 `SkeletonRow` ×6 | `color.skeleton` + `radius.chip 6` | 없음 |
| #5/#6 시트 | `surface.card` + `radius.card 20` + `state.tint 0.2`(선택 칩) | 없음 |
| #6 라디오 선택 상태 | `accent.brand` + `state.pressed/focus 0.12` | 없음 |
| #7 비교 강조 뱃지 | `semantic.lowest` + `badge` | 없음 |
| #9 별점 `★4.8` | `accent.warning #eda54b` (앰버 = 별점 관례) | 없음 |
| #9 `즉시 확정` 뱃지 | `semantic.lowest` + `lowestBg@0.2` | 없음 |
| #11/#12/#14 `EmptyState` | `text.secondary` + `icon.default` + `surface.raised` | 없음 |
| #13 `SoldOutDialog` | `surface.card` + `radius.card 20` + `semantic.deadline`(마감 뱃지) + 뒤 board `opacity 0.35` | 없음 |
| 전 화면 탭바 | `surface.card` + `radius.card 20` + `hairline` + `tabLabel 10` + `size.tabBarH 80` | 없음 |

**부족한 토큰 없음.** ③의 14개 화면은 위 상수만으로 저작 가능하다.

---

## L. ⑤로의 인계 한 줄 요약

> `T` 상수와 `fill()`·`applyFont()`·`text()`·`hairline()` 헬퍼를 **코드 맨 위에 복붙**하고,
> 원시 HEX·숫자를 컴포넌트 코드에 직접 쓰지 마라. 값이 필요하면 반드시 `T.*`를 통한다.
> 다크 배경 · 라운드 20 카드 · 좌측 22 정렬선 · 그림자 0 — 이 넷이 톤앤매너의 전부다.
