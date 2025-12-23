# Cloud Client Web

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> 클라우드 이미지 스트리밍 웹 테스트 클라이언트

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-010101?logo=socketdotio&logoColor=white)

---

## 개요

**Cloud Client Web**은 클라우드 UI 이미지 스트리밍 서비스를 테스트하기 위한 웹 기반 클라이언트입니다.

WebSocket을 통해 서버로부터 실시간 이미지 프레임을 수신하고 Canvas에 렌더링하여 스트리밍 상태를 확인할 수 있습니다.

---

## 주요 기능

### WebSocket 스트리밍
- **실시간 연결**: 이미지 서버와 WebSocket 연결
- **바이너리 수신**: ArrayBuffer 기반 이미지 데이터 수신
- **연결 상태 표시**: 연결/해제 상태 실시간 표시

### 프레임 파싱
- **Web Worker**: 메인 스레드 블로킹 방지를 위한 Worker 기반 파싱
- **바이너리 파싱**: 커스텀 프로토콜 이미지 프레임 파싱
- **다중 이미지 처리**: 단일 메시지 내 복수 이미지 프레임 처리

### 이미지 렌더링
- **Canvas 렌더링**: HTML5 Canvas 기반 이미지 표시
- **셀 기반 업데이트**: 변경된 영역만 선택적 업데이트
- **다중 포맷 지원**: WebP, PNG, JPEG 지원

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────────┐
│                    Cloud Client Web                          │
│                                                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │  WebSocket  │  │ Web Worker  │  │      Canvas         │  │
│  │  Handler    │──│ (Parser)    │──│      Renderer       │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│         │                                    │               │
│         ▼                                    ▼               │
│  ┌─────────────────────────────────────────────────────────┐│
│  │                   ByteBuffer Parser                      ││
│  │              (Binary Frame Decoding)                     ││
│  └─────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **언어** | JavaScript (ES6+) |
| **마크업** | HTML5 |
| **통신** | WebSocket |
| **렌더링** | Canvas API |
| **병렬처리** | Web Workers |

---

## 역할 및 기여

- WebSocket 기반 스트리밍 클라이언트 개발
- 바이너리 프레임 파서 구현
- Web Worker 기반 비동기 파싱 구현
- Canvas 렌더링 모듈 개발

---

*이 프로젝트는 클라우드 UI 서비스 개발 시 테스트 및 디버깅을 위해 사용되었습니다.*
