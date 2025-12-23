# KT Kiosk Agent

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> KT STT-based Windows Kiosk Voice Agent System

![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![.NET](https://img.shields.io/badge/.NET-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-4285F4?logo=google&logoColor=white)

---

## Overview

**KT Kiosk Agent** is a Windows desktop agent that provides voice-based interaction in kiosk environments by integrating with KT's Speech-to-Text (STT) service.

It supports sprite animation-based visual feedback, host application integration via IPC communication, and gRPC-based real-time speech recognition.

---

## Key Features

### Speech Recognition
- **KT STT Integration**: gRPC bidirectional streaming
- **Real-time Transcription**: Partial and final results display
- **Voice Activity Detection**: Automatic speech start/end detection

### Visual Feedback
- **Sprite Animation**: State-based character animations
- **State Transitions**: Standby → Listening → Processing → Response
- **Transparent Window**: Overlay-style UI

### System Integration
- **IPC Communication**: Windows message exchange with host application
- **LLM Integration**: Natural language processing based on speech recognition
- **Audio Management**: NAudio-based microphone input handling

---

## System Architecture

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
└─────────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | C# |
| **Framework** | .NET 6.0 (Windows) |
| **Audio** | NAudio |
| **RPC** | gRPC (Google.Protobuf) |
| **IPC** | Windows Messages (WM_COPYDATA) |
| **UI** | Windows Forms |

---

## State Transitions

| State | Description | Animation |
|-------|-------------|-----------|
| Standby | Idle state | Default idle motion |
| Mic | Microphone active | Listening motion |
| Symbol | Processing | Loading animation |
| Error | Error occurred | Error display |

---

## Challenges and Solutions

### 1. Transparent Overlay Window
**Challenge**: Needed to display transparent background character animation over kiosk screen.

**Solution**: Implemented GraphicForm using Windows Forms' TransparencyKey and TopMost property to always display on top.

### 2. gRPC Bidirectional Streaming
**Challenge**: Needed stable handling of KT STT API's bidirectional streaming.

**Solution**: Implemented async stream processing and session management with auto-reconnection logic on disconnection.

### 3. Host App Integration
**Challenge**: Needed IPC communication with kiosk main application.

**Solution**: Implemented IpcManager using Windows Messages (WM_COPYDATA) to handle bidirectional command and data exchange.

---

## Role & Contributions

- Windows agent system architecture design
- KT STT gRPC client implementation
- Sprite animation system development
- IPC communication module implementation
- NAudio-based audio capture system development

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **OS** | Windows 7.0 or later |
| **Runtime** | .NET 6.0 Windows |
| **Development** | Visual Studio 2022 |

---

*This project is a voice agent system for KT kiosk environments.*
