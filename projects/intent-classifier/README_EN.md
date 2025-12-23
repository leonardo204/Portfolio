# Intent Classifier Chat

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> sLLM-based Interactive Intent Classification Desktop Application

![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-lightgrey)
![Electron](https://img.shields.io/badge/Electron-47848F?logo=electron&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)

---

## Overview

**Intent Classifier Chat** is an interactive intent classification test tool for Vietnamese Voice Assistant. It utilizes sLLM (Small Language Model) API to classify user input intentions in real-time and displays results through an intuitive Chat UI.

It supports 19 intent categories and provides dynamic model switching and real-time health check features.

---

## Key Features

### Intent Classification
- **Real-time Classification**: Immediate intent analysis using sLLM API
- **Level 1/2 Intent**: Main Intent and Sub Intent display
- **Response Time Display**: Processing time in milliseconds

### Model Management
- **Dynamic Model Switching**: Change models without restart
- **Auto Model Validation**: Model test on server/page load
- **Default Model Restore**: One-click default setting restoration

### Monitoring
- **Health Check**: Automatic status check every 10 seconds
- **Status Indicator**: Green(normal)/Red(error)/Gray(checking)
- **API Logging**: Request/response logs in browser console

### Desktop App
- **Portable Version**: No installation required
- **Cross Platform**: macOS Universal, Windows Portable
- **Code Signing**: Apple Notarization support

---

## Supported Intent Categories (19)

| Main Intent | Description |
|-------------|-------------|
| Alarm | Alarm related |
| Calendar | Schedule related |
| Chat | General chat |
| DeviceControl | TV control |
| MediaControl | Media playback control |
| MediaRecommendation | Content recommendation |
| Weather | Weather information |
| Youtube | YouTube app control |
| Spotify | Spotify app control |
| ... | 10 more categories |

---

## Architecture

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
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│                 ┌─────────────────────────┐                     │
│                 │      vLLM API Server    │                     │
│                 └─────────────────────────┘                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## Challenges and Solutions

### 1. Dynamic Model Switching
**Challenge**: Needed to change models at runtime without app restart.

**Solution**: Implemented a system that dynamically updates YAML config files and performs automatic validation before model changes.

### 2. Stable Health Check
**Challenge**: Needed continuous monitoring of API server status.

**Solution**: Implemented real-time status monitoring system combining 10-second interval polling with visual status indicators.

---

## Role & Contributions

- Electron desktop app architecture design
- sLLM API integrated intent classification system development
- Dynamic model management system implementation
- Cross-platform build and deployment system setup
- Apple Notarization automation configuration

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **Additional Installation** | None (Portable) |
| **macOS** | macOS 10.13+ |
| **Windows** | Windows 10+ |

---

*This project is a development tool for Vietnamese Voice Assistant intent classification testing.*
