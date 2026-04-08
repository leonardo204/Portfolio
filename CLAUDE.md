# Claude Code 개발 가이드

> 공통 규칙(Agent Delegation, 커밋 정책, Context DB 등)은 글로벌 설정(`~/.claude/CLAUDE.md`)을 따릅니다.
> 글로벌 미설치 시: `curl -fsSL https://raw.githubusercontent.com/leonardo204/dotclaude/main/install.sh | bash`

---

## Slim 정책

이 파일은 **100줄 이하**를 유지한다. 새 지침 추가 시:
1. 매 턴 참조 필요 → 이 파일에 1줄 추가
2. 상세/예시/테이블 → ref-docs/*.md에 작성 후 여기서 참조
3. ref-docs 헤더: `# 제목 — 한 줄 설명` (모델이 첫 줄만 보고 필요 여부 판단)

---

## PROJECT

### 개요

**Portfolio** — GitHub Pages 기반 개인 포트폴리오 (Markdown)

| 항목 | 값 |
|------|-----|
| 형식 | Markdown (GitHub-flavored) |
| 구조 | README.md (한국어) + README_EN.md (영어) + projects/*/README*.md |
| 상태 | 운영 중 |

### 구조

- `README.md` / `README_EN.md` — 메인 포트폴리오 (한/영)
- `projects/<name>/README.md` + `README_EN.md` — 프로젝트별 상세 페이지
- 섹션: AI & Voice (Work), Cloud UI (Work), Media Player (Work), Dev Tools (Work), Side Projects

### 상세 문서

- [Context DB](Ref-docs/claude/context-db.md) — SQLite 기반 세션/태스크/결정 저장소
- [Context Monitor](Ref-docs/claude/context-monitor.md) — HUD + compaction 감지/복구
- [컨벤션](Ref-docs/claude/conventions.md) — 커밋, 주석, 로깅 규칙
- [셋업](Ref-docs/claude/setup.md) — 새 환경 초기 설정

### 핵심 규칙

- 프로젝트 추가 시 README.md + README_EN.md 동시 업데이트
- 프로젝트 상세 페이지는 `projects/<name>/` 하위에 한/영 README 쌍으로 생성
- 테이블 포맷: `| [Name](./projects/name/) | 설명 | \`Tech1\` \`Tech2\` |`
- 아키텍처/워크플로우 다이어그램은 **Mermaid** 사용 (ASCII art 금지) → [다이어그램 가이드](Ref-docs/diagram-guide.md)
- 프로젝트 추가/변경 시 메인 README **Tech Stack** 배지도 동기화 확인
- Side Projects 테이블: `| [Name](./projects/name/) | 설명 | \`Tech\` | 연도 | Link |`

---

*최종 업데이트: 2026-04-06*
