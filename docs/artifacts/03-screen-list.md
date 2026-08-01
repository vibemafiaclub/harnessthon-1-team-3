# 03 — 화면 목록

> 입력: `docs/artifacts/01-prd-spec.md` (C절 필수화면 · D절 유저스토리 8행 + 진입점 4종 · E절 상황 8행)
> 이 목록은 **계산 결과**다. 개수를 미리 정하고 맞춘 것이 아니다.
> 모든 행에 PRD 원문 인용이 붙어 있다. 인용이 없는 화면은 목록에 없다.
> 저작 Page = `김주철` (①의 B절 결정). 프레임 이름은 F절 규칙에 따라 전부 `New/` 접두.

## 계산 근거 요약 (어떻게 이 개수가 나왔나)

| 출처 | 뽑힌 화면 수 | 비고 |
|---|---|---|
| C절 (명시 필수) | 3 | PRD가 "최소 3개"라 부른 하한선 |
| D절 스토리 S1~S6 + 진입점 4종 | +6 | 동작/확인 분리 · 진입점의 목적지 |
| E절 상황 E1~E5 | +6 | 빈 상태·로딩·실패 2종·대량·스타일 미설정 |
| 중복 병합 | −1 | E2(빈 상태) = S4b(최대 이탈 지점) → 1개로 합침 |
| **합계** | **14** | |

## 요약
| 등급 | 개수 |
|---|---|
| P0 | 3 |
| P1 | 6 |
| P2 | 5 |
| **합계** | **14** |

> P0 3개는 무조건 만든다. P1·P2는 위에서부터 시간이 허용하는 만큼.
> P2 5개 중 4개는 `clone()` 기반 상태 변형이라 저작 비용이 낮다 — 실제로는 전부 만들 수 있다.

---

## 화면 목록

| # | 프레임 이름 | 등급 | 목적 | base 화면 | 필수 요소 | 근거 (PRD 인용) |
|---|---|---|---|---|---|---|
| 1 | `New/Watchlist` | P0 | 담아둔 종목의 현재가와 등락을 한 화면에서 훑는다 | — | 종목 목록(종목명·현재가·등락률) / 상승·하락 시각적 구분 / 정렬·필터 진입점 / 종목 담기 진입점 | §6-1 "사용자가 담아둔 종목의 현재가와 등락을 한 화면에서 훑는다." · "정렬 또는 필터 **진입점**" |
| 2 | `New/StockDetail` | P0 | 종목 하나를 판단하고 그 자리에서 주문까지 끝낸다 | — | 가격 차트(1일/1주/1개월 기간 전환) / 현재가·등락 / 종목 기본 정보 / 하단 고정 매수·매도 액션 / 관심종목 담기 토글 | §6-2 "종목 하나를 판단하고, 그 자리에서 주문까지 끝낸다." · "**매수 / 매도 주문 진입** — 하단 고정 액션" |
| 3 | `New/Discover` | P0 | 무엇을 살지 못 정한 사용자가 오늘 살 만한 것을 찾는다 | — | 스타일 기반 추천(추천 이유 한 줄) / 오늘의 시장 이슈 / 전문가 의견(매수·중립·매도 분포 + 목표주가) / 실적 발표 일정 / 테마별 등락 + 진입점 / 스타일 설정 진입점 | §6-3 "무엇을 살지 못 정한 사용자가 **오늘 살 만한 것**을 찾는다." · "추천 이유가 한 줄로 붙어야 함" |
| 4 | `New/StockDetail-OrderSheet` | P1 | 수량·가격을 입력해 주문을 확정한다 (StockDetail 위 오버레이) | `New/StockDetail` | 수량 입력 / 가격 입력 / 예상 금액 / 주문 확정 버튼 / 스크림 | §6-2 "**주문 시트** — 수량·가격 입력, 예상 금액, 주문 확정 (별도 화면이 아니라 이 화면 위에 올라오는 형태)" · S3 "수량과 가격을 입력해 주문하고" |
| 5 | `New/OrderComplete` | P1 | 넣은 주문의 **결과**를 확인한다 | — | 체결/접수 상태 / 주문 요약(종목·수량·단가·총액) / 다음 행동(관심종목으로·내 주문 보기) | S3 "수량과 가격을 입력해 주문하고 **그 결과를 확인**하고 싶다." → 동작 화면과 결과 화면이 각각 필요 |
| 6 | `New/Watchlist-SortSheet` | P1 | 무엇을 먼저 볼지(정렬 기준·지표) 바꾼다 | `New/Watchlist` | 정렬 기준 목록(등락률·내 수익률·거래량·종목명·담은 순) / 선택 상태 표시 / 필터 칩 / 스크림 | §6-1 "정렬 또는 필터 **진입점**" · S2b "어떤 사용자는 등락률을, 어떤 사용자는 내 수익률을, 어떤 사용자는 거래량을 먼저 봅니다." |
| 7 | `New/StyleSetup` | P1 | 투자 스타일·정보 유형·테마를 사용자가 직접 고른다 | — | 투자 스타일 4종 선택(단기 수익형·배당형·성장형·안정형) / 관심 정보 유형 선택(호재악재·전문가의견·실적·수급) / 테마 5종 선택(반도체·항공우주·방산·2차전지·바이오) / 저장 액션 | §4 "세 가지(정보·스타일·테마)를 **사용자가 직접 고르게 하고**" · §6-3 "투자 스타일이 아직 없는 사용자를 위한 **설정 진입점**" |
| 8 | `New/ThemeDetail` | P1 | 테마 하나를 열어 그 테마에 뭐가 들어 있는지 본다 | — | 테마 헤더(테마명·테마 등락률) / 테마 설명 / 구성 종목 목록 / 담기 액션 | §4-3 "'어떤 테마가 요즘 오르는지'와 '그 테마에 뭐가 들어 있는지'를 **둘 다** 알고 싶어 합니다." · §6-3 "테마 — 테마별 등락과 **진입점**" |
| 9 | `New/StockSearch` | P1 | 종목을 찾아 관심종목에 담는다 (빈 상태의 탈출 경로) | — | 검색 입력 / 검색 결과 목록 / 담기 토글 / 추천·인기 종목 제안 | S1 "관심 있는 종목을 **모아두고**" (동작) · §3-4 "관심종목이 비어 있으면 아무것도 시작되지 않습니다." → 담는 경로가 없으면 스토리가 성립하지 않음 |
| 10 | `New/Watchlist-Empty` | P2 | 아직 아무것도 담지 않은 사용자를 다음 행동으로 넘긴다 | `New/Watchlist` | 빈 상태 일러스트·문구 / **종목 찾아보기 CTA** / 추천 종목 미리보기 / Discover 진입 유도 | §5 "가입 첫날이라 **아직 아무것도 담지 않은** 사용자가 매일 유입됩니다." · §3-4 "→ 이게 **가장 큰 이탈 지점**입니다." |
| 11 | `New/Watchlist-Loading` | P2 | 시세가 아직 들어오지 않은 몇 초를 견딘다 | `New/Watchlist` | 종목명은 유지 / 가격·등락 자리에 스켈레톤 / "시세 불러오는 중" 안내 | §5 "장 시작 직후에는 **시세가 아직 들어오지 않는** 몇 초가 있습니다." |
| 12 | `New/Watchlist-Dense` | P2 | 200개를 담은 사용자에게도 목록이 무너지지 않는다 | `New/Watchlist` | 촘촘 밀도 행(다수) / 섹션·인덱스 구분 / 총 개수 표기 / 스크롤 위치 힌트 | §5 "관심종목은 **평균 12개**를 담습니다. 많게는 **200개**까지 담는 사용자도 있습니다." |
| 13 | `New/OrderFailed` | P2 | 주문 실패 사유를 알리고 복구 경로를 준다 | `New/StockDetail-OrderSheet` | 실패 사유 2종 표시(잔고 부족 / 장 마감) / 사유별 복구 액션(입금하기 / 예약주문) / 주문 내용 유지 | §5 "주문을 넣었는데 **잔고가 모자라거나 장이 닫혀** 실패하는 경우가 있습니다." |
| 14 | `New/Discover-NoStyle` | P2 | 투자 스타일을 아직 고르지 않은 사용자에게도 무언가는 보여준다 | `New/Discover` | 추천 섹션 자리에 **스타일 설정 유도 카드** / 스타일 무관 대체 콘텐츠(시장 이슈·거래량 상위) / 설정 진입점 강조 | §5 "**투자 스타일을 아직 고르지 않은** 사용자에게도 무언가는 보여줘야 합니다." · §6-3 "투자 스타일이 아직 없는 사용자를 위한 **설정 진입점**" |

### 목록에서 제외한 후보 (인용 근거 부족)

| 후보 | 제외 사유 |
|---|---|
| 로그인·온보딩 | PRD 어디에도 인용할 문장이 없다. §5의 "가입 첫날"은 가입 화면이 아니라 **빈 상태**를 가리킨다(#10으로 반영) |
| 포트폴리오·잔고 화면 | S2b의 "내 수익률"은 **관심종목 목록의 지표 선택지**로 등장할 뿐, 별도 화면을 요구하는 문장이 없다 → #6 정렬 시트의 선택지로 흡수 |
| 알림·설정 일반 | 인용 가능한 PRD 문장 없음 |
| 매도 주문 시트 | §6-2가 "매수 / 매도 주문 진입"을 요구하나 시트 요구는 하나. #4를 매수/매도 탭 전환 구조로 만들어 흡수 |

---

## 상태 변형 (clone 대상)

> ⑥은 base를 먼저 완성하고 `shape.clone()` → **덮을 것만 얹는다.** 처음부터 다시 짓지 않는다.

| base 화면 | 변형 | 무엇이 달라지나 |
|---|---|---|
| `New/Watchlist` | `New/Watchlist-Empty` | 종목 리스트 영역을 통째로 제거 → 빈 상태 블록 + CTA로 교체. 헤더·탭바·정렬 진입점은 그대로 |
| `New/Watchlist` | `New/Watchlist-Loading` | `StockRow` 인스턴스의 가격·등락 텍스트를 스켈레톤 Rect로 교체. 종목명은 유지. 상단에 로딩 안내 바 추가 |
| `New/Watchlist` | `New/Watchlist-Dense` | `StockRow` 인스턴스를 12행 → 20행 이상으로 복제, 행 높이·패딩 축소 변형 적용. 헤더에 "총 200" 카운트 추가 |
| `New/Watchlist` | `New/Watchlist-SortSheet` | 뒤 화면 보드의 `opacity`를 낮추고(스크림 Rect를 덮지 **않는다**) 하단에 정렬 시트 보드를 올린다 |
| `New/StockDetail` | `New/StockDetail-OrderSheet` | 뒤 화면 보드 `opacity` 낮춤 + 하단 주문 시트 보드. 하단 고정 매수/매도 액션은 시트에 가려짐 |
| `New/StockDetail-OrderSheet` | `New/OrderFailed` | 시트 상단에 실패 배너 삽입, 확정 버튼 → 복구 액션으로 텍스트 오버라이드. 입력값은 유지 |
| `New/Discover` | `New/Discover-NoStyle` | 최상단 추천 섹션을 `StyleSetupPromptCard`로 교체. 나머지 섹션(시장 이슈·전문가 의견·실적·테마)은 그대로 |

> ⚠️ 반투명 스크림 오버레이는 렌더링에서 사라질 수 있다 → **뒤 보드의 `opacity`를 낮추는 방식**으로 저작한다 (AGENTS.md 함정 표).

---

## 화면별 필요 컴포넌트 (⑤단계 입력)

> 기준: **2개 이상 화면에 등장** 또는 **한 화면에서 3회 이상 반복** → 컴포넌트.

| 컴포넌트 이름 | 쓰이는 화면 | 반복 횟수 | 가변 요소 |
|---|---|---|---|
| `StockRow` | Watchlist, Watchlist-Loading, Watchlist-Dense, ThemeDetail, StockSearch, Discover(추천 리스트) | 화면당 6~20회 · 전체 최다 | 종목명 / 현재가 / 등락률 텍스트 / 등락 색상(상승·하락·보합) / 우측 지표 슬롯 / 담기 토글 on·off |
| `ChangeBadge` | Watchlist, StockDetail, ThemeDetail, Discover, StockSearch | 화면당 5~20회 | 부호(+/−) / 퍼센트 값 / 배경·글자 색(상승 red · 하락 blue · 보합 gray) |
| `SectionHeader` | Discover, ThemeDetail, StyleSetup, OrderComplete | 화면당 4~6회 | 제목 / 우측 "더보기" 유무 |
| `PrimaryButton` | StockDetail, OrderSheet, OrderComplete, OrderFailed, StyleSetup, Watchlist-Empty, StockSearch | 화면당 1~2회 | 라벨 / 상태(default·disabled) / 색(매수 red · 매도 blue · 중립) / 폭(fill·hug) |
| `ChipToggle` | StyleSetup(스타일4+정보4+테마5=13회), Discover(테마 칩), Watchlist-SortSheet(필터 칩), ThemeDetail | 최다 13회 | 라벨 / 선택 상태(on·off) |
| `AppBar` | 전 14화면 | 화면당 1회 | 타이틀 / 좌측 back 유무 / 우측 액션 아이콘 슬롯 |
| `TabBar` | Watchlist(+3변형), Discover(+1변형), StockSearch | 8화면 | 활성 탭 인덱스 |
| `BottomSheet` | Watchlist-SortSheet, StockDetail-OrderSheet, OrderFailed | 3회 | 시트 높이 / 핸들 / 타이틀 / 본문 슬롯 |
| `ListRowSelectable` | Watchlist-SortSheet(정렬 기준 5행), StyleSetup(스타일 4행) | 화면당 4~5회 | 라벨 / 보조 설명 / 체크 on·off |
| `RecommendCard` | Discover, Discover-NoStyle | 화면당 3회 | 종목명 / 현재가 / **추천 이유 한 줄** / 등락 배지 |
| `IssueCard` | Discover, Discover-NoStyle | 화면당 2~3회 | 이슈 제목 / 호재·악재 태그 / 연결된 종목 칩(1~3개) |
| `ConsensusBar` | Discover, StockDetail | 화면당 1~2회 | 매수/중립/매도 3구간 비율 / 목표주가 텍스트 |
| `EarningsRow` | Discover, StockDetail | 화면당 3~4회 | 종목명 / 발표일 / 서프라이즈 뱃지 |
| `ThemeCard` | Discover, ThemeDetail | 화면당 3~5회 | 테마명 / 테마 등락률 / 대표 종목 요약 |
| `PriceChart` | StockDetail, OrderSheet(뒤 배경), ThemeDetail(선택) | 1~2회 | 차트 폴리라인 / 기간 탭(1일·1주·1개월·3개월·1년) 활성값 |
| `PeriodTabs` | StockDetail, ThemeDetail | 1회 | 활성 인덱스 |
| `InfoKeyValue` | StockDetail(기본정보 6행), OrderComplete(주문 요약 4행), OrderSheet(예상 금액) | 화면당 3~6회 | 키 / 값 / 강조 여부 |
| `StatusBanner` | OrderFailed, Watchlist-Loading, Discover-NoStyle | 3회 | 아이콘 / 문구 / 톤(error·info) / 액션 링크 |
| `EmptyState` | Watchlist-Empty, StockSearch(결과 없음) | 2회 | 일러스트·아이콘 / 제목 / 설명 / CTA 라벨 |
| `SkeletonRow` | Watchlist-Loading | 8회 이상 (한 화면 3회↑ 기준 충족) | 바 폭 |
| `SearchField` | StockSearch, Watchlist(선택) | 1~2회 | placeholder / 입력값 유무 |
| `StyleSetupPromptCard` | Discover, Discover-NoStyle | 1회씩 (2화면) | 문구 / CTA 라벨 |
| `QuantityStepper` | OrderSheet, OrderFailed | 1~2회 | 값 / +− 활성 여부 |

> **인스턴스 오버라이드 원칙**: 데이터가 다른 행은 새로 그리지 않고 `characters` 텍스트와
> `fills`(penpot 형식 `{fillColor:"#RRGGBB", fillOpacity:1}`)를 오버라이드해 처리한다.

---

## 저작 순서 (⑥단계 입력)

> PRD §6 "아래 순서대로 완성해주세요"(Watchlist → StockDetail → Discover)를 P0 골격으로 삼고,
> **base를 먼저 완성한 뒤 clone 변형을 몰아서** 만든다. base가 흔들리면 변형이 전부 흔들린다.

1. `New/Watchlist` — P0. 첫 화면이자 `StockRow`·`ChangeBadge`·`AppBar`·`TabBar` 검증대. 여기서 컴포넌트가 맞으면 나머지가 빨라진다
2. `New/StockDetail` — P0. `PriceChart`·`PeriodTabs`·`InfoKeyValue`·`ConsensusBar` 신규 검증. 하단 고정 액션은 Spacer 높이를 **계산해서 명시**
3. `New/Discover` — P0. 섹션 우선순위 = 추천 → 시장 이슈 → 테마 → 전문가 의견 → 실적 일정 (§6-3 "무엇을 위로 올릴지가 설계")
4. **여기서 P0 3개 export_shape로 PNG 확인.** 어긋났으면 여기서 고친다. 이후 변형은 base를 복제하므로 되돌리기 비싸다
5. `New/StockDetail-OrderSheet` — #2 clone + 뒤 보드 opacity 낮춤 + 시트
6. `New/OrderComplete` — 신규. S3의 "결과 확인"
7. `New/Watchlist-SortSheet` — #1 clone + 시트
8. `New/StyleSetup` — 신규. `ChipToggle` 13회 밀집 검증
9. `New/ThemeDetail` — 신규이나 `StockRow` 재사용률 높음
10. `New/StockSearch` — 신규. `SearchField` + `StockRow` 재사용
11. `New/Watchlist-Empty` — #1 clone
12. `New/Watchlist-Loading` — #1 clone
13. `New/Watchlist-Dense` — #1 clone (행 복제)
14. `New/OrderFailed` — #5 clone
15. `New/Discover-NoStyle` — #3 clone
16. **마감 처리**: 전 화면의 `growType === "auto-height"` 텍스트를 `resize`로 재계산시킨다 (hHug 프레임 안 텍스트 잘림 방지)

### 화면 배치 규칙 (⑥이 좌표를 정할 때)

- 1행: P0 3개 (`Watchlist` → `StockDetail` → `Discover`) — PRD 명시 순서
- 2행: P1 6개 (`OrderSheet` → `OrderComplete` → `SortSheet` → `StyleSetup` → `ThemeDetail` → `StockSearch`)
- 3행: P2 5개 (`Watchlist-Empty` → `Watchlist-Loading` → `Watchlist-Dense` → `OrderFailed` → `Discover-NoStyle`)
- base와 그 변형이 **같은 열 또는 인접**하도록 둔다. 심사자가 대응관계를 눈으로 읽을 수 있어야 한다

---

## ⑦단계 체크리스트 (PRD 충족도 검증용)

| 검증 항목 | 어느 화면에서 확인 | 근거 |
|---|---|---|
| 종목명·현재가·등락률이 목록에 있다 | #1 | §6-1 |
| 상승/하락이 **시각적으로** 구분된다 | #1 | §6-1 |
| 정렬·필터 진입점이 있고 **목적지가 있다** | #1 → #6 | §6-1 진입점 |
| 가격 차트에 **기간 전환**이 있다 | #2 | §6-2 |
| 주문 시트가 **별도 화면이 아니라 오버레이**다 | #4 | §6-2 괄호 지시 |
| 주문 **결과**를 확인할 수 있다 | #5 | S3 |
| 추천에 **이유가 한 줄** 붙어 있다 | #3 | §6-3 |
| 시장 이슈가 **움직인 종목과 연결**돼 있다 | #3 | §6-3 |
| 전문가 의견에 **분포 + 목표주가**가 있다 | #3 | §6-3 |
| 실적 발표 일정이 있다 | #3 | §6-3 |
| 테마 진입점이 있고 **목적지가 있다** | #3 → #8 | §6-3 진입점 + §4-3 |
| 스타일 설정 진입점이 있고 **목적지가 있다** | #3/#14 → #7 | §6-3 진입점 |
| 정보·스타일·테마 **3종을 직접 고를 수 있다** | #7 | §4 총괄 |
| 빈 상태가 **다음 행동으로 넘긴다** | #10 → #9 | §3-4 |
| 로딩 상태가 있다 | #11 | §5 |
| 200개 밀도에서 무너지지 않는다 | #12 | §5 |
| 실패 사유 **2종**(잔고·장마감)이 표현된다 | #13 | §5 |
| 스타일 미설정자에게도 볼 것이 있다 | #14 | §5 |
| 전 프레임 이름이 `New/` 로 시작한다 | 전체 | §8 |
| 이름이 의미를 말한다 (`Frame 27` 없음) | 전체 | 평가 절 |
