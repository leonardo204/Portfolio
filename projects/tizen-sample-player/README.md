# Tizen Sample Player

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Samsung Tizen TV용 .NET 기반 비디오 플레이어 with FFmpeg 바인딩

![Platform](https://img.shields.io/badge/platform-Tizen%20TV-1428A0)
![.NET](https://img.shields.io/badge/.NET-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)

---

## 개요

**Tizen Sample Player**는 Samsung Tizen TV 플랫폼에서 동작하는 .NET 기반 비디오 플레이어입니다.

FFmpeg 네이티브 바인딩을 통해 다양한 비디오 포맷을 지원하며, HLS/DASH 스트리밍 재생 기능을 제공합니다.

---

## 주요 기능

### 비디오 재생
- **FFmpeg 통합**: 네이티브 FFmpeg 라이브러리 바인딩
- **스트리밍 지원**: HLS, DASH 프로토콜 지원
- **Demuxer**: 비디오/오디오 스트림 분리

### 아키텍처
- **이벤트 루프**: 비동기 이벤트 처리
- **다운로더**: 네트워크 스트림 다운로드 관리
- **스케줄러**: 재생 타이밍 제어

---

## 프로젝트 구조

```
TizenSamplePlayer/
├── FFmpeg/              # FFmpeg C# 바인딩
├── Demux/               # 비디오/오디오 Demuxer
├── Downloader/          # 스트림 다운로드 관리
├── Common/              # 공통 유틸리티
├── EventLoop.cs         # 비동기 이벤트 처리
├── GenericScheduler.cs  # 스케줄링 로직
└── TizenSamplePlayer.cs # 메인 플레이어

FFmpegBindings/          # FFmpeg P/Invoke 바인딩
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **플랫폼** | Tizen TV 5.0+ |
| **언어** | C# |
| **프레임워크** | .NET 6, Tizen.NET |
| **미디어** | FFmpeg (Native Binding) |
| **프로토콜** | HLS, DASH |

---

## 해결한 문제

### 1. FFmpeg 네이티브 바인딩
**문제**: Tizen .NET에서 FFmpeg 사용 필요

**해결**: P/Invoke를 통한 FFmpeg 네이티브 라이브러리 바인딩 구현, 메모리 관리 및 콜백 처리

### 2. 스트리밍 재생 안정성
**문제**: 네트워크 불안정 시 재생 끊김

**해결**: 버퍼링 전략 및 재연결 로직 구현으로 안정적인 스트리밍 재생 보장

---

## 역할 및 기여

- Tizen .NET 플레이어 아키텍처 설계
- FFmpeg C# 바인딩 개발
- HLS/DASH 스트리밍 모듈 구현
- 이벤트 루프 및 스케줄러 개발

---

*이 프로젝트는 Samsung Tizen TV InApp TV 서비스를 위해 개발되었습니다.*
