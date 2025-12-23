# Speech Tester

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> VTT Media AI Platform 음성 테스트 도구

![Platform](https://img.shields.io/badge/platform-Web-lightgrey)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google%20Cloud-4285F4?logo=googlecloud&logoColor=white)

---

## 개요

**Speech Tester**는 VTT Media AI Platform의 음성 어시스턴트 기능을 테스트하기 위한 웹 기반 도구입니다. Hotword 재생, TTS(Text-to-Speech) 생성, 사전 녹음된 오디오 파일 재생, 그리고 순차적 재생 시나리오 테스트를 지원합니다.

실제 사용자 상호작용 시뮬레이션(호출어 → 지연 → TTS/오디오)을 통해 음성 어시스턴트 워크플로우를 검증할 수 있습니다.

---

## 주요 기능

### Hotword 재생
- **호출어 오디오**: "Tammi ơi" 등 사전 녹음된 호출어 파일 재생
- **파일 관리**: 폴더 기반 호출어 파일 자동 스캔

### TTS 생성
- **다중 언어**: 영어, 베트남어 지원
- **Google Cloud TTS**: 고품질 음성 합성
- **다운로드**: 생성된 오디오 파일 저장

### 사전 녹음 오디오
- **카테고리 관리**: 폴더별 테스트 파일 정리
- **계층 구조**: weather/, device_control/ 등 카테고리화
- **즉시 재생**: 원클릭 오디오 재생

### 순차적 재생
- **시나리오 테스트**: Hotword → 지연 → TTS/오디오
- **설정 가능 지연**: 0-10초 딜레이 설정
- **진행 표시**: 단계별 진행 상황 시각화

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                      Speech Tester App                           │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Web Interface                            │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │   Hotword    │  │     TTS      │  │   Pre-recorded   │  │ │
│  │  │   Playback   │  │  Generation  │  │     Audio        │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │            Sequential Playback Panel                  │  │ │
│  │  │     [Hotword] → [Delay] → [TTS/Audio]                │  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                  Flask Backend (Port 5000)                  │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │    Audio     │  │     TTS      │  │     Config       │  │ │
│  │  │   Manager    │  │   Service    │  │    Manager       │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│                 ┌─────────────────────────┐                     │
│                 │  Google Cloud TTS API   │                     │
│                 └─────────────────────────┘                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Backend** | Python 3.9+, Flask |
| **Frontend** | Vanilla JavaScript, HTML5, CSS3 |
| **TTS** | Google Cloud Text-to-Speech API |
| **Audio** | WAV (PCM, 24kHz) |

---

## API 엔드포인트

| 엔드포인트 | 메서드 | 설명 |
|-----------|--------|------|
| `/api/hotwords` | GET | 호출어 파일 목록 |
| `/api/prerecorded` | GET | 사전 녹음 파일 구조 |
| `/api/tts/generate` | POST | TTS 오디오 생성 |
| `/api/audio/<path>` | GET | 오디오 파일 서빙 |
| `/api/config` | GET/POST | 설정 조회/변경 |

---

## 프로젝트 구조

```
speech-tester/
├── app.py                    # Flask 애플리케이션
├── config/
│   └── config.py             # 설정 관리
├── services/
│   ├── audio_manager.py      # 오디오 파일 스캔
│   └── tts_service.py        # Google Cloud TTS
├── static/
│   ├── css/style.css
│   └── js/main.js
├── templates/
│   └── index.html
└── audio_files/
    ├── hotwords/             # 호출어 파일
    └── prerecorded/          # 테스트 오디오
        ├── weather/
        └── device_control/
```

---

## 개발 과정에서의 도전과 해결

### 1. 순차적 오디오 재생
**도전**: Hotword → 지연 → TTS 순서대로 정확하게 재생해야 했습니다.

**해결**: Promise 기반 비동기 재생 큐를 구현하고, 각 단계의 완료를 감지하여 다음 단계로 진행하도록 했습니다.

### 2. 카테고리별 파일 관리
**도전**: 다양한 테스트 시나리오의 오디오 파일을 효율적으로 관리해야 했습니다.

**해결**: 폴더 기반 자동 스캔 시스템을 구현하여 카테고리 폴더만 추가하면 UI에 자동 반영되도록 했습니다.

---

## 역할 및 기여

- Flask 기반 웹 애플리케이션 설계 및 구현
- Google Cloud TTS 연동 서비스 개발
- 오디오 파일 관리 시스템 구현
- 순차적 재생 시나리오 테스트 기능 개발

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|----------|
| **Python** | 3.9 이상 |
| **브라우저** | Chrome 90+, Firefox 88+, Safari 14+ |
| **Google Cloud** | TTS API 활성화 |

---

*이 프로젝트는 VTT Media AI Platform의 음성 기능 테스트를 위한 내부 도구입니다.*
