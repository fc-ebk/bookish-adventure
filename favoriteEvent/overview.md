# 찜 정모 MVP – 개발 & 분석 명세

## 1. 개요

### 목적

찜 정모 MVP는 사용자가 정모에 대해 관심을 저장하는 행동이
실제 정모 참여 및 모임 가입으로 이어지는지를 검증하기 위한 최소 기능이다.

이번 MVP의 성공 기준은 기능 사용량이 아니라, 찜 이후 사용자 행동이 실제로 달라지는지 여부임.

---

## 2. 핵심 원칙

* 기능 티켓에는 반드시 **분석 가능성(계측)**이 포함된다.
* 화면 단위가 아니라 **사용자 행동 단위**로 이벤트를 정의한다.
* MVP 단계에서는 **빈도보다 인지 여부**를 우선한다.
* 중복 로그는 의도적으로 제한한다.

---

## 3. 사용자 플로우 (요약)

1. 사용자가 정모를 인식한다
2. 정모를 찜한다
3. 찜한 정모를 다시 확인한다
4. 정모에 참여하거나 모임에 가입한다

이 흐름이 **GA 퍼널로 재현 가능해야 한다.**

---

## 4. 기능 & 계측 티켓 요약

### Ticket 1. 정모 노출 처리 + 노출 이벤트 계측

**기능**

* 모임 화면 내 정모 리스트 노출
* 정모 리스트 셀 클릭 시 해당 정모로 포커싱

**계측**

* `event_exposed`

  * 동일 사용자 + 동일 정모 기준 최초 1회만 기록
  * 화면 이동/스크롤 재노출 시 중복 기록하지 않음

**파라미터**

* user_id
* event_id
* group_id
* source_category: event_context / group_context / saved_event_list
* exposure_method: list_visible / scroll_focus

---

### Ticket 2. 정모 찜 / 해제 기능 + 이벤트 계측

**기능**

* 정모 카드 하단 찜 버튼 추가
* 찜/해제 토글
* 중복 찜 방지

**계측**

* `event_saved`
* `event_unsaved`

**파라미터**

* user_id
* event_id
* group_id
* timestamp

---

### Ticket 3. 마이페이지 ‘찜한 정모’ 진입 버튼

**기능**

* 마이페이지 요약 영역에 ‘찜한 정모’ 버튼 추가
* 찜한 정모 리스트로 이동
* 찜한 정모 개수 표시

**계측**

* `saved_event_entry_clicked`

**파라미터**

* user_id
* entry_point: mypage
* timestamp

---

### Ticket 4. 찜한 정모 리스트 화면

**기능**

* 찜한 정모 리스트 조회
* 정모 카드 UI 재사용
* 상태별 CTA 분기

  * 미가입: 모임 가입하고 참석
  * 종료: 모임 둘러보기
* 클릭 시 모임 화면으로 이동

  * 진행중: 해당 정모 포커싱
  * 종료: 정기모임 섹션 포커싱

**계측**

* `saved_event_list_viewed`
* 리스트 클릭 시 `event_exposed` 재사용

  * source_category: saved_event_list
  * exposure_method: scroll_focus

---

### Ticket 5. 정모 종료 처리 + 참여/가입 계측

**기능**

* 정모 종료 상태 업데이트
* 찜 데이터 유지
* 찜 목록에서 종료 상태 표시

**계측**

* `event_joined`
* `group_joined`

---

### Ticket 6. 알림 (선택, MVP 후순위)

**기능**

* 정모 D-1 알림
* 풀북 → 자리 발생 알림

**계측**

* 알림 노출/클릭 이벤트 (선택)

---

## 5. GA 퍼널 정의 (MVP 기준)

### 필수 퍼널

* `event_exposed → event_saved → event_joined`
* `event_saved → group_joined`

### 보조 퍼널

* `saved_event_list_viewed → event_exposed → event_joined`

퍼널은 **동일 사용자 기준**으로 해석한다.

---

## 6. 중복 기록 정책 (중요)

* `event_exposed`는 **정모 인지 이벤트**
* 동일 사용자 기준 동일 정모는 최초 1회만 기록
* 중복 기록은 퍼널 왜곡 및 전환율 저하를 유발할 수 있으므로 MVP에서는 제한

재노출/빈도 분석은 이후 버전에서 별도 이벤트로 확장한다.

---

## 7. Definition of Done

* 기능이 실제 사용자 행동으로 동작한다
* 모든 핵심 행동에 대응하는 이벤트가 GA로 전송된다
* GA에서 아래 흐름이 실제 데이터로 확인된다

  * event_exposed → event_saved → event_joined
  * event_saved → group_joined

---

## 8. 한 줄 요약

찜 정모 MVP는 정모에 대한 관심 저장 기능을 빠르게 출시하고,
그 관심이 실제 정모 참여와 모임 가입으로 이어지는지를
GA 퍼널로 검증하기 위한 최소 기능 세트다.
