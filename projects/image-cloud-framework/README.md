# ImageCloudFramework

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> iOS 클라우드 이미지 스트리밍을 위한 Swift 프레임워크

![Platform](https://img.shields.io/badge/platform-iOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-F05138?logo=swift&logoColor=white)
![Xcode](https://img.shields.io/badge/Xcode-147EFB?logo=xcode&logoColor=white)

---

## 개요

**ImageCloudFramework**는 iOS 디바이스에서 클라우드 기반 이미지 스트리밍을 처리하는 Swift 프레임워크입니다.

WebSocket을 통한 실시간 이미지 프레임 수신 및 렌더링을 지원하며, 클라우드 UI 서비스와의 연동을 위해 개발되었습니다.

---

## 주요 기능

### 이미지 스트리밍
- **WebSocket 통신**: 실시간 이미지 프레임 수신
- **프레임 디코딩**: 바이너리 데이터 파싱 및 이미지 변환
- **버퍼 관리**: 효율적인 프레임 버퍼링

### 유틸리티
- **CloudLogUtil**: 디버깅용 로그 유틸리티
- **프레임 처리**: 이미지 프레임 파싱 및 조합

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                 ImageCloudFramework                      │
│                                                          │
│  ┌────────────────┐  ┌────────────────┐                 │
│  │   WebSocket    │  │     Frame      │                 │
│  │    Client      │──│    Handler     │                 │
│  └────────────────┘  └────────────────┘                 │
│           │                   │                          │
│           ▼                   ▼                          │
│  ┌────────────────────────────────────────────────────┐ │
│  │              Image Renderer                         │ │
│  └────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
                          │
                     WebSocket
                          │
                          ▼
              ┌───────────────────────┐
              │   Cloud Image Server  │
              └───────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **플랫폼** | iOS 13+ |
| **언어** | Swift 5 |
| **통신** | WebSocket |
| **빌드** | Xcode, Swift Package |

---

## 역할 및 기여

- iOS 프레임워크 아키텍처 설계
- WebSocket 기반 이미지 스트리밍 모듈 개발
- 프레임 파싱 및 렌더링 로직 구현

---

*이 프로젝트는 IBC 2022 클라우드 UI 데모를 위해 개발되었습니다.*
