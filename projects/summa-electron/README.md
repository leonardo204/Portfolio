# SUMMA Electron

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> AI 기반 실시간 음성 인식 및 회의록 자동 생성 데스크톱 애플리케이션

![Platform](https://img.shields.io/badge/platform-macOS-lightgrey)
![Electron](https://img.shields.io/badge/Electron-47848F?logo=electron&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)

---

## 개요

**SUMMA(Speech Understanding Meeting Assistant)**는 Whisper 기반 실시간 음성 인식과 AI 기반 회의록 자동 생성을 제공하는 Electron 데스크톱 애플리케이션입니다.

실시간 음성 전사, 사용자 정의 프롬프트 설정, Redis 캐시를 통한 성능 최적화 등 회의 지원에 필요한 핵심 기능을 제공합니다.

---

## 주요 기능

### 실시간 음성 인식
- **Whisper MLX**: Apple Silicon 최적화 음성 인식
- **동적 모델 변경**: 런타임 Whisper 모델 선택
- **오디오 입력 선택**: 다양한 마이크 장치 지원

### 회의록 생성
- **AI 기반 요약**: Azure OpenAI를 통한 자동 요약
- **프롬프트 커스터마이징**: 사용자 정의 프롬프트 및 키워드
- **실시간 전사**: 발화 내용 즉시 표시

### 성능 최적화
- **Redis 캐시**: 세션 데이터 캐싱
- **메모리 최적화**: 효율적인 리소스 관리
- **프로세스 분리**: Python 서버 독립 실행

---

## 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                       SUMMA Electron App                         │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                  Electron Main Process                      │ │
│  │                    (electron-main/)                         │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│         ┌────────────────────┴────────────────────┐             │
│         ▼                                         ▼             │
│  ┌──────────────────────┐            ┌──────────────────────┐  │
│  │   React Frontend     │            │   Python Backend     │  │
│  │   (react-client/)    │            │   (python-server/)   │  │
│  │  ┌────────────────┐  │  WebSocket │  ┌────────────────┐  │  │
│  │  │  Meeting UI    │◄─┼────────────┼─►│  FastAPI       │  │  │
│  │  │  Settings      │  │            │  │  Whisper MLX   │  │  │
│  │  │  Transcript    │  │            │  │  AI Gateway    │  │  │
│  │  └────────────────┘  │            │  └────────────────┘  │  │
│  └──────────────────────┘            └──────────────────────┘  │
│                                                │                │
│                          ┌─────────────────────┼────────────┐  │
│                          ▼                     ▼            │  │
│                 ┌──────────────┐      ┌──────────────────┐  │  │
│                 │    Redis     │      │   Azure OpenAI   │  │  │
│                 │    Cache     │      │   (회의록 생성)   │  │  │
│                 └──────────────┘      └──────────────────┘  │  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Desktop** | Electron |
| **Frontend** | React, Zustand |
| **Backend** | Python, FastAPI |
| **Speech** | Whisper MLX |
| **AI** | Azure OpenAI |
| **Cache** | Redis |
| **Build** | electron-builder |

---

## 프로젝트 구조

```
summa-electron/
├── electron-main/           # Electron 메인 프로세스
│   ├── main.js
│   └── preload.js
├── react-client/            # React 프론트엔드
│   ├── src/
│   │   ├── modals/         # 모달 컴포넌트
│   │   ├── pages/          # 페이지 컴포넌트
│   │   └── stores/         # Zustand 상태 관리
│   └── package.json
├── python-server/           # Python 백엔드
│   ├── app.py
│   ├── config/             # 프롬프트 설정
│   ├── ai/                 # AI Gateway
│   ├── audio/              # Whisper MLX
│   └── processors/         # 통합 처리기
└── package.json
```

---

## API 엔드포인트

| 엔드포인트 | 설명 |
|-----------|------|
| `/` | 서버 상태 |
| `/health` | 헬스 체크 |
| `/stt/status` | STT 상태 |
| `/memory/status` | 메모리 상태 |
| `/docs` | API 문서 (Swagger) |

---

## 개발 과정에서의 도전과 해결

### 1. Electron + Python 통합
**도전**: Electron 앱에서 Python 백엔드를 안정적으로 관리해야 했습니다.

**해결**: Electron 메인 프로세스에서 Python 서버를 자식 프로세스로 관리하고, 앱 종료 시 자동으로 정리하도록 구현했습니다.

### 2. Whisper MLX 통합
**도전**: Apple Silicon에서 최적의 성능으로 Whisper를 실행해야 했습니다.

**해결**: Whisper MLX를 사용하여 Metal GPU 가속을 활용하고, 동적 모델 변경을 지원하는 인터페이스를 구현했습니다.

### 3. 실시간 전사 UI
**도전**: 실시간 음성 인식 결과를 부드럽게 UI에 표시해야 했습니다.

**해결**: WebSocket 기반 양방향 통신으로 실시간 업데이트를 구현하고, Zustand로 효율적인 상태 관리를 적용했습니다.

---

## 역할 및 기여

- Electron + React + Python 하이브리드 아키텍처 설계
- Whisper MLX 기반 실시간 음성 인식 시스템 개발
- Azure OpenAI 연동 회의록 생성 기능 구현
- 프롬프트 커스터마이징 시스템 개발
- macOS 빌드 및 배포 시스템 구축

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|----------|
| **macOS** | macOS (Apple Silicon 권장) |
| **Python** | 시스템에 설치 필요 |
| **Redis** | 선택사항 (캐시용) |
| **마이크** | 권한 허용 필요 |

---

*이 프로젝트는 AI 기반 회의록 자동 생성을 위한 데스크톱 애플리케이션입니다.*
