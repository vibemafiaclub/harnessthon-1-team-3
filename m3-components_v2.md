# Material 3 Components Spec

> **상태: 초안 (검증 필요)**
> 이 문서는 Material 3 표준 규격을 정리한 초안입니다.
> 사용 전 반드시 문서 하단의 "검증 절차"를 실행해 공식 문서와 대조하십시오.
> 컬러는 role 이름으로만 표기합니다. hex 값은 `tokens.json`에서만 관리합니다.
> 단위는 모두 dp (= iOS의 pt, 웹의 px과 1:1 대응).

---

## 0. 공통 규칙

| 항목 | 값 |
|---|---|
| 그리드 | 4dp 단위 (4 / 8 / 12 / 16 / 24 / 32 / 48) |
| 최소 터치 영역 | 48 × 48dp |
| 화면 좌우 여백 | 16dp |
| 기본 아이콘 크기 | 24dp |
| 폰트 | Roboto (한글: Pretendard 또는 Noto Sans KR) |

### Shape Scale (모서리)

| 이름 | 값 |
|---|---|
| None | 0 |
| Extra Small | 4 |
| Small | 8 |
| Medium | 12 |
| Large | 16 |
| Extra Large | 28 |
| Full | 완전 둥글게 (알약형) |

### Type Scale (텍스트)

| 이름 | 크기 | 행간 | 굵기 | 자간 |
|---|---|---|---|---|
| Display Large | 57 | 64 | 400 | -0.25 |
| Display Medium | 45 | 52 | 400 | 0 |
| Display Small | 36 | 44 | 400 | 0 |
| Headline Large | 32 | 40 | 400 | 0 |
| Headline Medium | 28 | 36 | 400 | 0 |
| Headline Small | 24 | 32 | 400 | 0 |
| Title Large | 22 | 28 | 400 | 0 |
| Title Medium | 16 | 24 | 500 | 0.15 |
| Title Small | 14 | 20 | 500 | 0.1 |
| Body Large | 16 | 24 | 400 | 0.5 |
| Body Medium | 14 | 20 | 400 | 0.25 |
| Body Small | 12 | 16 | 400 | 0.4 |
| Label Large | 14 | 20 | 500 | 0.1 |
| Label Medium | 12 | 16 | 500 | 0.5 |
| Label Small | 11 | 16 | 500 | 0.5 |

### 상태 (States) — 모든 컴포넌트 공통

| 상태 | State layer 불투명도 |
|---|---|
| Enabled | 0% |
| Hovered | 8% |
| Focused | 10% |
| Pressed | 10% |
| Dragged | 16% |
| Disabled | 컨테이너 12% / 콘텐츠 38% |

State layer 색상은 해당 요소의 콘텐츠 컬러 role을 사용합니다.

---

## 1. Button

### Variants (강조도 높은 순)

| Variant | 컨테이너 | 텍스트/아이콘 | 용도 |
|---|---|---|---|
| Filled | primary | on-primary | 화면당 1개, 최우선 행동 |
| Filled Tonal | secondary-container | on-secondary-container | 두 번째 강조 |
| Elevated | surface-container-low + 그림자 | primary | 배경과 분리 필요할 때 |
| Outlined | 투명 + outline 테두리 1dp | primary | 보조 행동 |
| Text | 투명 | primary | 최소 강조, 링크성 |

### 규격 (표준 크기)

| 항목 | 값 |
|---|---|
| 높이 | 40 |
| 모서리 | Full (= 20) |
| 좌우 패딩 | 24 |
| 아이콘 있을 때 패딩 | 왼쪽 16 / 오른쪽 24 |
| 아이콘 크기 | 18 |
| 아이콘–텍스트 간격 | 8 |
| 텍스트 | Label Large |
| 터치 영역 | 48 |
| 최소 너비 | 없음 (콘텐츠 기준) |

### Expressive 크기 5단계 — ⚠️ 미확인

M3 Expressive 업데이트로 XSmall / Small / Medium / Large / XLarge 5단계와
Round / Square 2가지 모양이 추가되었습니다. **정확한 수치는 검증 필요.**

| 크기 | 높이 | 모서리 | 텍스트 |
|---|---|---|---|
| XSmall | 미확인 | 미확인 | 미확인 |
| Small | 미확인 | 미확인 | 미확인 |
| Medium | 미확인 | 미확인 | 미확인 |
| Large | 미확인 | 미확인 | 미확인 |
| XLarge | 미확인 | 미확인 | 미확인 |

### 사용 규칙
- 한 화면에 Filled는 1개만
- 버튼 텍스트는 동사로, 1~2단어
- 텍스트 줄바꿈 금지
- 나란히 놓을 때 간격 8dp

출처: m3.material.io/components/buttons/specs

---

## 2. FAB (Floating Action Button)

| 종류 | 크기 | 모서리 | 아이콘 |
|---|---|---|---|
| FAB Small | 40 | 12 | 24 |
| FAB (기본) | 56 | 16 | 24 |
| FAB Large | 96 | 28 | 36 |

**Extended FAB**

| 항목 | 값 |
|---|---|
| 높이 | 56 |
| 모서리 | 16 |
| 좌우 패딩 | 16 |
| 아이콘–텍스트 간격 | 12 |
| 텍스트 | Label Large |

| 컬러 종류 | 컨테이너 | 아이콘 |
|---|---|---|
| Primary | primary-container | on-primary-container |
| Secondary | secondary-container | on-secondary-container |
| Tertiary | tertiary-container | on-tertiary-container |
| Surface | surface-container-high | primary |

### 사용 규칙
- 화면당 1개
- 위치: 우측 하단, 화면 가장자리에서 16dp
- Navigation Bar가 있으면 그 위 16dp
- 화면의 핵심 행동 하나에만 사용

출처: m3.material.io/components/floating-action-button/specs

---

## 3. Text Field

### Variants

| Variant | 특징 |
|---|---|
| Filled | 배경 채움, 하단 인디케이터 선 |
| Outlined | 테두리만, 배경 투명 |

### 규격

| 항목 | Filled | Outlined |
|---|---|---|
| 높이 | 56 | 56 |
| 모서리 | 4 (상단만) | 4 (전체) |
| 좌우 패딩 | 16 | 16 |
| 컨테이너 | surface-container-highest | 투명 |
| 테두리 | 하단 1dp (활성 시 2dp) | 1dp (활성 시 2dp) |
| 아이콘 크기 | 24 | 24 |

### 텍스트 스타일

| 요소 | 스타일 | 컬러 role |
|---|---|---|
| Label (기본 상태) | Body Large | on-surface-variant |
| Label (축소 상태) | Body Small | primary |
| 입력값 | Body Large | on-surface |
| Supporting text | Body Small | on-surface-variant |
| Error text | Body Small | error |

### 상태별 컬러
- Enabled: outline
- Focused: primary (테두리 2dp)
- Error: error
- Disabled: on-surface 38%

### 사용 규칙
- Label은 항상 표시 (placeholder만 쓰지 말 것)
- 에러 시 supporting text로 해결 방법 안내
- Filled와 Outlined를 한 화면에 섞지 말 것

출처: m3.material.io/components/text-fields/specs

---

## 4. Card

### Variants

| Variant | 컨테이너 | Elevation | 용도 |
|---|---|---|---|
| Elevated | surface-container-low | Level 1 | 배경과 분리 강조 |
| Filled | surface-container-highest | Level 0 | 그룹 구분 |
| Outlined | surface + outline-variant 1dp | Level 0 | 가장 담백 |

### 규격

| 항목 | 값 |
|---|---|
| 모서리 | 12 (Medium) |
| 내부 패딩 | 16 |
| 카드 간 간격 | 8 또는 16 |
| 이미지 모서리 | 카드 상단에 붙을 경우 상단만 12 |

### 내부 텍스트 권장

| 요소 | 스타일 |
|---|---|
| 제목 | Title Medium |
| 부제 | Body Medium (on-surface-variant) |
| 본문 | Body Small |

### 사용 규칙
- 카드 안에 카드 넣지 말 것
- 카드 전체가 클릭 가능하면 상태 레이어 적용
- 한 화면에서 Variant 하나만 사용

출처: m3.material.io/components/cards/specs

---

## 5. Navigation Bar (하단 탭)

| 항목 | 값 |
|---|---|
| 높이 | 80 |
| 컨테이너 | surface-container |
| 탭 개수 | 3~5개 |
| 아이콘 크기 | 24 |
| 활성 인디케이터 | 너비 64 / 높이 32 / 모서리 Full |
| 인디케이터 컬러 | secondary-container |
| 상단 여백 | 12 |
| 아이콘–라벨 간격 | 4 |
| 라벨 텍스트 | Label Medium |

### 컬러

| 상태 | 아이콘 | 라벨 |
|---|---|---|
| Active | on-secondary-container | on-surface |
| Inactive | on-surface-variant | on-surface-variant |

### 사용 규칙
- 최상위 목적지만 배치
- 라벨 1~2단어
- 6개 이상이면 Navigation Drawer 사용
- 탭 순서는 사용 빈도순

출처: m3.material.io/components/navigation-bar/specs

---

## 6. Top App Bar

### Variants

| Variant | 높이 | 제목 스타일 |
|---|---|---|
| Small | 64 | Title Large |
| Medium | 112 | Headline Small |
| Large | 152 | Headline Medium |
| Center-aligned | 64 | Title Large (중앙 정렬) |

### 규격

| 항목 | 값 |
|---|---|
| 컨테이너 | surface |
| 스크롤 시 컨테이너 | surface-container |
| 좌우 패딩 | 4 (아이콘 기준) / 16 (텍스트 기준) |
| 아이콘 크기 | 24 |
| 아이콘 터치 영역 | 48 |
| 우측 액션 아이콘 | 최대 3개 |

### 컬러
- 제목: on-surface
- 아이콘: on-surface-variant
- Leading 아이콘(뒤로가기): on-surface

### 사용 규칙
- 뒤로가기는 항상 좌측
- 액션 4개 이상이면 오버플로우 메뉴(⋮)로
- Medium/Large는 스크롤 시 Small로 축소

출처: m3.material.io/components/top-app-bar/specs

---

## 7. List

### 규격

| 종류 | 높이 | 텍스트 |
|---|---|---|
| 1줄 | 56 | Body Large |
| 2줄 | 72 | Body Large + Body Medium |
| 3줄 | 88 | Body Large + Body Medium ×2 |

| 항목 | 값 |
|---|---|
| 좌우 패딩 | 16 |
| Leading 아이콘 | 24 (좌측 여백 16) |
| Leading 아바타 | 40 |
| Leading 이미지 | 56 |
| Trailing 아이콘 | 24 |
| 아이콘–텍스트 간격 | 16 |
| 구분선 | outline-variant 1dp |

### 컬러
- 주 텍스트: on-surface
- 보조 텍스트: on-surface-variant
- 아이콘: on-surface-variant

출처: m3.material.io/components/lists/specs

---

## 8. Chip

### Variants

| Variant | 용도 |
|---|---|
| Assist | 보조 행동 |
| Filter | 필터 선택 (다중 가능) |
| Input | 사용자 입력값 표시 (삭제 가능) |
| Suggestion | 추천 항목 |

### 규격

| 항목 | 값 |
|---|---|
| 높이 | 32 |
| 모서리 | 8 (Small) |
| 좌우 패딩 | 16 (아이콘 없을 때) / 8 (아이콘 있을 때) |
| 아이콘 크기 | 18 |
| 아이콘–텍스트 간격 | 8 |
| 텍스트 | Label Large |
| 칩 간 간격 | 8 |
| 테두리 | outline 1dp (선택 안 됨) |

### 선택 상태
- 컨테이너: secondary-container
- 텍스트/아이콘: on-secondary-container
- 좌측에 체크 아이콘 표시

출처: m3.material.io/components/chips/specs

---

## 9. Bottom Sheet

| 항목 | 값 |
|---|---|
| 모서리 | 28 (상단만) |
| 컨테이너 | surface-container-low |
| Drag handle 크기 | 너비 32 / 높이 4 / 모서리 Full |
| Drag handle 컬러 | on-surface-variant 40% |
| Drag handle 상하 여백 | 22 |
| 내부 좌우 패딩 | 16 |
| 최대 너비 | 640 (태블릿) |

### 종류
- **Modal**: 뒤 배경에 scrim, 바깥 탭 시 닫힘
- **Standard**: scrim 없음, 콘텐츠와 공존

출처: m3.material.io/components/bottom-sheets/specs

---

## 10. Dialog

| 항목 | 값 |
|---|---|
| 모서리 | 28 (Extra Large) |
| 컨테이너 | surface-container-high |
| 내부 패딩 | 24 |
| 최소 너비 | 280 |
| 최대 너비 | 560 |
| 아이콘 크기 | 24 (선택, 중앙 정렬) |
| Scrim | scrim 32% |

### 텍스트

| 요소 | 스타일 | 컬러 role |
|---|---|---|
| 제목 | Headline Small | on-surface |
| 본문 | Body Medium | on-surface-variant |
| 버튼 | Label Large | primary |

### 버튼 배치
- 우측 하단 정렬
- 확인 버튼이 오른쪽
- Text Button 사용
- 버튼 간 간격 8

### 사용 규칙
- 제목은 질문형 또는 명확한 서술
- 버튼 최대 2개
- "확인/취소" 대신 구체적 동사 사용 (예: "삭제", "저장")

출처: m3.material.io/components/dialogs/specs

---

## 11. Snackbar

| 항목 | 값 |
|---|---|
| 최소 높이 | 48 (1줄) / 68 (2줄) |
| 모서리 | 4 (Extra Small) |
| 컨테이너 | inverse-surface |
| 텍스트 컬러 | inverse-on-surface |
| 액션 텍스트 컬러 | inverse-primary |
| 좌우 패딩 | 16 |
| 텍스트 | Body Medium |
| 액션 텍스트 | Label Large |
| 화면 가장자리 여백 | 16 |
| 표시 시간 | 4~10초 |

### 사용 규칙
- 화면당 1개만
- 액션은 최대 1개
- 필수 행동을 담지 말 것 (자동으로 사라짐)
- Navigation Bar나 FAB 위에 표시

출처: m3.material.io/components/snackbar/specs

---

## 12. Switch

| 항목 | 값 |
|---|---|
| 트랙 너비 | 52 |
| 트랙 높이 | 32 |
| 트랙 모서리 | Full |
| 핸들 크기 (Off) | 16 |
| 핸들 크기 (On) | 24 |
| 핸들 크기 (Pressed) | 28 |
| 터치 영역 | 48 |

### 컬러

| 상태 | 트랙 | 핸들 |
|---|---|---|
| On | primary | on-primary |
| Off | surface-container-highest + outline 테두리 2dp | outline |
| Disabled | surface-variant 12% | on-surface 38% |

### 사용 규칙
- 즉시 적용되는 설정에만 사용 (저장 버튼 불필요)
- 라벨은 항상 왼쪽, 스위치는 오른쪽
- 확인이 필요한 행동엔 Checkbox 사용

출처: m3.material.io/components/switch/specs

---

## 13. Tabs

| 항목 | Primary | Secondary |
|---|---|---|
| 높이 | 48 (텍스트만) / 64 (아이콘+텍스트) | 48 |
| 텍스트 | Title Small | Title Small |
| 인디케이터 | 너비=라벨 너비, 높이 3, 모서리 상단 3 | 전체 너비, 높이 2 |
| 인디케이터 컬러 | primary | primary |

| 항목 | 값 |
|---|---|
| 좌우 패딩 | 16 |
| 최소 탭 너비 | 90 |
| 컨테이너 | surface |
| 활성 텍스트 | primary (Primary) / on-surface (Secondary) |
| 비활성 텍스트 | on-surface-variant |

### 사용 규칙
- 탭 2~6개
- 라벨 1~2단어
- 스와이프로 전환 가능하게
- Primary는 최상위, Secondary는 그 하위 분류

출처: m3.material.io/components/tabs/specs

---

## 14. Elevation

| Level | 그림자 | 사용처 |
|---|---|---|
| 0 | 없음 | 기본 표면, Filled/Outlined Card |
| 1 | 1dp | Elevated Card, Search Bar |
| 2 | 3dp | 스크롤된 Top App Bar |
| 3 | 6dp | FAB, Dialog |
| 4 | 8dp | Navigation Drawer |
| 5 | 12dp | 드래그 중인 요소 |

M3에서는 그림자와 함께 surface-container 계열 색상으로 높이를 표현합니다.

---

## 15. 금지 사항

- iOS 컴포넌트 사용 금지 (Tab Bar, Action Sheet, Segmented Control, iOS Alert)
- 이 문서에 없는 컴포넌트를 임의로 만들지 말 것
- 크기·패딩·모서리를 임의로 조정하지 말 것
- 컬러 hex를 이 문서나 화면 명세에 직접 쓰지 말 것
- 한 화면에서 같은 컴포넌트의 여러 Variant를 섞지 말 것



