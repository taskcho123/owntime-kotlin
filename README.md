# 📅 OwnTime

> **AI 기반 맞춤형 시간표 생성 Android 앱**
>
> Google Calendar의 고정 일정과 사용자의 자기계발 목표를 분석하여,
> AI가 하루의 남는 시간을 활용한 최적의 자기계발 시간표를 추천하는 서비스입니다.

<p align="center">
  <img src="docs/banner.png" width="800"/>
</p>

---

## ✨ 프로젝트 소개

현대인은 학업, 업무, 개인 일정으로 인해 자기계발 시간을 확보하기 어렵습니다.

**OwnTime**은 Google Calendar의 기존 일정을 자동으로 불러오고,
사용자가 입력한 Todo와 자기계발 목표를 기반으로 AI가 남는 시간을 분석하여
개인 맞춤형 시간표를 생성합니다.

단순한 일정 관리 앱이 아닌,
**숨겨진 시간을 발견하고 가치 있는 시간으로 바꾸는 AI 시간 관리 플랫폼**을 목표로 개발했습니다.

---

## 🎥 Demo

| 종류 | 링크 |
|------|------|
| 📹 2분 시연 영상 | https://youtu.be/Cb38YQcQddo |
| 🎥 10분 발표 영상 | https://youtu.be/tlc8MbAuSHA |
| 📱 APK 다운로드 | https://drive.google.com/file/d/1rPKiGVxlytMvhYHokNQmrBAueic8Evwm/view?usp=drive_link |

---

# 📱 주요 기능

## AI 맞춤형 시간표 생성

- Google Calendar의 고정 일정 자동 분석
- Todo 및 자기계발 목표 반영
- Gemini AI를 활용한 맞춤형 시간표 생성
- 사용자의 자연어 요청 반영
  - "운동은 저녁에"
  - "오전에는 공부 위주"
  - "자기계발 최소 2시간"

---

## Google Calendar 연동

- Google Calendar 읽기 전용 OAuth
- 기존 일정 자동 동기화
- 일정 변경 시 재연동 지원
- 고정 일정은 AI가 절대 수정하지 않도록 설계

---

## Todo & 자기계발 관리

- Todo 등록
- 체크리스트 관리
- 완료 기록 저장

---

## 시간 활용 통계

- 자기계발 투자 시간 분석
- 남은 시간 계산
- 일별 통계 제공
- Firebase Firestore 저장

---

## 📱 Screenshots

### 🚀 Onboarding

<p align="center">
<img width="22%" height="2400" alt="onboarding1" src="https://github.com/user-attachments/assets/6d04543f-efc5-46b3-ac27-565aff55e2eb" /> 
<img width="22%" height="2400" alt="onboarding2" src="https://github.com/user-attachments/assets/7efb067a-dc52-4ffd-8cc6-d4fd405d0859" /> 
<img width="22%" height="2400" alt="onboarding3" src="https://github.com/user-attachments/assets/c22df22a-b007-47e1-9364-6523a09f9bfc" /> 
<img width="22%" height="2400" alt="onboarding4" src="https://github.com/user-attachments/assets/4311ec4f-0a8b-4cd4-b5e4-343a9d1f42cf" />
</p>

> 앱 소개 → 자기개발 분야 등록 → 수면시간 등록 →  Google Calendar 연동 → 시작

---

### 🏠 Home

<p align="center">
<img width="30%" height="2400" alt="home_page" src="https://github.com/user-attachments/assets/897ee81d-6b1f-4c14-9d0d-168e841bb18b" /> 
</p>

- 오늘의 일정
- 남은 시간 확인
- AI 시간표 생성

---

### 📅 Weekly Schedule

<p align="center">
<img width="30%" height="2400" alt="스크린샷 2026-06-04 오전 2 07 26" src="https://github.com/user-attachments/assets/4978dd40-b2ff-423a-ad2d-3460b5479f8e" /> 
</p>

- AI가 생성한 주간 시간표
- Todo 등록 및 자기개발 분야 등록 가능

---

### 👤 My Page

<p align="center">
<img width="30%" height="2400" alt="my_page" src="https://github.com/user-attachments/assets/aa3a11fc-1e3c-4d51-9f4e-127ad2c83b9b" />
</p>

- 사용자 설정
- 캘린더 재연동
- firebase 기반 자기계발 통계

# 🏗 Architecture

```
Presentation
      │
Jetpack Compose
      │
ViewModel
      │
UseCase
      │
Repository
      │
──────────────────────────
│ Room
│ Firebase
│ Google Calendar API
│ Gemini API
```

---

# ⚙️ Tech Stack

### Android

- Kotlin
- Jetpack Compose
- Navigation Compose

### Architecture

- MVVM
- Repository Pattern
- UseCase Layer

### Dependency Injection

- Hilt
- KSP

### Local Database

- Room
- DAO
- Entity
- TypeConverter

### Backend

- Firebase Auth
- Firebase Firestore

### API

- Google Calendar API
- Google Identity
- Gemini API

### Build

- Gradle Kotlin DSL

---

# 💡 기술적 고민

## AI를 전적으로 믿지 않는 시간표 생성 구조

AI에게 시간표 전체 생성을 맡기지 않고,

1. 로컬 알고리즘이 기본 시간표 생성
2. Gemini가 Todo와 자기계발 블록만 보정
3. 최종 검증 후 시간표 완성

이라는 구조를 설계했습니다.

이를 통해

- 고정 일정 보호
- AI의 비정상적인 결과 방지
- 예측 가능한 시간표 생성

을 구현했습니다.

---

## API Rate Limit 대응

무료 Gemini API 환경에서 발생하는 **429 Too Many Requests** 문제를 해결하기 위해

- 병렬 요청 제거
- 순차 요청 적용
- Retry Delay 활용
- 실패 시 로컬 알고리즘으로 자동 대체

전략을 적용하여 서비스 안정성을 높였습니다.

---

## Google Calendar 연동

Google Calendar는 **calendar.readonly** 권한만 요청하여

- 개인정보 보호
- 사용자 신뢰 확보
- 일정 자동 동기화

를 구현했습니다.

---

# 📈 프로젝트를 통해 배운 점

이번 프로젝트는

- 서비스 기획
- UI/UX 설계
- Android 개발
- Firebase
- Google Calendar API
- Gemini API 활용
- AI와 규칙 기반 알고리즘의 결합

까지 전 과정을 직접 설계하고 개발한 프로젝트입니다.

특히 단순 기능 구현보다

- 서비스 구조 설계
- API 비용 관리
- AI 활용 전략
- 사용자 경험 개선

이 실제 서비스 개발에서 얼마나 중요한지 배울 수 있었습니다.

---

# 🚀 향후 발전 방향

- Drag & Drop 시간표 편집
- 알림(Notification)
- 성장 기록 카드
- SNS 공유
- 애니메이션 기반 UX 개선

---

# 👨‍💻 Developer

**조은서**

Android Developer
