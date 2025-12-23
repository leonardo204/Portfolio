# Google Cloud STT Test

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Google Cloud Speech-to-Text Real-time Streaming Test Application

![Platform](https://img.shields.io/badge/platform-Web-lightgrey)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google%20Cloud-4285F4?logo=googlecloud&logoColor=white)

---

## Overview

**Google Cloud STT Test** is a web application for testing real-time streaming features of Google Cloud Speech-to-Text API. It provides various features including real-time voice transcription via microphone, multi-language support, and voice activity detection.

It also serves as a reference implementation for speech recognition in STB (Set-Top Box) environments, including an Android TV integration guide.

---

## Key Features

### Real-time Speech Recognition
- **16kHz Optimized**: Sample rate optimized for voice commands
- **Interim Results Display**: Real-time transcription during speech (gray italic)
- **Final Results Display**: Final transcription after speech (with confidence)

### Multi-language Support
- **Auto Language Detection**: Automatic detection of Korean, English, Vietnamese
- **Fixed Language Mode**: Lock to specific language

### Voice Activity Detection
- **Auto Speech End**: Based on END_OF_SINGLE_UTTERANCE event
- **Voice Activity Events**: Real-time speech start/end detection
- **Audio Level Visualization**: Canvas-based input level display

### Performance Analysis
- **Event Timeline**: Chronological logging of all events
- **Metadata Display**: Language, confidence, timestamps
- **Performance Metrics**: Transcription latency, end-of-speech detection speed

---

## System Architecture

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

## Tech Stack

| Category | Technology |
|----------|------------|
| **Backend** | Node.js 18+, WebSocket (ws) |
| **Frontend** | Vanilla JavaScript (ES6 Modules) |
| **Audio** | Web Audio API, AudioWorklet (16kHz) |
| **Cloud** | Google Cloud Speech-to-Text v6 (gRPC) |
| **Container** | Docker, Docker Compose |
| **Web Server** | nginx (Client), Express (API) |

---

## Challenges and Solutions

### 1. Real-time Audio Streaming
**Challenge**: Needed to capture 16kHz audio in real-time from the browser and transmit to server.

**Solution**: Built a pipeline using AudioWorklet API to process audio in a separate thread and convert to LINEAR16 format for WebSocket transmission.

### 2. gRPC Bidirectional Streaming
**Challenge**: Needed to connect Google Cloud STT API's bidirectional streaming with WebSocket-based web client.

**Solution**: Implemented a session manager in Node.js server to bridge WebSocket and gRPC streams.

### 3. End-of-Speech Detection
**Challenge**: Needed to accurately detect when user stops speaking.

**Solution**: Implemented auto-termination logic combining Google STT's END_OF_SINGLE_UTTERANCE event with voice activity events.

---

## Role & Contributions

- Real-time speech recognition system architecture design
- WebSocket-gRPC bridge server development
- AudioWorklet-based audio capture module implementation
- Docker containerization and deployment script creation
- Android TV integration guide documentation

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **Docker** | Docker Desktop or Docker Engine |
| **Node.js** | 18 or later (for manual execution) |
| **Browser** | Chrome 90+, Firefox 88+, Safari 14.1+ |
| **Google Cloud** | Speech-to-Text API enabled |

---

*This project is a POC testing tool for STB speech recognition feature development.*
