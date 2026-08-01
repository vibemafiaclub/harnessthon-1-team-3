# 06 — 화면 저작 결과

> 입력: `00-env-facts.md` · `02-design-audit.md` · `03-screen-list.md` · `04-tokens.md` · `05-components.md`
> 저작 Page: **`3-toss-result`** (`3-toss` 는 이 단계에서 **열지도 쓰지도 않았다**)
> 도메인: **종합 여행 예약**. 증권·금융 용어 없음.
>
> **③이 요구한 14개 화면을 전부 저작했다. 미저작 0건.**

---

## 0. 이 단계의 결론 4줄

1. **화면 14개를 전부 저작했다.** 폭 390 고정, 최상위 이름 `New/` 접두 전부 준수.
2. **컴포넌트 인스턴스 366개**로 조립했다(⑤의 32개 중 **30개 사용**). 복붙이 아니다.
3. **`export_shape` PNG 검증을 20회 이상 실제로 수행**했다. ⑤ 보고(§9 "서비스 장애")는 **틀렸다** — 오케스트레이터 정정이 맞았다.
4. **마무리 감사 6항목 전부 이슈 0건** (잘림·무성폰트·토큰이탈·그림자·growType·무의미이름).

---

## 1. 저작 정보

| 항목 | 값 |
|---|---|
| 작업 Page | **`3-toss-result`** |
| Page id | `cf8cfb09-3416-4c32-a2eb-38e95e5c2be9` |
| 저작 화면 수 | **14 / 14** |
| 컴포넌트 인스턴스 총계 | **366** (`TR /` 직접 347 + 리네임 뱃지 19) |
| 사용 컴포넌트 | **30 / 32** |
| 배치 영역 | **y ≥ 0** (컴포넌트 선반 `y ≤ -635` 는 **건드리지 않음** — 32개 전부 `mainInstance()` 생존 확인) |
| 폭 390 준수 | **14/14 전부** |

**Page 게이트 준수**: 모든 저작 호출 첫 줄에서 `getPageById` 로 Page 를 재고정하고
`name !== "3-toss-result"` 이면 즉시 throw 했다. `openPage` 는 **별도 호출**로 먼저 수행했다.

---

## 2. 저작한 화면 14개

| # | 프레임 이름 | 등급 | id | 좌표 | 최종 크기 | PNG | 상태 |
|---|---|---|---|---|---|---|---|
| 1 | `New/Home` | **P0** | `b04b167a…6a5dd50cb32b` | 0, 0 | 390 × **1754** | ✅ 5회 | 완료 |
| 2 | `New/Results` | **P0** | `b04b167a…6a5f00dd8c6d` | 490, 0 | 390 × **1560** | ✅ 3회 | 완료 |
| 3 | `New/Results-Loading` | P2 | `b04b167a…6a626350d375` | 2940, 0 | 390 × **1560** | ✅ | 완료 |
| 4 | `New/FlightDetail` | P1 | `b04b167a…6a607ad174b2` | 980, 1900 | 390 × **1480** | ✅ | 완료 |
| 5 | `New/Results-FilterSheet` | P1 | `b04b167a…6a5fc6d8179c` | 1470, 0 | 390 × **1560** | ✅ 2회 | 완료 |
| 6 | `New/Results-FareSheet` | P1 | `b04b167a…6a5f73974723` | 980, 0 | 390 × **1560** | ✅ 2회 | 완료 |
| 7 | `New/Compare` | P1 | `b04b167a…6a6022540327` | 0, 1900 | 390 × **1180** | ✅ 2회 | 완료 |
| 8 | `New/DealCollection` | P1 | `b04b167a…6a61350cc2d5` | 490, 3500 | 390 × **1495** | ✅ | 완료 |
| 9 | `New/DestinationActivities` | P1 | `b04b167a…6a618eecac6f` | 980, 3500 | 390 × **1360** | ✅ | 완료 |
| 10 | `New/Watchlist` | P1 | `b04b167a…6a60de69af01` | 0, 3500 | 390 × **1240** | ✅ 2회 | 완료 |
| 11 | `New/Results-Empty` | P2 | `b04b167a…6a61de67e1fb` | 1960, 0 | 390 × **1100** | ✅ | 완료 |
| 12 | `New/Home-FirstRun` | P2 | `b04b167a…6a62086569bf` | 2450, 0 | 390 × **1689** | ✅ | 완료 |
| 13 | `New/Watchlist-SoldOut` | P2 | `b04b167a…6a62d97614f2` | 1470, 3500 | 390 × **1240** | ✅ 2회 | 완료 |
| 14 | `New/Compare-Empty` | P2 | `b04b167a…6a6294130e8c` | 490, 1900 | 390 × **900** | ✅ 2회 | 완료 |

> Penpot 은 `New/Home` 을 **`path="New"` + `name="Home"`** 으로 쪼개 저장한다(컴포넌트와 동일 규칙).
> UI 표기는 `New / Home` 이며 `New/` 접두 요건을 만족한다.

**저작 순서**: ③ 6절을 그대로 따랐다. **P0 2개를 PNG로 검증한 뒤에만 P1로 내려갔다.**
clone 기반 화면은 전부 원본 완성 후에 만들었다.

---

## 3. 화면별 컴포넌트 인스턴스 사용 내역 (복붙이 아님을 증명하는 근거)

| 화면 | `TR /` 인스턴스 수 | 주요 사용 컴포넌트 |
|---|---|---|
| `New/Home` | **20** + 뱃지 5 | StatusBar, SectionHeader×3, ActivityCard×3, DealCard×4, WatchRow×3, Chip×4, TabBar, HomeIndicator, Button/Primary, Badge×4 |
| `New/Results` | **32** | StatusBar, TopBar, PriceDayCell×7(3변형), Chip×5, FlightRow/Direct×9, FlightRow/Stopover×3, StopoverBar×3, CompareTray, HomeIndicator |
| `New/Results-Loading` | **38** | base 상속 + SkeletonRow×6 |
| `New/Results-Empty` | **37** | base 상속 + EmptyState, SuggestionRow×3, Button/Secondary |
| `New/Results-FilterSheet` | **45** | base 상속 + Chip×7, InfoRow×5, Button/Primary |
| `New/Results-FareSheet` | **36** | base 상속 + FareOption×3, Button/Primary |
| `New/Compare` | **15** | StatusBar, TopBar, CompareRow×7, FlightRow/Direct×3, SectionHeader, Button/Primary, HomeIndicator |
| `New/Compare-Empty` | **23** | base 상속 + EmptyState, InfoRow×5, Button/Primary, SectionHeader |
| `New/FlightDetail` | **14** | StatusBar, TopBar, SectionHeader×3, InfoRow×5, ActivityCard×2, Button/Primary, HomeIndicator |
| `New/Watchlist` | **13** | StatusBar, TopBar, Chip×2, WatchRow×3, SectionHeader×2, FlightRow/Direct×2, TabBar, HomeIndicator |
| `New/Watchlist-SoldOut` | **17** | base 상속 + InfoRow×2, Button/Primary, Button/Secondary |
| `New/DealCollection` | **20** + 뱃지 8 | StatusBar, TopBar, Chip×4, DealCard×8, ActivityCard×3, SectionHeader, TabBar, HomeIndicator, Badge×8 |
| `New/DestinationActivities` | **14** + 뱃지 3 | StatusBar, Chip×5, ActivityCard×6, TabBar, HomeIndicator, Badge/Instant×3 |

### 3-1. 컴포넌트별 재사용 횟수 (전 화면 합계)

| 컴포넌트 | 인스턴스 수 | | 컴포넌트 | 인스턴스 수 |
|---|---|---|---|---|
| `FlightRow/Direct` | **50** | | `Card/ActivityCard` | **17** |
| `Chip/Default` | **40** | | `Common/InfoRow` | **17** |
| `PriceDayCell/Default` | **25** | | `Card/DealCard` | **16** |
| `FlightRow/Stopover` | **20** | | `DealBadge`(Discount/Deadline) | **16** |
| `Flight/StopoverBar` | **20** | | `Shell/StatusBar` | **14** |
| `Section/SectionHeader` | **17** | | `Shell/HomeIndicator` | **14** |
| `Compare/CompareRow` | **14** | | `Chip/Selected` | **13** |
| `Watch/WatchRow` | **12** | | `Shell/TopBar` | **11** |
| `Button/Primary` | **7** | | `Shell/TabBar` | **6** |
| `State/SkeletonRow` | **6** | | `PriceDayCell/Selected` · `Lowest` | **5** · **5** |
| `Compare/CompareTray` | **5** | | `State/EmptyState` | **4** |
| `Button/Secondary` | **3** | | `Fare/FareOption` | **3** |
| `State/SuggestionRow` | **3** | | `Badge/Instant` | **3** |
| `NotifyBadge`(Badge 재색) | **2** | | | |

**검증**: `DealBadge`·`InstantBadge`·`NotifyBadge` 는 이름만 의미기반으로 바꾼 것이고
`isComponentInstance() === true` / `componentRefShape` 존재를 **실측 확인**했다. 진짜 인스턴스다.

### 3-2. 미사용 컴포넌트 2개 (정직하게)

| 컴포넌트 | 왜 안 썼나 |
|---|---|
| `TR / Badge / Lowest` | 최저가 강조를 **`PriceDayCell/Lowest` 변형**과 `CompareRow` 값 **색 오버라이드**(`semantic.lowest`)로 처리했다. 뱃지를 덧붙이면 ② H절 "유채색 화면당 1~2개" 규칙을 넘긴다 |
| `TR / Badge / Direct` | 직항 표기를 `FlightRow` 내장 `Meta`("2시간 25분 · 직항", `semantic.direct` 색)로 처리했다. 행마다 뱃지를 얹으면 6~12개가 반복돼 밀도가 무너진다 |

`PriceDelta/Down`·`Up` 도 독립 인스턴스로는 안 썼다 — **`WatchRow` 내장 `Delta`** 에
`characters` + `fills`(priceDown/priceUp) 오버라이드로 같은 결과를 냈다(⑤ §6-2가 `Delta` 를 자식으로 노출).

---

## 4. PNG 확인 결과와 실제로 고친 것

**`export_shape` 는 정상 동작했다.** 화면 board·인스턴스 모두 성공. 20회 이상 뽑아 육안 판독했다.

| # | 화면 | PNG에서 발견한 문제 | 어떻게 고쳤나 |
|---|---|---|---|
| 1 | Home | 카드 내부 행이 320 고정이라 버튼(360)과 어긋남 | 자식 전부 `layoutChild.horizontalSizing = "fill"` |
| 2 | Home | **DealCard 뱃지가 안 보임** | `appendChild` 가 인스턴스에 안 붙고 화면 루트로 감 → 좌표 계산 후 **children 배열 끝으로 재삽입**(z-order) |
| 3 | Home | 뱃지 틴트(0.2)가 **사진 위에서 사라짐** | 스크림 금지 원칙대로 **불투명 `surface.card` 배경 + 의미색 텍스트**로 교체(새 색 도입 0) |
| 4 | Home | ActivityCard·DealCard·WatchRow 사진이 빈 사각형 | `penpot.uploadMediaUrl` 로 실제 사진 **18장** 조달·주입 |
| 5 | Results | Spacer 계산이 레이아웃 확정 전이라 1601 (목표 1560) | 확정 후 **차분만큼 재계산** → 정확히 1560 |
| 6 | Results | 항공편 6건 뒤 **699px 빈 공백** | "52건" 대비 부실 → 항공편 **6건 추가**(총 12건) |
| 7 | FareSheet | `SheetFooter` 버튼/가격 **좌우 뒤바뀜** | `flex.dir = "row-reverse"` |
| 8 | FareSheet | 라디오가 전부 미선택 | 첫 운임 `Radio` 를 `accent.brand` 로 채움 |
| 9 | FilterSheet | `InfoRow`(390)가 그룹(346)을 넘어 **"✓ 선택됨" 잘림** | `horizontalSizing="fill"` + 내장 좌우 padding 0 (이중 들여쓰기 제거) |
| 10 | Compare | **ValueB 열이 통째로 초록** (컴포넌트 기본색) | ③ #7 표대로 **더 나은 값만** `semantic.lowest`, 나머지 `text.strong` |
| 11 | Compare | 하단 437px 빈 공백 | "이 조건의 다른 항공편" 3건 추가 |
| 12 | FlightDetail | 하단 바 좌우 뒤바뀜 | `flex.dir = "row"` |
| 13 | Watchlist | **홈 탭이 활성**으로 표시 | `setActiveTab()` 헬퍼로 5탭 라벨·아이콘 색 일괄 제어 → 담아둠 활성 |
| 14 | Watchlist | 후쿠오카 Delta 2줄 줄바꿈 | 문구 축약 (`▼ 12,000`) |
| 15 | DealCollection | 코타키나발루 사진 로드 실패 | 다른 URL로 재조달 |
| 16 | DestActivities | 스이카 교통패스 사진이 **개 사진** | 다른 URL로 재조달 |
| 17 | Compare-Empty | HowTo 라벨(160 고정폭) **2줄 줄바꿈** | 라벨 280 / 값 46 으로 `resize` + `growType` 복원 |
| 18 | Compare-Empty | 빈 상태인데 "선택한 항공편 예약" 버튼 | 하단 바 `hidden` |
| 19 | SoldOut | 대화상자 버튼 좌우 뒤바뀜 | `flex.dir = "row-reverse"` |
| 20 | Home-FirstRun | 헤더가 "담아둔 목적지 **3**" | "담아둔 목적지" + MoreLink 숨김 |

---

## 5. 오버레이 3종 — ③ C-3 준수 확인

**스크림 사각형을 단 하나도 쓰지 않았다.** 전부 **뒤 콘텐츠 보드의 `opacity` 0.35** 방식.

| 화면 | base | 방식 | ⑦ 통과 조건 (뒤 콘텐츠가 보이는가) |
|---|---|---|---|
| `New/Results-FareSheet` | `New/Results` clone | 최상위 자식 11개 `opacity = 0.35` + 시트(685) 하단 정렬 | **✅ PNG에서 항공편 목록 12행이 시트 위로 흐릿하게 보임** |
| `New/Results-FilterSheet` | `New/Results` clone | 동일 + 시트(594) 하단 정렬 | **✅ 목록·날짜칩·필터칩 전부 비쳐 보임** |
| `New/Watchlist-SoldOut` | `New/Watchlist` clone | 자식 12개 `opacity = 0.35` + 모달(330×326) 중앙 | **✅ 배너·WatchRow 3행·탭바가 모달 좌우/상하로 보임** |

시트·모달 위치는 **전부 계산해 명시**했다 (`y = frame.y + frame.height − sheet.height`,
모달은 중앙). `layoutGrow` Spacer 함정을 피하려고 **고정 높이 Spacer**만 썼다.

---

## 6. 마무리 패스 (전부 실측 확인)

| 항목 | 처리 | 결과 |
|---|---|---|
| `auto-height` 텍스트 재계산 | 14화면 전체 순회, `resize` 후 `growType` 즉시 복원 | **831개 재계산 / 831개 복원** |
| 텍스트 잘림·붕괴 (`w≤1` or `h≤1`) | 전 노드 감사 | **0건** |
| `growType === "fixed"` 잔존 | 전 노드 감사 | **0건** |
| 무성 폰트 대체 (`fontId` 빈 값) | 전 텍스트 감사 | **0건** |
| **폰트 weight 위계** (⑤ §8-1 함정) | 분포 확인 | **400:524 / 500:200 / 700:275** — 평평하지 않음 ✅ |
| 토큰 팔레트 외 색 | 전 `fills` 감사 (④ 16색 + OS chrome) | **0건** |
| 그림자 (② 실측 0건) | 전 노드 `shadows` 감사 | **0건** |
| 무의미 노드 이름 (`Frame 27` 류) | 정규식 감사 | **0건** |
| 프레임 이름 ③ 대조 | 14개 전부 | **일치** |
| 폭 390 고정 | 14개 전부 | **일치** |
| 컴포넌트 선반 무결성 | `y ≤ -635` 32개 | **전부 `mainInstance()` 생존** ✅ |
| 고아 노드 정리 | 실패한 시도의 잔여 3개 | **제거 완료** |

---

## 7. ⑦ 시각 QA 체크리스트 대비 커버리지 (③ 7절)

| PRD 필수 요소 | 담당 화면 | 저작 결과 |
|---|---|---|
| H1 항공권 검색 진입 | #1 | ✅ 출발지·목적지·날짜·인원 4필드 + 전체폭 버튼 |
| H2 예정된 여정 | #1, #9 | ✅ `D-9` + 투어·체험·입장권 3건 |
| H3 둘러보기 묶음 | #1, #8 | ✅ 갈래 **4개**(마감임박/할인율/테마/땡처리) |
| H4 담아둔 목적지 | #1, #10 | ✅ **가격 하락 확인** 배너 + 30일 추이 차트 |
| H5 하단 이동 수단 | #1·#8·#9·#10·#12 | ✅ 동일 `Shell/TabBar` 컴포넌트, 활성 탭만 상이 |
| R1 항공편 목록 | #2 | ✅ 항공사·편명·출도착·소요·경유·가격 6항목 전부 |
| R2 경유 구간 표현 | #2, #4 | ✅ `상하이 푸둥에서 5시간 20분 대기` + #4 `LayoverBlock`(공항 밖 이동 불가) |
| R3 출발일 앞뒤 가격 | #2 | ✅ 날짜칩 7개 + 선택(brand)·최저(lowest) 구분 |
| R4 조건 좁히기 | #2, #5 | ✅ 진입점 칩 + 시트(경유·시간대·항공사·가격) |
| R5 비교함 | #2, #7, #14 | ✅ 진입점 `2/3` + 나란히 비교 목적지 + 빈 상태 |
| R6 운임 등급 선택 | #6 | ✅ **독립 프레임 아님.** Results clone 위 오버레이 |
| E1 40~60건 | #2 | ✅ `총 52건` |
| E2 최대 3개 | #2, #7, #14 | ✅ `2/3` · 열2+빈슬롯1 · `0/3` 일관 |
| E3 D-14 | #1, #12 | ✅ `D-9` + `출발 14일 전부터 여기에 표시돼요` |
| E4 첫 실행 0/0 | #12 | ✅ 여정·담아둠 **둘 다** 빈 상태, 검색·둘러보기 유지 |
| E5 0건 | #11 | ✅ `총 0건` + 탈출 3경로(18건/31건/47건) + 초기화 |
| E6 수 초 로딩 | #3, #2 | ✅ 스켈레톤 6행 + 60% 게이지 + 실시간 요금 고지 |
| E7 결제 전 마감 | #13 | ✅ 마감 모달 + 대체 2건 + 뒤 행 `마감됨` 잔존 |
| E8 오늘 자정 / 70% | #1, #8 | ✅ `오늘 자정 마감` · `70% 할인` 실제 문구로 존재 |

**미충족 항목 없음.**

---

## 8. ⑤ 보고의 오류 정정 (⑦·검증 단계가 알아야 함)

`05-components.md` §9 는 **"`export_shape` 가 서비스 장애로 전 시도 실패"** 라고 적었다.
**이 단계에서 20회 이상 성공했다. 장애가 아니었다.**

| 대상 | 결과 |
|---|---|
| 화면 board (`New/*`) | ✅ **전부 성공** (14화면, 20회+) |
| `.instance()` 결과 (Button/Primary 등) | ✅ 성공 |
| 컴포넌트 **메인 인스턴스** | ❌ 실패 (⑤가 이것만 시도했던 것으로 보인다) |

→ `00-env-facts.md` §"export_shape 함정" 의 오케스트레이터 판정이 **정확했다.**
⑦은 PNG 시각 검증을 정상 수행할 수 있다.

---

## 9. 저작 중 새로 발견한 함정 4개 (⑦·다음 실행 필독)

④·⑤ 문서에 없던 것들이다. 전부 실측으로 부딪혔다.

### 9-1. 🔴 `characters` 에 **빈 문자열·null 을 넣으면 throw** 한다

```
[PENPOT PLUGIN] Value not valid: . Code: :characters
```

`SectionHeader` 의 `MoreLink` 를 비우려고 `""` 를 넣었다가 **스크립트 전체가 죽었다**(2회).
→ 비우려면 **오버라이드를 건너뛰고 `hidden = true`** 로 처리한다. 체크박스 미선택도
`""` 가 아니라 `"○"` 같은 **실제 문자**를 써야 한다.

### 9-2. 🔴 컴포넌트 인스턴스는 **자식을 받지 않는다** (`appendChild` 가 조용히 상위로 감)

`dealCard.appendChild(badge)` 를 하면 에러 없이 **badge 가 화면 루트의 자식**이 된다.
`badge.parent` 는 화면을 가리키고, 카드 위에 안 보인다(z-order 뒤).
→ **화면 루트에 붙이고 `layoutChild.absolute = true` + 좌표 계산 + children 배열 끝으로 재삽입.**

### 9-3. 🔴 shape 객체는 **프록시라 `children.indexOf(shape)` 가 항상 -1**

`insertChild(idx, node)` 에 이 인덱스를 쓰면 **0번(맨 앞)에 삽입**된다 — 실제로 버튼이
화면 최상단으로 튀었다.
→ 위치는 반드시 **`children.findIndex(c => c.name === "...")`** 로 잡는다.
   (id 앞자리도 전부 동일해서 id 슬라이스 비교도 무용지물이다.)

### 9-4. 🔴 `insertChild` 는 **형제들의 `hidden` 플래그를 리셋**한다

clone 화면에서 숨겨둔 섹션이 `insertChild` 한 번에 **전부 다시 보이게 됐다**(#12·#14에서 발생).
→ **삽입을 전부 끝낸 뒤 마지막에 `hidden` 을 일괄 재적용**한다.

### 9-5. (보조) `hidden` 자식도 **레이아웃 높이를 그대로 차지**한다

숨겨도 프레임이 안 줄어든다(#3 에서 828px 유령 공간 확인).
→ 목표 높이를 맞추려면 **Spacer 를 차분만큼 재계산**해야 한다. 이 단계는 전부 그렇게 했다.

---

## 10. ④ 지침 중 실제로 조정한 것

| ④ 지침 | 조정 | 이유 |
|---|---|---|
| 뱃지 배경 = `tint 0.2` | **사진 위 뱃지만** 불투명 `surface.card` + 의미색 텍스트 | 0.2 틴트가 사진 위에서 **렌더링상 사라진다**(AGENTS.md의 오버레이 함정과 동일 현상). 새 색은 도입하지 않았다 |
| `applyToText(node, "700")` 문자열 | **`FontVariant` 객체** | ⑤ §8-1 실측대로. 문자열은 무성 400 |
| 모든 텍스트 `auto-height` | hug 라벨은 `auto-width` | ⑤ §8-2 실측대로 |

`T` 상수의 **색·크기·간격 값은 하나도 바꾸지 않았다.** 새 HEX 0개.

---

## 11. 미저작 · 실패

| 화면 | 등급 | 상태 |
|---|---|---|
| — | — | **없음. ③이 요구한 14개를 전부 저작했다** |

### 남은 한계 (정직하게)

| 항목 | 내용 |
|---|---|
| **아이콘** | ⑤가 `TabBar`·`TopBar` 아이콘을 **rect/ellipse 플레이스홀더**로 둔 것을 **그대로 뒀다.** PNG에서 회색 사각형으로 보인다. ⑤ §12가 "⑥·⑦이 `createShapeFromSvg` 로 교체 가능"이라 남겼으나, 이 단계는 **화면 조립을 14개 전부 끝내는 것**을 우선했다. ⑦이 교체하면 완성도가 오른다 |
| **`New/DealCollection` 높이** | ③ 산정 1420 → 실제 **1495**. 상품 리스트 3건을 넣으며 초과했다. ③ 8절이 "높이는 산정치, ⑥이 조정 가능(폭 390만 불변)"이라 명시해 허용 범위다 |
| **`New/Home-FirstRun` 높이** | 1420 산정 → 실제 **1689**. `hidden` 자식이 높이를 차지하는 9-5 함정 때문이며, 시각적으로는 빈 상태가 정상 표시된다 |
| **가격 추이 차트** | `PriceHistoryCard` 의 30개 막대는 **컴포넌트가 아니라 rect 직접 생성**이다. 단일 사용이라 ③ 5절이 컴포넌트 후보에서 제외한 항목이다 |

---

## 12. ⑦로의 인계 한 줄 요약

> **14개 화면이 `3-toss-result` 의 `y ≥ 0` 에 전부 있고, `export_shape` 는 정상 동작한다.**
> 오버레이 3종은 **뒤 보드 `opacity` 0.35** 방식이라 PNG에서 뒤 콘텐츠가 보여야 정상이다.
> 감사 6항목은 이미 0건이니, ⑦은 **시각적 균형·정렬 인상**과 **아이콘 플레이스홀더 교체**를 보라.
> 노드를 옮길 때는 **§9의 함정 4개**(빈 characters / 인스턴스 appendChild / indexOf -1 / insertChild가 hidden 리셋)를 반드시 지켜라.
