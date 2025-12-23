# Tammi Performance Chart (Trace Tool)

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> AI Agent 성능 모니터링 및 시각화 도구 v2.0.0

![Version](https://img.shields.io/badge/version-2.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-lightgrey)

---

## 개요

**Tammi Performance Chart**는 Android 디바이스에서 실행되는 AI Agent의 성능을 실시간으로 모니터링하고 시각화하는 데스크톱 도구입니다. ADB(Android Debug Bridge)를 통해 디바이스의 로그를 수집하고, 각 Agent의 응답 시간을 직관적인 차트로 표현하여 QA 테스트 및 성능 분석에 활용됩니다.

이 도구는 AI 서비스의 품질 보증(QA) 과정에서 성능 병목 현상을 식별하고, 응답 시간 기준을 검증하는 데 핵심적인 역할을 합니다.

---

## 주요 기능

### 실시간 성능 모니터링
- **Turn별 처리 시간 추적**: HTTP 요청/응답의 전체 소요 시간과 개별 Agent의 처리 시간을 실시간으로 모니터링
- **타임라인 차트**: 시간 순서대로 성능 데이터를 시각화하여 트렌드 파악 용이

### 로그 파일 분석
- 기존에 저장된 로그 파일(`.txt`, `.log`)을 불러와 분석
- 실시간 모니터링과 병행하여 비교 분석 가능

### QA 테스트 지원 기능
- **Y축 기준선(Threshold) 설정**: 3초, 6초, 10초 프리셋 또는 커스텀 값 지정
- **Threshold 초과 턴 즉시 표시**: 기준선을 초과하는 턴 목록 자동 제공
- QA 테스트 기준에 맞는 성능 검증 자동화

### 데이터 관리
- **Export/Import Traces**: 실시간 데이터를 JSON 형식으로 내보내기/불러오기
- 테스트 데이터의 공유 및 재현 가능

### 사용자 경험
- **차트 줌 인/아웃**: 1x~3x 확대 및 가로 스크롤 지원
- **차트 범례 토글**: 클릭으로 특정 Agent 그래프 표시/숨김
- **모던 UI 테마**: 라이트 배경과 통일된 버튼 색상
- **UI 영문화**: 글로벌 팀과의 협업을 위한 영문 인터페이스

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Frontend** | HTML5, CSS3, JavaScript, Chart.js |
| **Backend** | Node.js |
| **Desktop App** | Electron (Cross-platform) |
| **Device Integration** | ADB (Android Debug Bridge) |
| **Data Format** | JSON |

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                    Desktop Application                   │
│  ┌─────────────────────────────────────────────────┐    │
│  │              Web UI (Browser View)               │    │
│  │  ┌─────────────┐  ┌─────────────────────────┐   │    │
│  │  │   Menu Bar  │  │     Chart Container     │   │    │
│  │  │  - Open Log │  │  ┌─────────────────────┐│   │    │
│  │  │  - Export   │  │  │  Timeline Chart     ││   │    │
│  │  │  - Import   │  │  │  (Chart.js)         ││   │    │
│  │  │  - Clear    │  │  └─────────────────────┘│   │    │
│  │  └─────────────┘  │  ┌─────────────────────┐│   │    │
│  │                   │  │  Threshold Controls ││   │    │
│  │                   │  └─────────────────────┘│   │    │
│  │                   └─────────────────────────────┘│   │
│  └─────────────────────────────────────────────────┘    │
│                           │                              │
│  ┌─────────────────────────────────────────────────┐    │
│  │              Node.js Backend Server              │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────┐  │    │
│  │  │ ADB Handler │  │ Log Parser  │  │WebSocket│  │    │
│  │  └─────────────┘  └─────────────┘  └─────────┘  │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
              ┌─────────────────────────┐
              │    Android Device       │
              │  (AI Agent Running)     │
              │    via ADB logcat       │
              └─────────────────────────┘
```

---

## 스크린샷

### 초기 화면
*ADB 장치 연결 대기 상태*

![초기 화면](./images/initial.png)

### 로그 그래프
*AI Agent의 Turn별 처리 시간을 시각화*

![로그 그래프](./images/log-graph.png)

### 장치 정보
*연결된 Android 디바이스 정보 확인*

![장치 정보](./images/device.png)

### 턴별 상세 정보
*각 턴의 발화 내용 및 Agent별 소요시간 확인*

![턴별 정보](./images/turn-info.png)

### 기준선 설정 기능
*QA 테스트를 위한 Threshold 설정 및 초과 턴 표시*

![기준선 설정](./images/graph-threshold.png)

---

## 지원 플랫폼

| 플랫폼 | 파일명 |
|--------|--------|
| Windows 10/11 (64-bit) | `tammi-chart-v2.0.0-win.exe` |
| macOS (Intel) | `tammi-chart-v2.0.0-macos-intel` |
| macOS (Apple Silicon M1/M2/M3) | `tammi-chart-v2.0.0-macos-apple-silicon` |

---

## 개발 과정에서의 도전과 해결

### 1. 실시간 로그 스트리밍 처리
**도전**: ADB logcat에서 대량의 로그가 빠르게 스트리밍되는 상황에서 안정적인 파싱과 UI 업데이트가 필요했습니다.

**해결**: 로그 버퍼링 및 배치 처리를 통해 성능을 최적화하고, WebSocket을 통한 효율적인 실시간 데이터 전송을 구현했습니다.

### 2. 크로스 플랫폼 호환성
**도전**: Windows와 macOS(Intel/Apple Silicon) 모두에서 동작하는 애플리케이션 배포가 필요했습니다.

**해결**: Electron을 활용하여 단일 코드베이스로 세 가지 플랫폼을 지원하고, 각 플랫폼별 빌드 파이프라인을 구축했습니다.

### 3. 다중 Agent 시각화
**도전**: 여러 Agent의 처리 시간을 하나의 차트에서 명확하게 구분하여 표시해야 했습니다.

**해결**: Chart.js의 다중 데이터셋 기능과 범례 토글 기능을 활용하여 사용자가 원하는 Agent만 선택적으로 볼 수 있도록 구현했습니다.

---

## 역할 및 기여

- 전체 애플리케이션 아키텍처 설계 및 구현
- ADB 연동 및 로그 파싱 로직 개발
- Chart.js 기반 실시간 시각화 구현
- Threshold 설정 및 QA 지원 기능 개발
- 크로스 플랫폼(Windows, macOS) 빌드 및 배포

---

## 버전 히스토리

| 버전 | 날짜 | 주요 변경사항 |
|------|------|--------------|
| v2.0.0 | 2025.12.20 | UI 영문화, 모던 테마 적용, 범례 토글 기능 |
| v1.8.0 | - | 차트 줌 인/아웃 기능, 범례 분리 |
| v1.7.0 | - | 메뉴 UI 그룹화, 버전 표시 개선 |
| v1.6.0 | - | Export/Import Traces 기능 |
| v1.5.0 | - | Clear Traces UI 개선, Show Logs 탭 UI |
| v1.4.0 | - | Y축 Threshold 기능, 초과 턴 표시 |

---

*이 프로젝트는 AI 음성 서비스 QA 및 성능 분석을 위해 개발되었습니다.*
