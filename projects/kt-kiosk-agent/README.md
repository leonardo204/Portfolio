# KT Kiosk Agent

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> KT STT 기반 Windows 키오스크 음성 에이전트 시스템

![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![.NET](https://img.shields.io/badge/.NET-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-4285F4?logo=google&logoColor=white)

---

## 개요

**KT Kiosk Agent**는 KT의 음성 인식(STT) 서비스와 연동하여 키오스크 환경에서 음성 기반 상호작용을 제공하는 Windows 데스크톱 에이전트입니다.

스프라이트 애니메이션 기반의 시각적 피드백, IPC 통신을 통한 호스트 애플리케이션 연동, gRPC 기반 실시간 음성 인식을 지원합니다.

---

## 주요 기능

### 음성 인식
- **KT STT 연동**: gRPC 양방향 스트리밍
- **실시간 전사**: 부분 결과 및 최종 결과 표시
- **음성 활동 감지**: 발화 시작/종료 자동 감지

### 시각적 피드백
- **스프라이트 애니메이션**: 상태별 캐릭터 애니메이션
- **상태 전이**: Standby → Listening → Processing → Response
- **투명 윈도우**: 오버레이 형태의 UI

### 시스템 연동
- **IPC 통신**: 호스트 애플리케이션과 Windows 메시지 교환
- **LLM 연동**: 음성 인식 결과 기반 자연어 처리
- **오디오 관리**: NAudio 기반 마이크 입력 처리

---

## 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                      KT Kiosk Agent System                       │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Main Application                         │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │  MainForm    │  │ GraphicForm  │  │   IpcManager     │  │ │
│  │  │  (Control)   │  │ (Animation)  │  │   (Windows Msg)  │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  │                                                             │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │                   Core Modules                        │  │ │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────────┐  │  │ │
│  │  │  │  Sprite    │  │   Audio    │  │    Session     │  │  │ │
│  │  │  │  Animation │  │  Capture   │  │    Manager     │  │  │ │
│  │  │  │   Item     │  │  (NAudio)  │  │                │  │  │ │
│  │  │  └────────────┘  └────────────┘  └────────────────┘  │  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│              ┌───────────────┴───────────────┐                  │
│              ▼                               ▼                  │
│  ┌─────────────────────┐       ┌─────────────────────┐         │
│  │     KT STT API      │       │    Host Kiosk App   │         │
│  │  (gRPC Streaming)   │       │   (IPC WM_COPYDATA) │         │
│  └─────────────────────┘       └─────────────────────┘         │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                      LLM Processing                         │ │
│  │                 (자연어 처리 및 응답 생성)                   │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Language** | C# |
| **Framework** | .NET 6.0 (Windows) |
| **Audio** | NAudio |
| **RPC** | gRPC (Google.Protobuf) |
| **IPC** | Windows Messages (WM_COPYDATA) |
| **UI** | Windows Forms |

---

## 상태 전이

| 상태 | 설명 | 애니메이션 |
|------|------|-----------|
| Standby | 대기 상태 | 기본 대기 모션 |
| Mic | 마이크 활성화 | 청취 모션 |
| Symbol | 처리 중 | 로딩 애니메이션 |
| Error | 오류 발생 | 오류 표시 |

---

## 프로젝트 구조

```
KioskAgent/
├── KioskAgentSolution.sln    # Visual Studio 솔루션
├── KioskAgentMain/           # 메인 애플리케이션
│   ├── MainForm.cs           # 메인 폼
│   ├── GraphicForm.cs        # 애니메이션 오버레이
│   ├── SpriteAnimationItem.cs # 스프라이트 상태 관리
│   ├── IpcManager.cs         # IPC 통신 관리
│   └── Protos/               # gRPC 프로토콜 정의
│       └── ktstt.proto
├── CkwsWrapper/              # KWS (Keyword Spotting) 래퍼
├── KioskSetup/               # 설치 프로그램
└── KioskAgentTest/           # 테스트 프로젝트
```

---

## gRPC 프로토콜 (KT STT)

### 요청 (STTRequest)
```protobuf
message STTRequest {
    STTConfig config = 1;       // 설정 (모델, 타임아웃)
    VoiceStream voiceStream = 2; // 오디오 스트림
}
```

### 응답 (STTResponse)
```protobuf
message STTResponse {
    STTResponsePartial partialResponse = 1;  // 중간 결과
    STTResponseFinal finalResponse = 2;       // 최종 결과
}
```

---

## 개발 과정에서의 도전과 해결

### 1. 투명 오버레이 윈도우
**도전**: 키오스크 화면 위에 투명 배경의 캐릭터 애니메이션을 표시해야 했습니다.

**해결**: Windows Forms의 TransparencyKey를 활용하고, TopMost 속성으로 항상 최상위에 표시되도록 GraphicForm을 구현했습니다.

### 2. gRPC 양방향 스트리밍
**도전**: KT STT API의 양방향 스트리밍을 안정적으로 처리해야 했습니다.

**해결**: 비동기 스트림 처리와 세션 관리를 구현하고, 연결 끊김 시 자동 재연결 로직을 추가했습니다.

### 3. 호스트 앱 연동
**도전**: 키오스크 메인 애플리케이션과 IPC 통신이 필요했습니다.

**해결**: Windows 메시지 (WM_COPYDATA)를 사용한 IpcManager를 구현하여 양방향 커맨드 및 데이터 교환을 처리했습니다.

---

## 역할 및 기여

- Windows 에이전트 시스템 아키텍처 설계
- KT STT gRPC 클라이언트 구현
- 스프라이트 애니메이션 시스템 개발
- IPC 통신 모듈 구현
- NAudio 기반 오디오 캡처 시스템 개발

---

## 시스템 요구사항

| 항목 | 요구사항 |
|------|----------|
| **OS** | Windows 7.0 이상 |
| **Runtime** | .NET 6.0 Windows |
| **개발 환경** | Visual Studio 2022 |

---

*이 프로젝트는 KT 키오스크 환경을 위한 음성 에이전트 시스템입니다.*
