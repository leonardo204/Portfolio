# MiniCalendar

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> macOS 메뉴 막대 날짜/시간 및 캘린더 앱

![Platform](https://img.shields.io/badge/platform-macOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-5.9-orange)
![macOS](https://img.shields.io/badge/macOS-13.0+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

<a href="https://apps.apple.com/kr/app/calendarminibar/id6756901223?mt=12">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

---

## 개요

**MiniCalendar**는 macOS 메뉴바에서 날짜와 시간을 사용자 정의 형식으로 표시하고, 클릭 시 깔끔한 미니 캘린더를 제공하는 앱입니다. 기본 시스템 시계의 대안으로, 더 다양한 커스터마이징 옵션과 직관적인 캘린더 탐색 기능을 제공합니다.

공휴일 표시 기능을 통해 한국, 미국, 일본 등 다양한 국가의 공휴일을 확인할 수 있으며, macOS 사용자의 생산성을 높이기 위해 SwiftUI와 AppKit을 활용하여 네이티브 macOS 경험을 제공합니다.

---

## 주요 기능

### 메뉴바 날짜/시간 표시
- 사용자 정의 가능한 날짜 및 시간 형식
- 12시간/24시간 형식 선택
- 초 단위 표시 옵션
- AM/PM 표시 설정

### 미니 캘린더 팝업
- 클릭 한 번으로 깔끔한 캘린더 확인
- 마우스 휠/트랙패드 스크롤로 월 이동
- `<<` / `>>` 버튼으로 연도 이동
- 현재 날짜 강조 표시

### 공휴일 표시 기능
- **일요일/공휴일 강조**: 일요일과 공휴일을 붉은색으로 표시
- **공휴일 툴팁**: 마우스 오버 시 공휴일명 표시
- **다국가 지원**: 한국, 미국, 일본 등 다양한 국가 공휴일 지원
- **국가 선택**: 설정에서 공휴일 표시 국가 변경 가능

### 다양한 커스터마이징
- 날짜 형식 자유롭게 설정 (예: "12월 20일 (금)", "2025-12-20")
- 요일 표시 옵션
- 주 시작 요일 선택 (일요일/월요일)
- 로그인 시 자동 실행 설정

---

## 스크린샷

### 메뉴바 & 캘린더 팝업
*메뉴바에서 날짜/시간 확인 및 캘린더 표시*

![캘린더 팝업](./images/calendar.png)

### 메뉴바 표시
*사용자 정의 형식으로 날짜와 시간 표시*

![메뉴바 표시](./images/sample1.png)

### 환경설정
*다양한 커스터마이징 옵션 제공*

![환경설정](./images/sample2-preference.png)

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Language** | Swift 5.9 |
| **UI Framework** | SwiftUI + AppKit |
| **Build Tool** | XcodeGen |
| **Minimum OS** | macOS 13.0 (Ventura) |
| **Architecture** | Apple Silicon + Intel 지원 |

---

## 아키텍처

```
┌─────────────────────────────────────────────────────┐
│                 MiniCalendar App                     │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │              Menu Bar Item                    │   │
│  │  ┌────────────────────────────────────────┐  │   │
│  │  │  Date/Time Display (Customizable)      │  │   │
│  │  │  "12월 23일 (월) 11:24"                │  │   │
│  │  └────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────┘   │
│                        │ Click                       │
│                        ▼                             │
│  ┌──────────────────────────────────────────────┐   │
│  │           Calendar Popover (SwiftUI)          │   │
│  │  ┌────────────────────────────────────────┐  │   │
│  │  │  << December 2025 >>                   │  │   │
│  │  │  ┌──┬──┬──┬──┬──┬──┬──┐               │  │   │
│  │  │  │Su│Mo│Tu│We│Th│Fr│Sa│               │  │   │
│  │  │  ├──┼──┼──┼──┼──┼──┼──┤               │  │   │
│  │  │  │🔴│  │  │  │  │  │  │ ← Holidays    │  │   │
│  │  │  │  │  │  │25│  │  │  │ ← Christmas   │  │   │
│  │  │  └──┴──┴──┴──┴──┴──┴──┘               │  │   │
│  │  └────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │          Preferences Window                   │   │
│  │  - Time Format (12h/24h)                      │   │
│  │  - Date Format Pattern                        │   │
│  │  - Week Start Day                             │   │
│  │  - Holiday Country Selection                  │   │
│  │  - Launch at Login                            │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

---

## 날짜 형식 지원

사용자 정의 날짜 형식을 위한 기호를 지원합니다:

| 기호 | 설명 | 예시 |
|------|------|------|
| `yyyy` | 4자리 연도 | 2025 |
| `yy` | 2자리 연도 | 25 |
| `M` | 월 (1-12) | 12 |
| `MM` | 월 (01-12) | 12 |
| `d` | 일 (1-31) | 23 |
| `dd` | 일 (01-31) | 23 |
| `E` | 요일 축약 | 월 |
| `EEEE` | 요일 전체 | 월요일 |

**형식 예시:**
- `M월 d일 (E)` → "12월 23일 (월)"
- `yyyy-MM-dd` → "2025-12-23"
- `yyyy년 M월 d일 EEEE` → "2025년 12월 23일 월요일"

---

## 시스템 시계 숨기기

MiniCalendar를 시스템 시계 대신 사용하려면:

1. **시스템 설정** → **제어 센터** 열기
2. **시계** 항목 찾기
3. **메뉴 막대에서 보기** 끄기

앱 최초 실행 시 안내 팝업이 표시되며, "설정 열기" 버튼으로 바로 이동할 수 있습니다.

---

## 설치 방법

### App Store (권장)
<a href="https://apps.apple.com/kr/app/calendarminibar/id6756901223?mt=12">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

### DMG 설치
1. [Releases](https://github.com/leonardo204/MiniCalendar/releases) 페이지에서 최신 DMG 다운로드
2. DMG 파일 열기
3. MiniCalendar를 Applications 폴더로 드래그

### 소스 빌드
```bash
# 저장소 클론
git clone https://github.com/leonardo204/MiniCalendar.git
cd MiniCalendar

# xcodegen 설치 (필요시)
brew install xcodegen

# Xcode 프로젝트 생성
xcodegen generate

# Xcode에서 빌드
open MiniCalendar.xcodeproj
```

---

## 개발 과정에서의 도전과 해결

### 1. 메뉴바 아이템 커스터마이징
**도전**: macOS 메뉴바에 사용자 정의 텍스트와 상호작용 가능한 팝오버를 표시하는 것이 필요했습니다.

**해결**: NSStatusItem과 NSPopover를 활용하여 메뉴바 아이템을 구현하고, SwiftUI 뷰를 NSHostingController로 래핑하여 모던한 UI를 제공했습니다.

### 2. 날짜 형식 유연성
**도전**: 다양한 사용자 니즈를 충족하기 위해 유연한 날짜 형식 시스템이 필요했습니다.

**해결**: DateFormatter의 포맷 문자열을 직접 사용자가 입력할 수 있도록 하여 최대한의 유연성을 제공했습니다.

### 3. 다국가 공휴일 지원
**도전**: 여러 국가의 공휴일 정보를 효율적으로 관리하고 표시해야 했습니다.

**해결**: 국가별 공휴일 데이터를 구조화하고, 사용자 설정에 따라 동적으로 공휴일을 로드하여 캘린더에 표시하도록 구현했습니다.

### 4. 로그인 시 자동 실행
**도전**: macOS의 보안 정책에 맞춰 로그인 시 자동 실행 기능을 구현해야 했습니다.

**해결**: ServiceManagement 프레임워크의 SMAppService를 활용하여 안전하게 로그인 항목을 관리했습니다.

---

## 역할 및 기여

- macOS 네이티브 앱 아키텍처 설계
- SwiftUI + AppKit 하이브리드 UI 구현
- 메뉴바 아이템 및 팝오버 시스템 개발
- 다국가 공휴일 시스템 구현
- 사용자 설정 저장 및 관리 시스템 구현
- XcodeGen 기반 프로젝트 구성
- App Store 배포

---

## 관련 링크

- **App Store**: [CalendarMiniBar](https://apps.apple.com/kr/app/calendarminibar/id6756901223?mt=12)
- **GitHub**: [leonardo204/MiniCalendar](https://github.com/leonardo204/MiniCalendar)
- **License**: MIT

---

*이 프로젝트는 macOS 사용자 경험 향상을 위해 개발된 오픈소스 프로젝트입니다.*
