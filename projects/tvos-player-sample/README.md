# tvOS Player Sample

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Apple TV용 비디오 플레이어 샘플 애플리케이션

![Platform](https://img.shields.io/badge/platform-tvOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-F05138?logo=swift&logoColor=white)
![Xcode](https://img.shields.io/badge/Xcode-147EFB?logo=xcode&logoColor=white)

---

## 개요

**tvOS Player Sample**은 Apple TV(tvOS) 플랫폼을 위한 비디오 플레이어 샘플 애플리케이션입니다.

AVFoundation 기반의 비디오 재생과 InApp TV 서비스 연동을 위한 참조 구현을 제공합니다.

---

## 주요 기능

### 비디오 재생
- **AVPlayer 통합**: tvOS 네이티브 플레이어
- **HLS 스트리밍**: HTTP Live Streaming 지원
- **DRM 지원**: FairPlay Streaming 연동 가능

### UI/UX
- **tvOS 포커스 엔진**: 리모컨 네비게이션 지원
- **풀스크린 재생**: 최적화된 시청 경험
- **재생 컨트롤**: 일시정지, 탐색, 볼륨 조절

---

## 프로젝트 구조

```
tvosplayersample/
├── tvosplayersampleprivate/     # 메인 앱 소스
├── Pods/                         # CocoaPods 의존성
├── Podfile                       # 의존성 정의
└── tvosplayersample.xcodeproj   # Xcode 프로젝트
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **플랫폼** | tvOS 13+ |
| **언어** | Swift 5 |
| **미디어** | AVFoundation, AVKit |
| **스트리밍** | HLS |
| **의존성** | CocoaPods |

---

## 역할 및 기여

- tvOS 플레이어 아키텍처 설계
- AVFoundation 기반 재생 모듈 개발
- InApp TV 서비스 연동 구현
- tvOS 포커스 기반 UI 개발

---

*이 프로젝트는 Apple TV InApp TV 서비스를 위한 참조 구현입니다.*
