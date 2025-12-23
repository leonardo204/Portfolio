# zeroPlayer

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> YouTube Playlist-based Music Streaming App

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20iPadOS%20%7C%20macOS%20%7C%20visionOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-5.0-orange)
![iOS](https://img.shields.io/badge/iOS-12.4+-blue)
![App Store](https://img.shields.io/badge/App%20Store-Available-blue)

<a href="https://apps.apple.com/kr/app/zeroplayer/id1610259595">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

---

## Overview

**zeroPlayer** is an iOS music streaming app that allows you to add public YouTube playlists and enjoy music. You can freely add any YouTube playlist you want and use the sleep timer feature to comfortably listen to music before falling asleep.

With a focus on simple yet practical features, this app supports iOS, iPadOS, macOS (Apple Silicon), and visionOS.

---

## Key Features

### YouTube Playlist Integration
- **Add Playlists**: Add public YouTube playlist URLs to listen to music
- **Free Management**: Freely add/delete playlists as desired
- **YouTube Integration**: Seamless YouTube integration using YoutubeKit

### Music Playback
- **Background Playback**: Music continues playing even when the app is closed
- **Marquee Label**: Long titles displayed with scrolling animation
- **Continuous Playback**: Automatic continuous playback within playlist

### Sleep Timer
- **Timer Setting**: Sleep timer feature available in settings
- **Auto Stop**: Automatically stops playback after specified time
- **Sleep Mode**: Optimized for listening to music before sleep

### Side Menu Navigation
- **Intuitive UI**: Easy screen switching through side menu
- **Playlist Management**: View and manage saved playlist list

---

## Screenshots

### App Icon

![App Icon](./images/app-icon.png)

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Swift 5.0 (98.6%) |
| **UI Framework** | UIKit, Storyboard |
| **Architecture** | MVC |
| **Dependency Manager** | CocoaPods |
| **YouTube Integration** | YoutubeKit |
| **HTML Parsing** | Kanna |
| **JSON Parsing** | SwiftyJSON |
| **UI Components** | MarqueeLabel, QuickTableViewController |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                       zeroPlayer App                             │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                   Main View Controller                      │ │
│  │  ┌──────────────────────────────────────────────────────┐  │ │
│  │  │              Music Player Interface                   │  │ │
│  │  │  ┌────────────┐  ┌─────────────────────────────────┐ │  │ │
│  │  │  │  Artwork   │  │  Track Info (MarqueeLabel)      │ │  │ │
│  │  │  │            │  │  Artist / Title                 │ │  │ │
│  │  │  └────────────┘  └─────────────────────────────────┘ │  │ │
│  │  │  ┌──────────────────────────────────────────────────┐│  │ │
│  │  │  │            ◂◂    advancement-pause-icon: ⏸  ▸▸              ││  │ │
│  │  │  └──────────────────────────────────────────────────┘│  │ │
│  │  └──────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐   │
│  │  Side Menu   │  │   YouTube    │  │      Settings        │   │
│  │  ┌────────┐  │  │   Module     │  │  ┌────────────────┐  │   │
│  │  │Playlist│  │  │  ┌────────┐  │  │  │  Sleep Timer   │  │   │
│  │  │  List  │  │  │  │YoutubeK│  │  │  │  Preferences   │  │   │
│  │  └────────┘  │  │  │  it    │  │  │  └────────────────┘  │   │
│  └──────────────┘  │  └────────┘  │  └──────────────────────┘   │
│                    │  ┌────────┐  │                              │
│                    │  │ Kanna  │  │                              │
│                    │  │(Parser)│  │                              │
│                    │  └────────┘  │                              │
│                    └──────────────┘                              │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Utility Layer                            │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │ │
│  │  │  SwiftyJSON  │  │    Push      │  │   Custom Views   │  │ │
│  │  │              │  │  Handling    │  │                  │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     YouTube API         │
                 │   (Public Playlists)    │
                 └─────────────────────────┘
```

---

## Dependencies

| Library | Purpose |
|---------|---------|
| **YoutubeKit** | YouTube API integration and video playback |
| **Kanna** | HTML/XML parsing (playlist info extraction) |
| **SwiftyJSON** | JSON data parsing |
| **MarqueeLabel** | Scrolling animation label (long title display) |
| **QuickTableViewController** | Settings screen table view configuration |

---

## Challenges and Solutions

### 1. YouTube Playlist Parsing
**Challenge**: Needed to extract YouTube playlist information and convert it into a playable format within the app.

**Solution**: Used Kanna library to parse HTML and extracted video information through YoutubeKit to convert into a playable format.

### 2. Background Audio Playback
**Challenge**: Music needed to continue playing even when the app transitioned to background.

**Solution**: Enabled iOS Audio Background Mode and properly configured AVAudioSession to implement seamless playback in background.

### 3. Sleep Timer Implementation
**Challenge**: Needed functionality to precisely stop playback after user-specified time.

**Solution**: Implemented a sleep timer that works in background using Timer, and stored user settings in UserDefaults to maintain settings even after app restart.

---

## Role & Contributions

- Overall iOS app architecture design and implementation
- YouTube playlist integration system development
- Music playback engine and background playback implementation
- Sleep timer feature development
- Side menu navigation UI implementation
- App Store deployment and maintenance

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **iOS** | iOS 12.4 or later |
| **iPadOS** | iPadOS 12.4 or later |
| **macOS** | macOS 11.0 or later (Apple Silicon) |
| **visionOS** | visionOS 1.0 or later |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1.7 | 2023.08.15 | Thumbnail image bug fix |

---

## Related Links

- **App Store**: [zeroPlayer](https://apps.apple.com/kr/app/zeroplayer/id1610259595)
- **GitHub**: [leonardo204/cloudRadio_ios](https://github.com/leonardo204/cloudRadio_ios)

---

*This project is a personal music streaming app utilizing YouTube playlists.*
