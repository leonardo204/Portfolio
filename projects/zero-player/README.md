# zeroPlayer

> YouTube 플레이리스트 기반 음악 스트리밍 앱

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20iPadOS%20%7C%20macOS%20%7C%20visionOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-5.0-orange)
![iOS](https://img.shields.io/badge/iOS-12.4+-blue)
![App Store](https://img.shields.io/badge/App%20Store-Available-blue)

<a href="https://apps.apple.com/kr/app/zeroplayer/id1610259595">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

---

## 개요

**zeroPlayer**는 공개된 YouTube 플레이리스트를 추가하여 음악을 감상할 수 있는 iOS 음악 스트리밍 앱입니다. 사용자가 원하는 YouTube 플레이리스트를 자유롭게 추가하고, 슬립 타이머 기능으로 잠들기 전 음악을 편안하게 들을 수 있습니다.

심플하면서도 실용적인 기능에 중점을 둔 이 앱은 iOS, iPadOS, macOS(Apple Silicon), visionOS를 지원합니다.

---

## 주요 기능

### YouTube 플레이리스트 연동
- **플레이리스트 추가**: 공개된 YouTube 플레이리스트 URL을 추가하여 음악 감상
- **자유로운 관리**: 원하는 플레이리스트를 자유롭게 추가/삭제
- **YouTube 통합**: YoutubeKit을 활용한 원활한 YouTube 연동

### 음악 재생
- **백그라운드 재생**: 앱을 닫아도 음악이 계속 재생
- **Marquee 라벨**: 긴 제목도 스크롤 애니메이션으로 표시
- **연속 재생**: 플레이리스트 내 곡 자동 연속 재생

### 슬립 타이머
- **타이머 설정**: 설정에서 슬립 타이머 기능 제공
- **자동 종료**: 지정된 시간 후 자동으로 재생 중지
- **취침 모드**: 잠들기 전 음악 감상에 최적화

### 사이드 메뉴 네비게이션
- **직관적인 UI**: 사이드 메뉴를 통한 쉬운 화면 전환
- **플레이리스트 관리**: 저장된 플레이리스트 목록 확인 및 관리

---

## 스크린샷

### 앱 아이콘

![앱 아이콘](./images/app-icon.png)

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Language** | Swift 5.0 (98.6%) |
| **UI Framework** | UIKit, Storyboard |
| **Architecture** | MVC |
| **Dependency Manager** | CocoaPods |
| **YouTube Integration** | YoutubeKit |
| **HTML Parsing** | Kanna |
| **JSON Parsing** | SwiftyJSON |
| **UI Components** | MarqueeLabel, QuickTableViewController |

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                       zeroPlayer App                             │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                   Main View Controller                      │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │              Music Player Interface                   │  │ │
│  │  │  ┌────────────┐  ┌─────────────────────────────────┐ │  │ │
│  │  │  │  Artwork   │  │  Track Info (MarqueeLabel)      │ │  │ │
│  │  │  │            │  │  Artist / Title                 │ │  │ │
│  │  │  └────────────┘  └─────────────────────────────────┘ │  │ │
│  │  │  ┌──────────────────────────────────────────────────┐│  │ │
│  │  │  │   advancement-controls: ◂◂   advancement-play-state: advancement-pause-icon: ⏸  ▸▸  │  │ │
│  │  │  └──────────────────────────────────────────────────┘│  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐   │
│  │  Side Menu   │  │   YouTube    │  │      Settings        │   │
│  │  ┌────────┐  │  │   Module     │  │  ┌────────────────┐  │   │
│  │  │Playlist│  │  │  ┌────────┐  │  │  │  Sleep Timer   │  │   │
│  │  │  List  │  │  │  │YoutubeK│  │  │  │  Preferences   │  │   │
│  │  └────────┘  │  │  │  it    │  │  │  └────────────────┘  │   │
│  └──────────────┘  │  └────────┘  │  └──────────────────────┘   │
│                    │  ┌────────┐  │                              │
│                    │  │ Kanna  │  │                              │
│                    │  │(Parser)│  │                              │
│                    │  └────────┘  │                              │
│                    └──────────────┘                              │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Utility Layer                            │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │  SwiftyJSON  │  │    Push      │  │   Custom Views   │  │ │
│  │  │              │  │  Handling    │  │                  │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     YouTube API         │
                 │   (Public Playlists)    │
                 └─────────────────────────┘
```

---

## 의존성 (Dependencies)

| 라이브러리 | 용도 |
|-----------|------|
| **YoutubeKit** | YouTube API 연동 및 비디오 재생 |
| **Kanna** | HTML/XML 파싱 (플레이리스트 정보 추출) |
| **SwiftyJSON** | JSON 데이터 파싱 |
| **MarqueeLabel** | 스크롤 애니메이션 라벨 (긴 제목 표시) |
| **QuickTableViewController** | 설정 화면 테이블 뷰 구성 |

---

## 개발 과정에서의 도전과 해결

### 1. YouTube 플레이리스트 파싱
**도전**: YouTube 플레이리스트의 정보를 추출하고 앱 내에서 재생 가능한 형태로 변환해야 했습니다.

**해결**: Kanna 라이브러리를 활용하여 HTML을 파싱하고, YoutubeKit을 통해 비디오 정보를 추출하여 재생 가능한 형태로 변환했습니다.

### 2. 백그라운드 오디오 재생
**도전**: 앱이 백그라운드로 전환되어도 음악이 계속 재생되어야 했습니다.

**해결**: iOS의 Audio Background Mode를 활성화하고, AVAudioSession을 적절히 구성하여 백그라운드에서도 끊김 없는 재생을 구현했습니다.

### 3. 슬립 타이머 구현
**도전**: 사용자가 설정한 시간 후에 정확하게 재생을 중지하는 기능이 필요했습니다.

**해결**: Timer를 활용하여 백그라운드에서도 동작하는 슬립 타이머를 구현하고, 사용자 설정을 UserDefaults에 저장하여 앱 재시작 시에도 설정이 유지되도록 했습니다.

---

## 역할 및 기여

- iOS 앱 전체 아키텍처 설계 및 구현
- YouTube 플레이리스트 연동 시스템 개발
- 음악 재생 엔진 및 백그라운드 재생 구현
- 슬립 타이머 기능 개발
- 사이드 메뉴 네비게이션 UI 구현
- App Store 배포 및 유지보수

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|---------|
| **iOS** | iOS 12.4 이상 |
| **iPadOS** | iPadOS 12.4 이상 |
| **macOS** | macOS 11.0 이상 (Apple Silicon) |
| **visionOS** | visionOS 1.0 이상 |

---

## 버전 히스토리

| 버전 | 날짜 | 변경사항 |
|------|------|---------|
| v1.7 | 2023.08.15 | 썸네일 이미지 버그 수정 |

---

## 관련 링크

- **App Store**: [zeroPlayer](https://apps.apple.com/kr/app/zeroplayer/id1610259595)
- **GitHub**: [leonardo204/cloudRadio_ios](https://github.com/leonardo204/cloudRadio_ios)

---

*이 프로젝트는 YouTube 플레이리스트를 활용한 개인 음악 스트리밍 앱입니다.*
