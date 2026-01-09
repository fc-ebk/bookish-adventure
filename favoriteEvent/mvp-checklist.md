# 찜 정모 MVP – 최종 개발 체크리스트

> 1차(W03): 정모 찜 기능, 리스트업 기능 + 분석 가능성

---

## 1. 정모 찜 / 해제 기능

### 목적

- 사용자가 정모에 관심을 저장하거나 해제할 수 있도록 한다.
- 찜 행동을 이벤트 단위로 기록한다.

### 기능 작업 - 1: 모임 내 정기모임

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl8mRhfTUk4FJal078XwnlK5_Ere-9QmJcA0k3DJJ0HgPaFnT5rn0Uv0gXMbJ96pTIoRBWVgAjunehYefyTt816Fv7Ae-Szau-XhjfpJyY26VCB4Fk9gDxtJH8K55s79UjRyOwelMTv4W8cU18vDdjvOeXEF3iOJHisoNkbB4DZaAMzEs_KE=s1024-rj-mp2" width="360">

> TO-BE: 1번 카드 <br>
> AS-IS: 2번 카드

- [ ] 모임 > 정기 모임 > 정모 카드 하단에 `하트(찜)` 아이콘 버튼 추가
- [ ] 모임 > 정기 모임 > 정모 카드 하단의 `공유` 아이콘 버튼 UI 조정(찜 버튼 오른쪽에 함께 배치)
- [ ] 찜 / 해제 토글 동작 구현
  - [ ] 찜인 경우 빨간색 하트
  - [ ] 해제인 경우 회색 하트
- [ ] 동일 정모/클래스 중복 찜 방지

### 기능 작업 - 2: 클래스 상세화면

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl-tpbqDiwz3VRu3Md9x6LUTq4KHJg222Rf89BfmC_glnhESLkXQbsV-yNJ6rWl_7VUs5ERy9hco896N58Q7lozGOuDGSicnn-I5nGvRpTtEIlY8O1N82Rky3tol3r3Bm8h4UhTn_VY-fZJ-4HeSOO9MXWKK9tutqkDSHO7AsSGrAQ_FaP-S=s1024-rj-mp2" width="360">

- [ ] 클래스 > 소셜 클래스 우측 상단에 `하트(찜)` 아이콘 버튼 추가(공유 버튼 왼쪽에 함께 배치)
- [ ] 찜 / 해제 토글 동작 구현
  - [ ] 찜인 경우 빨간색 하트
  - [ ] 해제인 경우 회색 하트
- [ ] 동일 정모/클래스 중복 찜 방지

---

## 2. 마이페이지 ‘찜한 정모’ 진입 버튼 추가

### 목적

- 사용자가 찜한 정모 리스트로 진입할 수 있게 한다.

### 기능 작업

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl9mm8lktZDt8MnBOv8kKwjQjqXjpobK2NJ_WwQjS-x4jPcayiDbL9HM8gjFtFhmVXZYE_qI02owu69poVY5YYbjItNQ0hv1_s5q6WAr_L3exETv3a57tOxYAcy2FjvOiwtTaQp12pRj2bBCFZphcLJ6EpaFqrDeLulYH_qeg9S7S8NufsER=s1024-rj-mp2" width="360" />

- [ ] 마이페이지 상단 요약 영역에 `찜한 정모` 버튼 추가
- [ ] 기존 `찜 모임 / 최근 본 모임 / 초대받은 모임`과 동일한 UI 패턴 사용
- [ ] 버튼 클릭 시 `찜한 정모 리스트` 화면으로 이동
- [ ] 찜한 정모 개수 표시

---

## 3. 찜한 정모 리스트 화면 구성

### 목적

- 사용자가 찜한 정모를 한 화면에서 확인하고, 빠르게 참석 여부를 결정할 수 있게 한다.
- 리스트를 뚱뚱하게 만들지 않으면서(압축 UI) 메인 행동(참석)을 유지한다.

### 기능 작업 - 1: 리스트

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl9Rjsg77xGKd59gT6vr_Iy2G0V_T6I2Yn0HwAviUFxpvKbWJdEeBZT63gMQBEtPrNREUi6yv3KxJhinAGniDT4XOKwDLXcRfDCcgWx0sKfWTqf2qIlBrzn5k_GXgmLJuHrwXs6Vzdl0YpfMu7k3G20mSpGzw6bsbu-HdKWbkPKMhxUcn_1H=s1024-rj-mp2" width="360" />

*UI는 참고만 바랍니다.


- [ ] 찜한 정모 리스트 조회 API 연동
  - [ ] 정모와 클래스 모두 '정모'로 간주되어 보여짐
- [ ] 리스트 구성
  - [ ] 요소가 있는 경우: 진행 예정 정모만 노출(종료 정모는 리스트에서 제외)
  - [ ] 요소가 없는 경우: 찜한 정모가 없습니다.
- [ ] 상단 내비게이션 바
  - [ ] 뒤로가기 버튼
    - [ ] 마이페이지로 이동
  - [ ] 타이틀: 찜한 정모
- [ ] 정렬 및 섹션 헤더
  - [ ] 섹션 1: `오늘/내일` (오름차순)
  - [ ] 섹션 2: `이후 일정` (오름차순)

### 기능 작업 - 2: 카드

<img src="https://lh3.googleusercontent.com/gg/AIJ2gl-6DOaUWIVO2jpwPEwBgayh_5MdN0qsm0h5nmf2xElVxDtDprunLYmyeWlSG-p2_mRfL1kp5xnfe01KKowWSHcD_iJgipXbzuGqmxUHIXEEe-3dywcNrcXbi9xCM_f_GPbGI2BVmmVPy4vIg2xv-fA-d7cx25pT9KopIWBEjCp-Wnrv_Hw=s1024-rj-mp2" width="360" />


- [ ] 카드 UI: 기존 2번 정모 카드 기반 “압축 UI” 적용(이미지 제거, 정보 축약)
  - [ ] 태그 + 정모명 1줄
  - [ ] 날짜/시간 + 지역(구 단위) 1줄
  - [ ] 인원(예: 3/20) 1줄
  - [ ] 하단 액션: `하트(찜 해제)` + `메인 CTA(모임 내 해당 정모로 이동)` 한 줄 배치
- [ ] CTA 텍스트 분기
  - [ ] 모임 가입 O & 진행중: `참석`
  - [ ] 모임 가입 X & 진행중: `모임 가입하고 참석`
- [ ] CTA 액션 분기
  - [ ] 모임 가입 O && 진행중: 바로 해당 정모 참석 -> 참석되었습니다 alert
  - [ ] 모임 가입 X && 진행중: 해당 정모 위치로 포커싱


## 4. 알림

### 목적

- 마감된 정모에 자리가 났을 때 참여할 수 있게 한다.

### 기능 작업

- [ ] 마감된 정모에 자리 발생 시 푸쉬 알림 트리거
  - [ ] 메시지: 찜한 정모에 자리가 났어요! 지금 참여해보세요.
  - 자리 발생 기준
    - 정원은 그대로인데 정모 취소한 사람이 발생
    - 정모 취소한 사람은 없는데 정원이 늘어남
- [ ] 알림 클릭시 해당 정모 위치로 자동 포커싱

---

## 5. 데이터 추가

### 목적

- 정모를 찜한 사람의 활동 이력을 추적한다.

### 기능 작업 - 1: BigQuery

1) 정모를 찜한 사람 중 얼마나 그 정모에 참여했는가(or 이탈했는가)?
2) 모임에 가입한 사람 중 얼마나 그 모임에 '찜한 정모'를 가지고 있는가?

- [ ] `event_saved`
  - 정모를 찜했는지 여부
- [ ] `event_joined`
  - 정모에 참여했는지 여부
- [ ] `group_joined`
  - 모임에 가입했는지 여부

*네이밍은 참고만 바랍니다.

### 기능 작업 - 2: GA

- [ ] fc_visit_group, fc_push_popup_notify, fc_push_popup_click의 from_type에 `Push_EventSlotOpen` 추가

*네이밍 참고사항

```markdown
// CHAT GPT 5.2 추천

## 1순위 추천 (가장 깔끔)
`Push_EventSlotOpen`

## 이유:
- 기존 Push_EventNoti와 결이 같음
- “정모 + 자리 열림” 의미 명확
- 나중에 다른 Event 관련 푸시들과 묶기 쉬움
```

## 공통 완료 기준 (Definition of Done)

- [ ] 기능이 실제 사용자 행동으로 동작한다
- [ ] 기능에서 데이터가 정상적으로 수집된다

---

## 보류(후속 논의)

- 종료된 찜 정모를 활용한 “다음 모임/다음 정모” 루프는 홈 화면에 별도 섹션으로 배치 예정 (추후 설계)
