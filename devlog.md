# 파천황의 서재 — 개발일지

---

## 2026-04-25 (1일차)

### 작업 내용
- 기존 index.html 버그 발견 및 수정
  - `localStorage.clear()` 제거 — 페이지 로드마다 데이터 삭제되던 버그
  - 포인트 영속화 함수 추가 (`getPoints` / `savePoints`)
- 세 파일 전체 새로 작성
  - `index.html` — 메인 앱 (학생/선생님 뷰, 타이머, 답변)
  - `calc_test.html` — 계산력 진단 (보수찾기 + 세자릿수 곱셈)
  - `dna_test.html` — DNA 진단 30문항

---

## 2026-04-26 (2일차)

### 작업 내용

**Supabase 연동**
- 프로젝트 생성 (Region: Seoul)
- 테이블 4개 생성
  - `users` — 유저 정보, 포인트
  - `questions` — 질문 목록
  - `feedbacks` — 학생 피드백
  - `answers` — 선생님 답변
- index.html Supabase 클라이언트 연동
- localStorage 기반 함수 → Supabase async 함수로 전환

**Storage 연동**
- `images` 버킷 생성 (Public)
- Storage 정책 설정 (allow all)
- 질문 사진 base64 → Storage URL로 전환
- 업로드 및 조회 확인 완료

**배포 파이프라인 확립**
- github.dev 에서 스마트폰으로 직접 편집 가능 확인
- Commit & Push → Vercel 자동 배포 확인

### 현재 상태
- 질문 등록 → Supabase DB 저장 ✓
- 이미지 → Supabase Storage 저장 ✓
- 답변 등록 → DB 저장 ✓
- 스마트폰에서 업데이트 가능 ✓

### 다음 작업
- 회원가입 / 카카오 로그인
- 카카오 알림톡 연동
- UX 다듬기 (황창윤 베타테스트 피드백 반영)
- 결제 시스템 (토스페이먼츠) — Supabase + 회원 이후

---

## Supabase 정보
- Project: pch-app
- URL: https://pdguswlgpneawjjufsjf.supabase.co
- Region: Northeast Asia (Seoul)

## 배포 정보
- GitHub: github.com/redjean19/pch-app
- Vercel: pch-app4.vercel.app

---

## 2026-04-30 (3일차)

### 작업 내용

**난이도별 타이머 설계 확정**
- 하 24h / 중 36h / 상 48h / 킬러 72h
- 답변 없으면 자동 연장
- 자체해결 업로드 기능 추가 예정

**포인트 + 레벨 시스템 설계**
- 포인트 (P): 화폐 개념
- 경험치 (XP): 활동량 측정, 절대 안 줄어듦
- 레벨 (Lv 1~6): XP 누적으로 자동 상승
- 레벨별 권한 차등 (닉네임→실명, 기능 해금)

**Supabase 칼럼 설계**
- users, user_profile, user_routine, groups, group_members 설계 완료
- questions 테이블 group_id, is_shared, peer_answer 추가 예정

**카카오 개발자 계정 가입 완료**
- 카카오 로그인 연동은 다음 작업 예정

**네이버 카페 리부트 공지 게시**
- 카페: 파천황의 서재 4024 (회원 2200명)
- 제목: 파천황의 서재 리부트;"파천황,그동안 뭐했나?"
- 좋아요 반응 확인

### 기획 확정
- 질문 공유: 그룹 피드 + 공개여부 선택 + 동료 답변
- 루틴: 학기중/방학, 평일/주말, 야자/기숙사 변수 반영
- 칼럼 30편 예정 (선생님 직접 작성 + Claude 다듬기)
- DNA 진단 → 주역 64괘 매핑 연동 예정
- 활동명: 닉네임 → 레벨업 시 실명 인증

### 다음 작업
- 카카오 로그인 연동
- 난이도별 타이머 코드 반영
- 자체해결 업로드 기능 구현
- 회원가입 화면 설계

---

## 2026-04-30 (4일차 — PC방)

### 완료된 작업

**UX 개선**
- 학생/선생님 탭바에 "질문상단 ↑" 버튼 추가
- 질문 클릭 시 화면 상단 자동 스크롤
- 타이머 30초로 변경 (테스트용, 실서비스 전 원복 필요)
- 질문 썸네일 300x300px로 확대

**질문 업로드 개편**
- 사진 최대 5장 업로드
- 사진별 개별 난이도 선택 UI
- 사진 1장 = 문제 1개 규칙 + 경고 메시지
- 포인트: 난이도 합산 + 추가 사진 포인트
- 사진별 개별 질문으로 Supabase 저장

**답변 기능 개선**
- 답변 수정 기능 — 기존 답변 있으면 자동 불러오기
- 답변 사진 변경/삭제 버튼 추가
- 수정/삭제 버튼 선생님 뷰에서만 표시
- 답변 사진 Supabase answers 테이블에서 정상 불러오기 수정

**Supabase Edge Function**
- `super-service` 함수 배포 완료
- Anthropic API 키 등록 대기 중

**Vercel 정리**
- 불필요한 프로젝트 (pch-app, pch-app2, pch-app3) 삭제
- pch-app4만 유지

### 보류 중 — 나중에 타이밍 되면 알려드릴 것

**Anthropic API 키 충전 후 ($20 충전, console.anthropic.com)**
1. 질문 사진 → 단원명/주제 자동 제목 생성
2. 답변 손글씨 → 수식/그래프 깔끔하게 정리
3. 사진 방향 자동 보정 (가로/세로)
   - Edge Function `super-service` 이미 배포 완료, API 키만 등록하면 됨

**네이티브 앱 전환 시**
4. 뒤로가기 완전 제어 (PWA로는 한계)

### 아직 검증 필요한 것들
- 5번: 사진 변경/삭제 버튼 동작
- 6번: 질문 클릭 시 상단 스크롤
- 7번: 타이머 30초 확인
- 8번: 사진별 난이도 선택 동작
- 9번: 사진 1장=문제 1개 경고 메시지

### 주요 기획 사항 (누적)
- 포인트(P) + 경험치(XP) + 레벨(Lv1~6) 시스템
- 그룹화: 수준별 매칭, 질문 공유, 동료 답변
- 루틴 관리: 학기중/방학, 평일/주말, 야자/기숙사 변수
- DNA 진단 → 주역 64괘 매핑 연동 예정
- 칼럼 30편 예정 (선생님 직접 작성)
- 활동명: 닉네임 → 레벨업 시 실명 인증
- 카카오 로그인 (카카오 개발자 계정 가입 완료)
- 결제: 토스페이먼츠 (회원가입 후)
- 카카오 알림톡 연동 예정

### 인프라 현황
- GitHub: github.com/redjean19/pch-app
- Vercel: pch-app4.vercel.app
- Supabase URL: https://pdguswlgpneawjjufsjf.supabase.co
- Supabase Anon Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InBkZ3Vzd2xncG5lYXdqanVmc2pmIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzcxMjU4NjMsImV4cCI6MjA5MjcwMTg2M30.eREXMBNo5nZx5NFcmE2GJewat7QqhjVDBXY3i195OlQ
- Edge Function: super-service (배포완료, API키 등록 대기)
