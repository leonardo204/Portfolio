# SimpleSecretRotto (Lucky Lotto)

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> AI-Powered Lottery Number Analysis and Recommendation App

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20iPadOS%20%7C%20macOS%20%7C%20visionOS-lightgrey)
![Swift](https://img.shields.io/badge/Swift-5.9-orange)
![SwiftUI](https://img.shields.io/badge/SwiftUI-blue)
![App Store](https://img.shields.io/badge/App%20Store-Available-blue)

<a href="https://apps.apple.com/kr/app/simplesecretrotto/id6740446215">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

---

## Overview

**SimpleSecretRotto (Lucky Lotto)** is an iOS app that uses AI algorithms to analyze lottery winning numbers and recommend weekly lucky numbers. Through big data-based trend analysis and pattern visualization, it provides number frequency, probability analysis, and latest trends, generating weighted number combinations based on this data.

It smartly combines user preferences with AI recommendations to provide insights for lottery number selection through an intuitive UI. Supports iOS, iPadOS, macOS (Apple Silicon), and visionOS.

---

## Key Features

### Winning Number Analysis
- **Latest Winning Numbers**: Check the latest lottery winning numbers in real-time
- **Winning Statistics**: History and statistics of winning numbers by draw
- **Number Frequency**: Analysis of historical occurrence count for each number

### Probability-Based Recommendations
- **Weighted Recommendations**: Generate numbers reflecting frequency and latest trends
- **Exponential Trend Analysis**: Higher weight for recent draws
- **Animated Number Generation**: Display recommended numbers with spring animation

### Data Visualization
- **Probability Charts**: Visualize occurrence probability for each number
- **Frequency Analysis List**: Rankings of most/least occurring numbers
- **Winning Statistics View**: Comprehensive winning pattern analysis

### User Settings
- **Lucky Number Setting**: Save preferred numbers and combine with AI recommendations
- **Lucky Number History**: View generated number history
- **Weekly Winning Statistics**: Weekly winning status statistics
- **Offline Mode Support**: Use cached data without network connection
- **Auto Data Sync**: Auto-update latest data when app activates

---

## Screenshots

> Screenshots coming soon

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Swift 5.9 (100%) |
| **UI Framework** | SwiftUI |
| **Architecture** | MVVM |
| **Networking** | URLSession |
| **Data Persistence** | UserDefaults, Cache |
| **Backend** | REST API (Private Server) |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     SimpleSecretRotto App                        │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                      Views Layer                            │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────────┐    │ │
│  │  │  HomeView    │ │AnalysisView │ │  SettingsView    │    │ │
│  │  └──────────────┘ └──────────────┘ └──────────────────┘    │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────────┐    │ │
│  │  │LatestNumbers │ │WinningStats │ │ProbabilityChart  │    │ │
│  │  │    View      │ │    View     │ │     View         │    │ │
│  │  └──────────────┘ └──────────────┘ └──────────────────┘    │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Services Layer                           │ │
│  │  ┌─────────────────────┐  ┌─────────────────────────────┐  │ │
│  │  │    APIService       │  │     LottoDataService        │  │ │
│  │  │  - Health Check     │  │  - Fetch Draw History       │  │ │
│  │  │  - Get Draws        │  │  - Generate Numbers         │  │ │
│  │  │  - Get Statistics   │  │  - Frequency Analysis       │  │ │
│  │  │  - Post Numbers     │  │  - Trend Weighting          │  │ │
│  │  └─────────────────────┘  └─────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │    REST API Server      │
                 │   (Private Backend)     │
                 └─────────────────────────┘
```

---

## Number Generation Algorithm

```
Weight = Base Frequency Weight × Latest Trend Weight

Latest Trend Weight = exp(-λ × Draw_Difference)
```

- Calculate base weight from historical winning number frequencies
- Apply exponential function for higher weight on recent draws
- Select 6 numbers through weighted random sampling

---

## Challenges and Solutions

### 1. Statistics-Based Number Generation Algorithm
**Challenge**: A meaningful number recommendation system based on historical data, not simple random, was needed.

**Solution**: Designed a weight algorithm combining frequency and latest trends. Used exponential function to give higher weight to recent draws, performing probabilistic sampling based on this.

### 2. Offline Mode and Data Synchronization
**Challenge**: The app needed to function normally even with unstable network connections.

**Solution**: Implemented dual queue system (primary + retry queue) to manage failed transmission data, preventing data loss through automatic retry scheduling.

### 3. Real-time Data Refresh
**Challenge**: Latest data needed to be automatically reflected when the app returns from background to foreground.

**Solution**: Monitored app lifecycle using SwiftUI's `scenePhase`, implementing automatic data refresh on foreground transition.

---

## Role & Contributions

- iOS app overall architecture design (MVVM)
- SwiftUI-based UI/UX implementation
- Statistics-based number generation algorithm development
- REST API integration and network layer implementation
- Offline mode and caching system development
- Data synchronization and scheduling system implementation

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **iOS** | iOS 17.6 or later |
| **iPadOS** | iPadOS 17.6 or later |
| **macOS** | macOS 14.0 or later (Apple Silicon) |
| **visionOS** | visionOS 1.0 or later |
| **Build Environment** | Xcode 15.0+ |
| **Language** | Swift 5.9 |

---

## Related Links

- **App Store**: [SimpleSecretRotto - Lucky Lotto](https://apps.apple.com/kr/app/simplesecretrotto/id6740446215)
- **GitHub**: [leonardo204/SimpleSecretRotto](https://github.com/leonardo204/SimpleSecretRotto)

---

*This project is a personal project for AI-based lottery number analysis and recommendation.*
