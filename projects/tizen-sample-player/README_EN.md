# Tizen Sample Player

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> .NET-based Video Player for Samsung Tizen TV with FFmpeg Bindings

![Platform](https://img.shields.io/badge/platform-Tizen%20TV-1428A0)
![.NET](https://img.shields.io/badge/.NET-512BD4?logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)

---

## Overview

**Tizen Sample Player** is a .NET-based video player running on Samsung Tizen TV platform.

It supports various video formats through FFmpeg native bindings and provides HLS/DASH streaming playback capabilities.

---

## Key Features

### Video Playback
- **FFmpeg Integration**: Native FFmpeg library bindings
- **Streaming Support**: HLS, DASH protocol support
- **Demuxer**: Video/audio stream separation

### Architecture
- **Event Loop**: Asynchronous event processing
- **Downloader**: Network stream download management
- **Scheduler**: Playback timing control

---

## Project Structure

```
TizenSamplePlayer/
├── FFmpeg/              # FFmpeg C# bindings
├── Demux/               # Video/audio Demuxer
├── Downloader/          # Stream download management
├── Common/              # Common utilities
├── EventLoop.cs         # Async event processing
├── GenericScheduler.cs  # Scheduling logic
└── TizenSamplePlayer.cs # Main player

FFmpegBindings/          # FFmpeg P/Invoke bindings
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Platform** | Tizen TV 5.0+ |
| **Language** | C# |
| **Framework** | .NET 6, Tizen.NET |
| **Media** | FFmpeg (Native Binding) |
| **Protocol** | HLS, DASH |

---

## Challenges and Solutions

### 1. FFmpeg Native Binding
**Challenge**: Need to use FFmpeg in Tizen .NET

**Solution**: Implemented FFmpeg native library binding through P/Invoke, handling memory management and callbacks

### 2. Streaming Playback Stability
**Challenge**: Playback interruption during network instability

**Solution**: Implemented buffering strategy and reconnection logic for stable streaming playback

---

## Role & Contributions

- Tizen .NET player architecture design
- FFmpeg C# binding development
- HLS/DASH streaming module implementation
- Event loop and scheduler development

---

*This project was developed for Samsung Tizen TV InApp TV service.*
