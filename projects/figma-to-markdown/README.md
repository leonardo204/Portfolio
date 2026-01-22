# Figma to Markdown

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Figma 디자인을 Confluence 호환 Markdown 문서로 자동 변환하는 AI 기반 플러그인

![Platform](https://img.shields.io/badge/platform-Figma-F24E1E)
![TypeScript](https://img.shields.io/badge/TypeScript-83.7%25-3178C6)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 개요

**Figma to Markdown**은 AI를 활용하여 Figma 디자인 프레임을 Confluence 호환 Markdown 문서로 자동 변환하는 Figma 플러그인입니다. 디자인 스펙 문서화 작업을 자동화하여 개발자와 디자이너 간의 협업 효율을 크게 향상시킵니다.

---

## 주요 기능

### AI 기반 문서 변환
- 다양한 LLM 제공자 지원 (OpenAI, Claude, Azure OpenAI, Ollama)
- Figma 프레임 구조를 지능적으로 분석하여 Markdown 생성

### 다중 프레임 처리
- 여러 프레임을 순차 처리하여 하나의 통합 문서로 병합
- 프레임별 독립적인 문서 생성도 가능

### Mermaid 다이어그램 자동 생성
- 디자인 흐름을 분석하여 플로우차트 자동 생성
- 프로세스 다이어그램 및 시퀀스 다이어그램 지원

### 다국어 지원
- 6개 언어 지원: 영어, 일본어, 중국어, 스페인어, 프랑스어, 독일어
- 문서 출력 언어 선택 가능

### Rate Limiting 관리
- API 제한 자동 감지 및 재시도 로직
- 안정적인 대량 처리 지원

### 토큰 사용량 추적
- 프레임별 토큰 사용량 실시간 모니터링
- 전체 비용 관리 기능

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Language** | TypeScript (83.7%), JavaScript (16.3%) |
| **UI Framework** | React |
| **Platform** | Figma Plugin API |
| **AI Providers** | OpenAI, Claude (Anthropic), Azure OpenAI, Ollama |
| **Output Format** | Markdown, Mermaid |
| **License** | MIT |

---

## 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                    Figma to Markdown Plugin                      │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                      Plugin UI (React)                      │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌────────────────────┐  │ │
│  │  │  Frame       │ │   Settings   │ │   Token Usage      │  │ │
│  │  │  Selector    │ │   Panel      │ │   Monitor          │  │ │
│  │  └──────────────┘ └──────────────┘ └────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Core Processing                          │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌────────────────────┐  │ │
│  │  │  Frame       │ │   LLM        │ │   Markdown         │  │ │
│  │  │  Parser      │ │   Provider   │ │   Generator        │  │ │
│  │  └──────────────┘ └──────────────┘ └────────────────────┘  │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌────────────────────┐  │ │
│  │  │  Mermaid     │ │   Rate       │ │   Multi-Frame      │  │ │
│  │  │  Generator   │ │   Limiter    │ │   Merger           │  │ │
│  │  └──────────────┘ └──────────────┘ └────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                   LLM Providers                             │ │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────────┐ ┌──────────────┐  │ │
│  │  │ OpenAI  │ │ Claude  │ │ Azure OpenAI│ │   Ollama     │  │ │
│  │  │   API   │ │   API   │ │     API     │ │   (Local)    │  │ │
│  │  └─────────┘ └─────────┘ └─────────────┘ └──────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## 사용 방법

### 플러그인 설치
1. Figma에서 Community 탭으로 이동
2. "Figma to Markdown" 검색
3. 플러그인 설치

### 기본 사용법
1. Figma에서 변환할 프레임 선택
2. 플러그인 실행 (Plugins > Figma to Markdown)
3. LLM 제공자 및 API 키 설정
4. 출력 언어 선택
5. "Generate" 버튼 클릭
6. 생성된 Markdown 복사 또는 내보내기

### LLM 설정
- **OpenAI**: API 키 입력
- **Claude**: Anthropic API 키 입력
- **Azure OpenAI**: Endpoint 및 키 입력
- **Ollama**: 로컬 서버 URL 입력 (무료)

---

## 개발 과정에서의 도전과 해결

### 1. Figma 프레임 구조 분석
**도전**: Figma의 복잡한 레이어 구조와 컴포넌트 인스턴스를 정확하게 파싱하여 문서화 가능한 형태로 변환해야 했습니다.

**해결**: Figma Plugin API의 노드 트리를 재귀적으로 탐색하여 계층 구조를 추출하고, 컴포넌트 타입별 맞춤 처리 로직을 구현했습니다.

### 2. 다중 LLM 제공자 통합
**도전**: OpenAI, Claude, Azure, Ollama 등 다양한 API 형식과 응답 구조를 통일된 인터페이스로 처리해야 했습니다.

**해결**: Provider 패턴을 적용하여 각 LLM의 특성을 추상화하고, 공통 인터페이스를 통해 일관된 호출이 가능하도록 설계했습니다.

### 3. Rate Limiting 및 대량 처리
**도전**: 여러 프레임을 연속 처리할 때 API Rate Limit에 걸리는 문제가 발생했습니다.

**해결**: 지수 백오프 재시도 로직과 요청 큐잉 시스템을 구현하여 안정적인 대량 처리가 가능하도록 했습니다.

---

## 역할 및 기여

- Figma 플러그인 아키텍처 설계 및 구현
- 다중 LLM 제공자 통합 인터페이스 개발
- React 기반 플러그인 UI 구현
- Mermaid 다이어그램 자동 생성 로직 개발
- 다국어 지원 시스템 구현

---

## 관련 링크

- **GitHub**: [leonardo204/figma-to-markdown](https://github.com/leonardo204/figma-to-markdown)
- **Contact**: zerolive7@gmail.com

---

*이 프로젝트는 디자인-개발 협업 효율화를 위한 자동화 도구입니다.*
