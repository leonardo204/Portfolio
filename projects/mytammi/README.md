# MyTammi

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> 베트남 TV 미디어 AI 어시스턴트 — Multi-Agent 아키텍처 기반 지능형 대화 시스템

![Platform](https://img.shields.io/badge/platform-Web-blue)
![Backend](https://img.shields.io/badge/backend-NestJS-E0234E)
![Frontend](https://img.shields.io/badge/frontend-Vue%203-4FC08D)
![TypeScript](https://img.shields.io/badge/TypeScript-100%25-3178C6)
![LLM](https://img.shields.io/badge/LLM-Gemini%202.5-4285F4)
![Monorepo](https://img.shields.io/badge/monorepo-Turborepo-EF4444)

---

## 개요

**MyTammi**는 베트남 TV 미디어 서비스를 위한 AI 어시스턴트로, Multi-Agent 아키텍처를 기반으로 사용자의 자연어 질의를 18개 도메인(72개 액션)으로 분류하고, 8개의 전문 서비스 에이전트로 라우팅하여 처리하는 지능형 대화 시스템입니다. LangChain/LangGraph를 활용한 에이전트 오케스트레이션과 Google Gemini 2.5 Flash/Pro 기반의 자연어 처리를 통해 TV 편성표 조회, 콘텐츠 검색, 사용자 지원 등 다양한 미디어 서비스를 대화형으로 제공합니다.

---

## 주요 기능

### Multi-Agent 오케스트레이션
- 8개 전문 서비스 에이전트 (ChatAgent, ScheduleAgent 등)
- Core Agent가 인텐트 분류 결과를 기반으로 적절한 서비스 에이전트로 자동 라우팅
- LangGraph 기반 에이전트 상태 관리 및 워크플로우 제어

### 인텐트 분류 시스템
- 18개 도메인, 72개 액션에 대한 정밀 인텐트 분류
- 슬롯 필링(Slot Filling)을 통한 누락 정보 자동 수집
- 세션 캐시 기반 대화 컨텍스트 유지

### AI 기반 자연어 처리
- Google Gemini 2.5 Flash (빠른 응답) / Pro (복잡한 추론) 모델 활용
- Gemini Google Search Grounding을 통한 실시간 웹 검색 통합
- 베트남어/영어 다국어 자연어 이해

### 실시간 대화 인터페이스
- Vue 3 + Naive UI 기반 반응형 채팅 UI
- 스트리밍 응답 지원으로 실시간 타이핑 효과
- 세션 기반 대화 이력 관리

### 외부 서비스 연동
- TV 편성표 API, 콘텐츠 메타데이터 API 등 외부 시스템 연동
- Gemini Google Search Grounding 내장 웹 검색
- 도메인별 전용 비즈니스 로직 처리

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **Language** | TypeScript 100% |
| **Backend** | NestJS |
| **Frontend** | Vue 3 + Naive UI |
| **AI/LLM** | Google Gemini 2.5 Flash/Pro |
| **Agent Framework** | LangChain, LangGraph |
| **Web Search** | Gemini Google Search Grounding (built-in) |
| **Monorepo** | Turborepo + pnpm workspaces |
| **Build** | Vite (Frontend), tsc (Backend) |

---

## 아키텍처

```
┌──────────────────────────────────────────────────────────────────────┐
│                          MyTammi System                              │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐  │
│  │                   Chat UI (Vue 3 + Naive UI)                   │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌─────────────────────┐  │  │
│  │  │  Chat Input  │  │  Message     │  │  Session Manager    │  │  │
│  │  │  Interface   │  │  Stream      │  │  & History          │  │  │
│  │  └──────────────┘  └──────────────┘  └─────────────────────┘  │  │
│  └────────────────────────────┬───────────────────────────────────┘  │
│                               │                                      │
│                               ▼                                      │
│  ┌────────────────────────────────────────────────────────────────┐  │
│  │                Core Agent (NestJS + LangGraph)                 │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌─────────────────────┐  │  │
│  │  │   Intent     │  │   Session    │  │   Slot Filling      │  │  │
│  │  │   Router     │  │   Cache      │  │   Engine            │  │  │
│  │  │ (18 domains) │  │              │  │                     │  │  │
│  │  └──────────────┘  └──────────────┘  └─────────────────────┘  │  │
│  └────────────────────────────┬───────────────────────────────────┘  │
│                               │                                      │
│                               ▼                                      │
│  ┌────────────────────────────────────────────────────────────────┐  │
│  │              Service Agents (8 Specialized Agents)             │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌───────────────────────┐  │  │
│  │  │  Chat       │  │  Schedule   │  │  Content Search       │  │  │
│  │  │  Agent      │  │  Agent      │  │  Agent                │  │  │
│  │  └─────────────┘  └─────────────┘  └───────────────────────┘  │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌───────────────────────┐  │  │
│  │  │  Domain     │  │  Web Search │  │  External API         │  │  │
│  │  │  Logic      │  │  (Gemini    │  │  Integration          │  │  │
│  │  │  Agent      │  │  Grounding) │  │  Agent                │  │  │
│  │  └─────────────┘  └─────────────┘  └───────────────────────┘  │  │
│  └────────────────────────────────────────────────────────────────┘  │
│                               │                                      │
│                               ▼                                      │
│  ┌────────────────────────────────────────────────────────────────┐  │
│  │                    External Services                           │  │
│  │  ┌──────────┐  ┌──────────────┐  ┌─────────────────────────┐  │  │
│  │  │  Gemini  │  │  TV Schedule │  │  Content Metadata       │  │  │
│  │  │  2.5 API │  │  API         │  │  API                    │  │  │
│  │  └──────────┘  └──────────────┘  └─────────────────────────┘  │  │
│  └────────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 개발 과정에서의 도전과 해결

### 1. 대규모 인텐트 분류 시스템 설계
**도전**: 18개 도메인, 72개 액션이라는 대규모 인텐트 체계를 정확하게 분류해야 했으며, 베트남어의 언어적 특성까지 고려해야 했습니다.

**해결**: 계층적 인텐트 분류 구조를 설계하여 먼저 도메인을 분류한 후 세부 액션을 결정하는 2단계 분류 방식을 적용했습니다. Gemini 모델의 structured output 기능을 활용하여 분류 정확도를 높이고, 슬롯 필링을 통해 부족한 정보를 대화형으로 수집하도록 구현했습니다.

### 2. Multi-Agent 오케스트레이션
**도전**: 8개의 서비스 에이전트 간 상태 공유, 에러 핸들링, 그리고 대화 컨텍스트 유지가 복잡한 문제였습니다.

**해결**: LangGraph를 활용하여 에이전트 워크플로우를 그래프 기반으로 모델링하고, 세션 캐시를 통해 대화 상태를 중앙 집중 관리했습니다. 각 에이전트의 실패 시 fallback 로직과 재시도 메커니즘을 구현하여 안정성을 확보했습니다.

### 3. 실시간 웹 검색 통합
**도전**: 에이전트가 최신 정보를 필요로 할 때 적절한 시점에 웹 검색을 트리거하고, 검색 결과를 대화 컨텍스트에 자연스럽게 통합해야 했습니다.

**해결**: Gemini Google Search Grounding을 활용하여 LLM 레벨에서 웹 검색이 내장되도록 구현했습니다. 모델이 자체적으로 검색 필요성을 판단하고 결과를 응답에 반영하므로, 별도의 검색 오케스트레이션 없이도 최신 정보를 제공할 수 있었습니다.

### 4. Monorepo 환경에서의 프론트엔드/백엔드 통합
**도전**: Turborepo + pnpm workspaces 기반 모노레포에서 프론트엔드(Vue 3)와 백엔드(NestJS)의 공유 타입, 빌드 순서, 개발 환경을 효율적으로 관리해야 했습니다.

**해결**: 공유 패키지(shared types, utilities)를 별도 워크스페이스로 분리하고, Turborepo의 태스크 파이프라인을 설정하여 빌드 의존성을 자동 관리했습니다. 개발 환경에서는 동시 실행(dev 모드)을 지원하여 프론트엔드/백엔드를 하나의 명령으로 구동할 수 있도록 구성했습니다.

---

## 역할 및 기여

- Multi-Agent 아키텍처 설계 및 LangGraph 기반 워크플로우 구현
- 18개 도메인 / 72개 액션 인텐트 분류 시스템 개발
- NestJS 백엔드 서비스 및 8개 서비스 에이전트 구현
- Vue 3 + Naive UI 기반 실시간 채팅 인터페이스 개발
- Gemini Google Search Grounding 통합 및 웹 검색 기능 구현
- Turborepo + pnpm workspaces 기반 모노레포 구성

---

## 관련 링크

- **Repository**: Private (Bitbucket) — 회사 프로젝트로 소스 코드 비공개
- **Contact**: zerolive7@gmail.com

---

*이 프로젝트는 베트남 TV 미디어 서비스를 위한 AI 기반 지능형 대화 어시스턴트입니다.*
