# dotclaude

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Make Claude Code Smarter — Enhanced Claude Code Agent System

![Platform](https://img.shields.io/badge/platform-Claude%20Code-7C3AED)
![TypeScript](https://img.shields.io/badge/TypeScript-blue?logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-22%2B-339933?logo=node.js&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white)

---

## Overview

**dotclaude** is a framework that enhances Claude Code's agent system. It enables more systematic and intelligent use of Claude Code through a pipeline of 7 specialized agents, SQLite-based context preservation across sessions, a real-time HUD dashboard, and Telegram notifications. The entire environment can be set up instantly with a single command (`/dotclaude-init`).

---

## Key Features

### 7 Specialized Agent System
- **Planner**: Task analysis and execution planning
- **Architect**: System architecture design and structural decisions
- **Ralph (Implementer)**: Actual code implementation
- **Verifier**: Implementation verification and quality assurance
- **Reviewer**: Code review and improvement suggestions
- **Debugger**: Error analysis and problem resolution
- **Test Engineer**: Test creation and coverage management

### Agent Delegation Pipeline
- Automatic pipeline: Planner → Architect → Ralph + Test Engineer → Verifier → Reviewer
- Auto-triggering based on complexity (2+ file changes, architecture changes, etc.)
- Main context focuses on judgment and delegation; execution is delegated to specialized agents

### SQLite-Based Context Preservation
- Persistent storage of work state, key findings, and design decisions across sessions
- Knowledge accumulation and reuse through Context DB
- Automatic recovery during compaction (context compression)

### Real-Time HUD Dashboard
- Real-time rate limit usage monitoring
- Current task status and progress display
- Automatic error context tracking

### Automated Hooks System
- 5 auto-executing scripts (PreToolUse, PostToolUse, Notification, etc.)
- Automatic working file tracking and error context saving
- Automatic session summary generation

### Telegram Notifications
- Automatic Telegram messages upon long-running task completion
- Immediate alerts on error occurrence
- Remote monitoring support

### One-Command Initialization
- Instant full environment setup with `/dotclaude-init`
- Auto-generation of `.claude/` folder structure, DB, agents, and hooks
- Existing project updates via `/dotclaude-update`

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | TypeScript, JavaScript |
| **Runtime** | Node.js 22+ |
| **Database** | SQLite |
| **Platform** | Claude Code CLI |
| **Notification** | Telegram Bot API |
| **Architecture** | Multi-Agent Pipeline, Hook System |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     dotclaude Framework                          │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                   Agent Pipeline                            │ │
│  │  ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌─────────────┐  │ │
│  │  │ Planner  │→│ Architect │→│  Ralph   │→│ Test        │  │ │
│  │  │          │ │           │ │(Implmtr) │ │ Engineer    │  │ │
│  │  └──────────┘ └───────────┘ └──────────┘ └─────────────┘  │ │
│  │                                    │                        │ │
│  │                                    ▼                        │ │
│  │  ┌──────────┐ ┌───────────┐ ┌──────────┐                  │ │
│  │  │ Debugger │ │ Reviewer  │←│ Verifier │                  │ │
│  │  │          │ │           │ │          │                  │ │
│  │  └──────────┘ └───────────┘ └──────────┘                  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                  Core Infrastructure                        │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌────────────────────┐  │ │
│  │  │  Context DB  │ │   HUD        │ │   Hook System      │  │ │
│  │  │  (SQLite)    │ │   Dashboard  │ │   (5 Scripts)      │  │ │
│  │  └──────────────┘ └──────────────┘ └────────────────────┘  │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌────────────────────┐  │ │
│  │  │  Context     │ │  Telegram    │ │   Session          │  │ │
│  │  │  Monitor     │ │  Messenger   │ │   Manager          │  │ │
│  │  └──────────────┘ └──────────────┘ └────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    Claude Code CLI                          │ │
│  │  ┌─────────────────────────────────────────────────────┐   │ │
│  │  │  CLAUDE.md  ←→  .claude/agents/  ←→  .claude/db/   │   │ │
│  │  └─────────────────────────────────────────────────────┘   │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## Challenges and Solutions

### 1. Context Loss Between Sessions
**Challenge**: Claude Code loses the context of previous work when a session ends, and key information is also lost during context compaction.

**Solution**: Designed a SQLite-based Context DB to persistently store work state, key findings, and design decisions. Implemented a Context Monitor that automatically restores critical context when compaction is detected.

### 2. Systematic Handling of Complex Tasks
**Challenge**: Quality degraded when the agent proceeded without structure on large-scale tasks involving multiple file modifications.

**Solution**: Separated responsibilities into 7 specialized agents and built an automatic pipeline (Planner → Architect → Ralph → Verifier → Reviewer) to ensure accountability and quality control at each stage.

### 3. Rate Limit Management and Monitoring
**Challenge**: Work was interrupted when Claude Code's API rate limit was exceeded, and it was difficult to track current usage.

**Solution**: Implemented a real-time HUD dashboard for visual rate limit monitoring and integrated Telegram notifications for remote status checking of long-running tasks.

---

## Role & Contributions

- Designed and implemented multi-agent pipeline architecture
- Developed SQLite-based context preservation system
- Built real-time HUD dashboard and Context Monitor
- Developed 5 auto-executing hooks system
- Integrated Telegram notification system
- Implemented one-command initialization system (`/dotclaude-init`, `/dotclaude-update`)

---

## Links

- **GitHub**: [leonardo204/dotclaude](https://github.com/leonardo204/dotclaude)
- **Contact**: zerolive7@gmail.com

---

*This project enhances Claude Code's agent system to provide a more systematic and intelligent AI development environment.*
