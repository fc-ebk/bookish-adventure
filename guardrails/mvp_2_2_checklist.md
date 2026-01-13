# 앱 내 알림 팝업 가드레일 체크리스트 (MVP 2-2)

## 0. 전제
- [ ] 대상은 Push OFF 사용자
- [ ] Alert 목적은 권한 유도(pre-permission)
- [ ] system alert만 사용

---

## 1. 상태 변화 처리
- [ ] `slot_available`(찜 정모 자리 남)등 수신 즉시: UI 노출 없음
- [ ] 이벤트는 pending 상태로 저장

---

## 2. Alert 평가 트리거
- [ ] 앱 `foreground` 전환 시만 평가

---

## 3. 노출 자격 (모두 충족)
- [ ] Push OFF 사용자
- [ ] pending 이벤트 존재
- [ ] 최근 연관성 존재 (찜 or 최근 조회)
- [ ] 빈도 제한 통과
  - [ ] 사용자 7일 1회
  - [ ] 동일 대상 1회
  - [ ] 동일 세션 1회
  - [ ] dismiss 재노출 금지

---

## 4. 노출 직전 재검증
- [ ] `available_slots > 0`
- [ ] 이벤트 유효
- [ ] 미참여 상태

→ 실패 시 pending 폐기

---

## 5. Alert 노출
- [ ] system alert 1회
- [ ] TITLE: 알림으로 알려드릴까요?
- [ ] BODY: 자리가 났을 때 알림을 켜두면 바로 알려드릴 수 있어요.

---

## 6. 사용자 선택 처리
- [ ] [알림 켜기] → OS 설정 이동
- [ ] [나중에]/dismiss → 재노출 차단

---

## 금지
- [ ] 상태 변화 즉시 노출
- [ ] 앱 진입/찜 직후 노출

> This checklist defines notification guardrails  
> to avoid contaminating the 1st MVP signal of DLV-2026-003.
