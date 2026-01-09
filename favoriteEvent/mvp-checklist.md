# 찜 정모 MVP – 최종 개발 체크리스트

> 기능 티켓 = 사용자 기능 + 분석 가능성(계측)까지 포함

---

## 1. 정모 노출 처리 + 노출 이벤트 계측

### 목적

- 사용자가 특정 정모를 인식한 시점을 기록한다.
- 정모가 여러 방식으로 보여져도 하나의 이벤트로 관리한다.

### 기능 작업

- [x] 모임 화면에서 정모 리스트 렌더링
- [x] 정모 리스트에서 해당 셀 클릭 시, 모임 화면 내 해당 정모 위치로 포커싱

### 계측 작업

- [ ] `event_exposed` 이벤트 정의 및 전송
- [ ] 동일 사용자 기준, 동일 정모에 대해 최초 1회만 기록(화면 이동/스크롤 재노출 포함 중복 기록 금지)
- [ ] 중복 전송 방지 로직 적용

### 이벤트 조건

- 모임 화면 진입 시 정모 카드가 화면에 노출된 경우
- 정모 리스트에서 클릭 후, 해당 정모가 화면에 포커싱된 경우

### 파라미터

- `user_id`
- `event_id`
- `group_id`
- `source_category`

  - `event_context` (정모를 보고 들어온 경우)
  - `group_context` (모임 화면 내 정모를 본 경우)
  - `saved_event_list` (찜한 정모 리스트에서 진입한 경우)
- `exposure_method`

  - `list_visible` (카드가 자연스럽게 화면에 노출된 경우)
  - `scroll_focus` (해당 정모가 포커싱된 경우)

---

## 2. 정모 찜 / 해제 기능 + 찜 이벤트 계측

### 목적

- 사용자가 정모에 관심을 저장하거나 해제할 수 있도록 한다.
- 찜 행동을 이벤트 단위로 기록한다.

### 기능 작업

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl8mRhfTUk4FJal078XwnlK5_Ere-9QmJcA0k3DJJ0HgPaFnT5rn0Uv0gXMbJ96pTIoRBWVgAjunehYefyTt816Fv7Ae-Szau-XhjfpJyY26VCB4Fk9gDxtJH8K55s79UjRyOwelMTv4W8cU18vDdjvOeXEF3iOJHisoNkbB4DZaAMzEs_KE=s1024-rj-mp2" width="360">

> TO-BE: 1번 카드 <br>
> AS-IS: 2번 카드

- [ ] 모임 > 정기 모임 > 정모 카드 하단에 `하트(찜)` 아이콘 버튼 추가
- [ ] 모임 > 정기 모임 > 정모 카드 하단의 `공유` 아이콘 버튼 UI 조정(찜 버튼과 함께 배치)
- [ ] 찜 / 해제 토글 동작 구현
- [ ] 동일 정모 중복 찜 방지

### 계측 작업

- [ ] 찜 시 `event_saved` 이벤트 전송
- [ ] 찜 해제 시 `event_unsaved` 이벤트 전송

### 파라미터

- `user_id`
- `event_id`
- `group_id`
- `timestamp`

---

## 3. 마이페이지 ‘찜한 정모’ 진입 버튼 추가 + 계측

### 목적

- 사용자가 찜한 정모 리스트로 진입할 수 있게 한다.

### 기능 작업

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl9mm8lktZDt8MnBOv8kKwjQjqXjpobK2NJ_WwQjS-x4jPcayiDbL9HM8gjFtFhmVXZYE_qI02owu69poVY5YYbjItNQ0hv1_s5q6WAr_L3exETv3a57tOxYAcy2FjvOiwtTaQp12pRj2bBCFZphcLJ6EpaFqrDeLulYH_qeg9S7S8NufsER=s1024-rj-mp2" width="360" />

- [ ] 마이페이지 상단 요약 영역에 `찜한 정모` 버튼 추가
- [ ] 기존 `찜 모임 / 최근 본 모임 / 초대받은 모임`과 동일한 UI 패턴 사용
- [ ] 버튼 클릭 시 `찜한 정모 리스트` 화면으로 이동
- [ ] 찜한 정모 개수 표시

### 계측 작업

- [ ] 마이페이지에서 버튼 클릭 시 이벤트 기록: `saved_event_entry_clicked`

### 파라미터

- `user_id`
- `entry_point`: `mypage`
- `timestamp`

---

## 4. 찜한 정모 리스트 화면 구성 (정렬/섹션 포함) + 계측

### 목적

- 사용자가 찜한 정모를 한 화면에서 확인하고, 빠르게 참석 여부를 결정할 수 있게 한다.
- 리스트를 뚱뚱하게 만들지 않으면서(압축 UI) 메인 행동(참석)을 유지한다.

### 기능 작업

#### 리스트

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl9Rjsg77xGKd59gT6vr_Iy2G0V_T6I2Yn0HwAviUFxpvKbWJdEeBZT63gMQBEtPrNREUi6yv3KxJhinAGniDT4XOKwDLXcRfDCcgWx0sKfWTqf2qIlBrzn5k_GXgmLJuHrwXs6Vzdl0YpfMu7k3G20mSpGzw6bsbu-HdKWbkPKMhxUcn_1H=s1024-rj-mp2" width="360" />

- [ ] 찜한 정모 리스트 조회 API 연동
- [ ] 리스트 구성: 진행 예정 정모만 노출(종료 정모는 리스트에서 제외)
- [ ] 상단 네비게이션 바
  - [ ] 뒤로가기 버튼
    - [ ] 마이페이지로 이동
  - [ ] 타이틀: 찜한 모임
- [ ] 정렬 및 섹션 헤더
  - [ ] 섹션 1: `오늘/내일` (오름차순)
  - [ ] 섹션 2: `이후 일정` (오름차순)

#### 카드

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl-6DOaUWIVO2jpwPEwBgayh_5MdN0qsm0h5nmf2xElVxDtDprunLYmyeWlSG-p2_mRfL1kp5xnfe01KKowWSHcD_iJgipXbzuGqmxUHIXEEe-3dywcNrcXbi9xCM_f_GPbGI2BVmmVPy4vIg2xv-fA-d7cx25pT9KopIWBEjCp-Wnrv_Hw=s1024-rj-mp2" width="360" />

- [ ] 카드 UI: 기존 2번 정모 카드 기반 “압축 UI” 적용(이미지 제거, 정보 축약)
  - [ ] 정모명 1줄
  - [ ] 날짜/시간 + 지역(구 단위) + 인원(예: 3/20) 1줄
  - [ ] 하단 액션: `하트(찜 해제)` + `메인 CTA(모임 내 해당 정모로 이동)` 한 줄 배치
- [ ] CTA 텍스트 분기
  - [ ] 모임 가입 O & 진행중: `참석`
  - [ ] 모임 가입 X & 진행중: `모임 가입하고 참석`
  - [ ] (종료 정모는 리스트에서 제외하므로) 종료 CTA는 리스트에서 사용하지 않음
- [ ] 리스트 아이템 클릭 시 해당 정모가 포함된 모임 화면으로 이동
  - [ ] 해당 정모 위치로 포커싱(스크롤)

### 계측 작업

- [ ] 찜한 정모 리스트 진입 시 이벤트 기록: `saved_event_list_viewed`
- [ ] 찜한 정모 리스트에서 정모 클릭 후 포커싱 완료 시 `event_exposed` 재사용 전송

  - `source_category`: `saved_event_list`
  - `exposure_method`: `scroll_focus`

### `saved_event_list_viewed` 파라미터

- `user_id`
- `source`: `mypage`
- `timestamp`

---

## 5. 정모 참여/모임 가입 이벤트 계측 + 종료 상태 처리

### 목적

- 찜 이후 실제 행동(참여/가입)을 측정한다.
- 종료 상태는 데이터로 관리하되, 찜 리스트에서는 노출하지 않는다.

### 기능 작업

- [ ] 정모 종료 시 상태 업데이트
- [ ] 찜 데이터는 유지(삭제하지 않음)
- [ ] 찜한 정모 리스트 조회 시 종료 정모는 제외 처리

### 계측 작업

- [ ] 정모 참여 확정 시 `event_joined` 이벤트 전송
- [ ] 모임 가입 완료 시 `group_joined` 이벤트 전송
- [ ] 동일 사용자 기준으로 이벤트 연결 가능하도록 전송

---

## 6. 알림

### 목적

- 찜한 정모를 다시 떠올리게 한다.

### 기능 작업

#### 푸쉬 알림

- [ ] 정모 1일 전 알림 트리거
  - [ ] 메시지: 찜한 정모가 내일 시작돼요. 확인해 보세요.
- [ ] 풀북 정모에 자리 발생 시 알림 트리거
  - [ ] 메시지: 찜한 정모에 자리가 났어요! 참여해 보세요.
- [ ] 알림 트리거의 우선순위는 자리 발생 > 1일 전

#### 알림 리스트

- [ ] 알림 리스트에서 정모로 바로가기
  - [ ] UI는 기존 그대로
    - [ ] 사진: 정모에 등록된 사진
    - [ ] 내용
      - [ ] 1일 전: 찜하셨던 정모 `정모 제목(날짜/위치)`가 내일 시작돼요. 확인해보세요!
      - [ ] 자리 발생 시: 찜하셨던 정모 `정모 제목(날짜/위치)`에 빈자리가 났어요. 지금 바로 참여해보세요!
    - [ ] 아이콘: 메일 아이콘

### 계측 작업

- [ ] 푸시/앱 내 알림 클릭 시 `notification_clicked` 이벤트 전송
- [ ] 알림 이후 행동은 기존 이벤트(event_exposed, event_joined 등)로 연결

### `notification_clicked` 파라미터

- `user_id`
- `channel`

  - `push`
  - `inapp`
- `notification_type`

  - `event_d-1`
  - `event_slot_opened`
- `event_id`
- `group_id`
- `timestamp`

---

## 공통 완료 기준 (Definition of Done)

- [ ] 기능이 실제 사용자 행동으로 동작한다
- [ ] 각 기능에 대응하는 이벤트 로그가 GA로 전송된다
- [ ] GA에서 아래 퍼널이 구성 가능하고, 실제 데이터로 확인된다

  - [ ] 동일 사용자 기준 `event_exposed → event_saved → event_joined`
  - [ ] `event_saved → group_joined`
- [ ] `event_exposed`는 동일 사용자-정모 기준 중복 기록되지 않는다

---

## 보류(후속 논의)

- 종료된 찜 정모를 활용한 “다음 모임/다음 정모” 루프는 홈 화면에 별도 섹션으로 배치 예정 (추후 설계)
