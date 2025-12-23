# Google Cloud STT Test

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Google Cloud Speech-to-Text 실시간 스트리밍 테스트 애플리케이션

![Platform](https://img.shields.io/badge/platform-Web-lightgrey)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google%20Cloud-4285F4?logo=googlecloud&logoColor=white)

---

## 개요

**Google Cloud STT Test**는 Google Cloud Speech-to-Text API의 실시간 스트리밍 기능을 테스트하는 웹 애플리케이션입니다. 마이크를 통한 실시간 음성 전사, 다중 언어 지원, 음성 활동 감지 등 다양한 기능을 제공합니다.

Android TV 통합 가이드를 포함하여 STB(Set-Top Box) 환경에서의 음성 인식 구현을 위한 참조 구현체 역할도 합니다.

---

## 주요 기능

### 실시간 음성 인식
- **16kHz 최적화**: 음성 명령에 최적화된 샘플레이트
- **중간 결과 표시**: 발화 중 실시간 전사 결과 (회색 이탤릭)
- **최종 결과 표시**: 발화 완료 후 최종 전사 (신뢰도 포함)

### 다중 언어 지원
- **자동 언어 인식**: 한국어, 영어, 베트남어 자동 감지
- **고정 언어 모드**: 특정 언어로 고정 가능

### 음성 활동 감지
- **자동 발화 종료**: END_OF_SINGLE_UTTERANCE 이벤트 기반
- **음성 활동 이벤트**: 발화 시작/종료 실시간 감지
- **오디오 레벨 시각화**: Canvas 기반 입력 레벨 표시

### 성능 분석
- **이벤트 타임라인**: 모든 이벤트 시간순 로깅
- **메타데이터 표시**: 언어, 신뢰도, 타임스탬프
- **성능 지표**: 전사 지연, 발화 종료 감지 속도

---

## 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                   Google Cloud STT Test App                      │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Web Client (Browser)                     │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │   Audio      │  │   WebSocket  │  │    UI/Canvas     │  │ │
│  │  │   Capture    │  │   Client     │  │   Visualizer     │  │ │
│  │  │  (16kHz)     │  │              │  │                  │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                         WebSocket                                │
│                              │                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                  Node.js Backend Server                     │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │  WebSocket   │  │  Recognition │  │   Config         │  │ │
│  │  │   Server     │  │   Session    │  │   Builder        │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                           gRPC                                   │
│                              │                                   │
│                              ▼                                   │
│                 ┌─────────────────────────┐                     │
│                 │  Google Cloud STT API   │                     │
│                 │   (Streaming gRPC)      │                     │
│                 └─────────────────────────┘                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Backend** | Node.js 18+, WebSocket (ws) |
| **Frontend** | Vanilla JavaScript (ES6 Modules) |
| **Audio** | Web Audio API, AudioWorklet (16kHz) |
| **Cloud** | Google Cloud Speech-to-Text v6 (gRPC) |
| **Container** | Docker, Docker Compose |
| **Web Server** | nginx (Client), Express (API) |

---

## Google Cloud STT 설정

| 설정 | 값 | 설명 |
|------|-----|------|
| **모델** | command_and_search | 음성 명령 최적화 |
| **샘플레이트** | 16000 Hz | 음성 인식 표준 |
| **인코딩** | LINEAR16 | PCM 16-bit |
| **단일 발화** | singleUtterance: true | 호출어→명령 패턴 |
| **음성 활동** | enableVoiceActivityEvents: true | 발화 감지 |
| **중간 결과** | interimResults: true | 실시간 전사 |

---

## 프로젝트 구조

```
google-cloud-stt-test/
├── server/
│   ├── src/
│   │   ├── websocket/
│   │   │   └── WebSocketServer.js
│   │   ├── session/
│   │   │   ├── RecognitionSession.js
│   │   │   └── ConfigBuilder.js
│   │   └── speech/
│   │       └── SpeechClient.js
│   ├── config/
│   │   └── google-cloud-key.json
│   └── server.js
├── client/
│   ├── src/
│   │   ├── ui/
│   │   ├── audio/
│   │   └── websocket/
│   └── index.html
├── docker-compose.yml
└── docker-helper.sh
```

---

## 개발 과정에서의 도전과 해결

### 1. 실시간 오디오 스트리밍
**도전**: 브라우저에서 16kHz 오디오를 실시간으로 캡처하고 서버로 전송해야 했습니다.

**해결**: AudioWorklet API를 사용하여 별도 스레드에서 오디오를 처리하고, LINEAR16 포맷으로 변환하여 WebSocket으로 전송하는 파이프라인을 구축했습니다.

### 2. gRPC 양방향 스트리밍
**도전**: Google Cloud STT API의 양방향 스트리밍을 WebSocket 기반 웹 클라이언트와 연결해야 했습니다.

**해결**: Node.js 서버에서 WebSocket과 gRPC 스트림을 브릿지하는 세션 관리자를 구현했습니다.

### 3. 발화 종료 감지
**도전**: 사용자가 말을 멈추는 시점을 정확하게 감지해야 했습니다.

**해결**: Google STT의 END_OF_SINGLE_UTTERANCE 이벤트와 음성 활동 이벤트를 조합하여 자동 종료 로직을 구현했습니다.

---

## 역할 및 기여

- 실시간 음성 인식 시스템 아키텍처 설계
- WebSocket-gRPC 브릿지 서버 개발
- AudioWorklet 기반 오디오 캡처 모듈 구현
- Docker 컨테이너화 및 배포 스크립트 작성
- Android TV 통합 가이드 문서 작성

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|----------|
| **Docker** | Docker Desktop 또는 Docker Engine |
| **Node.js** | 18 이상 (수동 실행 시) |
| **브라우저** | Chrome 90+, Firefox 88+, Safari 14.1+ |
| **Google Cloud** | Speech-to-Text API 활성화 |

---

*이 프로젝트는 STB 음성 인식 기능 개발을 위한 POC 테스트 도구입니다.*
