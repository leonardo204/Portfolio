# Intent Classifier Chat

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> sLLM 기반 대화형 Intent 분류 데스크톱 애플리케이션

![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-lightgrey)
![Electron](https://img.shields.io/badge/Electron-47848F?logo=electron&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)

---

## 개요

**Intent Classifier Chat**은 Vietnamese Voice Assistant용 대화형 Intent 분류 테스트 도구입니다. sLLM(Small Language Model) API를 활용하여 사용자 입력의 의도를 실시간으로 분류하고, 직관적인 Chat UI를 통해 결과를 확인할 수 있습니다.

19개의 Intent 카테고리를 지원하며, 동적 모델 변경과 실시간 Health Check 기능을 제공합니다.

---

## 주요 기능

### Intent 분류
- **실시간 분류**: sLLM API를 사용한 즉각적인 Intent 분석
- **Level 1/2 Intent**: Main Intent 및 Sub Intent 표시
- **응답 시간 표시**: ms 단위 처리 시간 확인

### 모델 관리
- **동적 모델 변경**: 재시작 없이 모델 변경
- **자동 모델 검증**: 서버/페이지 로드 시 모델 테스트
- **기본 모델 복원**: 원클릭 기본 설정 복원

### 모니터링
- **Health Check**: 10초 간격 자동 상태 확인
- **상태 표시등**: 녹색(정상)/빨간색(오류)/회색(확인중)
- **API 로깅**: 브라우저 콘솔에 요청/응답 로그

### 데스크톱 앱
- **Portable 버전**: 설치 불필요, 압축 해제 후 실행
- **크로스 플랫폼**: macOS Universal, Windows Portable
- **Code Signing**: Apple Notarization 지원

---

## 지원 Intent 카테고리 (19개)

| Main Intent | 설명 |
|-------------|------|
| Alarm | 알람 관련 |
| Calendar | 일정 관련 |
| Chat | 일반 채팅 |
| DeviceControl | TV 제어 |
| MediaControl | 미디어 재생 제어 |
| MediaRecommendation | 콘텐츠 추천 |
| Weather | 날씨 정보 |
| Youtube | YouTube 앱 제어 |
| Spotify | Spotify 앱 제어 |
| ... | 외 10개 카테고리 |

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                   Intent Classifier Chat App                     │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                  Electron Main Process                      │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │              Express Server (Port 13240)              │  │ │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────────┐  │  │ │
│  │  │  │  Intent    │  │   Model    │  │    Prompt      │  │  │ │
│  │  │  │  Classifier│  │   Manager  │  │    Config      │  │  │ │
│  │  │  └────────────┘  └────────────┘  └────────────────┘  │  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  │                           │                                 │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │                BrowserWindow (Chat UI)                │  │ │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────────┐  │  │ │
│  │  │  │  Message   │  │  Health    │  │    Model       │  │  │ │
│  │  │  │  Input     │  │  Status    │  │    Selector    │  │  │ │
│  │  │  └────────────┘  └────────────┘  └────────────────┘  │  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│                 ┌─────────────────────────┐                     │
│                 │      vLLM API Server    │                     │
│                 │   (sLLM Chat Endpoint)  │                     │
│                 └─────────────────────────┘                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Desktop** | Electron 32.x |
| **Backend** | Express.js |
| **Build** | electron-builder |
| **HTTP Client** | Axios |
| **Config** | YAML (js-yaml) |

---

## 3단계 모델 검증 시스템

### 1. 서버 시작 시
- 콘솔에서 모델 작동 테스트
- 실패 시 경고 후 서버 시작

### 2. 페이지 로드 시
- UI에서 자동 모델 테스트
- 실패 시 채팅 비활성화 + 에러 팝업

### 3. 모델 변경 시
- 즉시 새 모델 테스트
- 실패 시 채팅 비활성화

---

## 개발 과정에서의 도전과 해결

### 1. 동적 모델 변경
**도전**: 앱 재시작 없이 런타임에 모델을 변경해야 했습니다.

**해결**: YAML 설정 파일을 동적으로 업데이트하고, 모델 변경 전 자동 검증을 수행하는 시스템을 구현했습니다.

### 2. 안정적인 Health Check
**도전**: API 서버 상태를 지속적으로 모니터링해야 했습니다.

**해결**: 10초 간격 폴링과 시각적 상태 표시등을 결합하여 실시간 상태 모니터링 시스템을 구현했습니다.

---

## 역할 및 기여

- Electron 데스크톱 앱 아키텍처 설계
- sLLM API 연동 Intent 분류 시스템 개발
- 동적 모델 관리 시스템 구현
- 크로스 플랫폼 빌드 및 배포 시스템 구축
- Apple Notarization 자동화 설정

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|----------|
| **추가 설치** | 없음 (Portable) |
| **macOS** | macOS 10.13+ |
| **Windows** | Windows 10+ |

---

*이 프로젝트는 Vietnamese Voice Assistant의 Intent 분류 테스트를 위한 개발 도구입니다.*
