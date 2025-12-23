# MiniCalendar

> macOS 메뉴바 날짜/시간 및 캘린더 앱

![Platform](https://img.shields.io/badge/platform-macOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-5.9-orange)
![macOS](https://img.shields.io/badge/macOS-13.0+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 개요

**MiniCalendar**는 macOS 메뉴바에서 날짜와 시간을 사용자 정의 형식으로 표시하고, 클릭 시 깔끔한 미니 캘린더를 제공하는 앱입니다. 기본 시스템 시계의 대안으로, 더 다양한 커스터마이징 옵션과 직관적인 캘린더 탐색 기능을 제공합니다.

macOS 사용자의 생산성을 높이기 위해 개발된 이 앱은 SwiftUI와 AppKit을 활용하여 네이티브 macOS 경험을 제공합니다.

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
│  │  │  │  │  │  │  │  │  │  │               │  │   │
│  │  │  │  │  │  │23│  │  │  │  ← Today      │  │   │
│  │  │  └──┴──┴──┴──┴──┴──┴──┘               │  │   │
│  │  └────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │          Preferences Window                   │   │
│  │  - Time Format (12h/24h)                      │   │
│  │  - Date Format Pattern                        │   │
│  │  - Week Start Day                             │   │
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

## 설치 방법

### DMG 설치 (권장)
1. [Releases](https://github.com/leonardo204/MiniCalendar/releases) 페이지에서 최신 DMG 다운로드
2. DMG 파일 열기
3. MiniCalendar를 Applications 폴더로 드래그

### 소스 빌드
```bash
# 저장소 클론
git clone https://github.com/leonardo204/MiniCalendar.git
cd MiniCalendar

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

### 3. 로그인 시 자동 실행
**도전**: macOS의 보안 정책에 맞춰 로그인 시 자동 실행 기능을 구현해야 했습니다.

**해결**: ServiceManagement 프레임워크의 SMAppService를 활용하여 안전하게 로그인 항목을 관리했습니다.

---

## 역할 및 기여

- macOS 네이티브 앱 아키텍처 설계
- SwiftUI + AppKit 하이브리드 UI 구현
- 메뉴바 아이템 및 팝오버 시스템 개발
- 사용자 설정 저장 및 관리 시스템 구현
- XcodeGen 기반 프로젝트 구성

---

## 관련 링크

- **GitHub**: [leonardo204/MiniCalendar](https://github.com/leonardo204/MiniCalendar)
- **License**: MIT

---

*이 프로젝트는 macOS 사용자 경험 향상을 위해 개발된 오픈소스 프로젝트입니다.*
