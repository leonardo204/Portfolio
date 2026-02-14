# STB Middleware 정합/개발

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> 케이블 TV 셋톱박스 미들웨어 개발 및 신규 단말 정합 (2012-2022)

![Language](https://img.shields.io/badge/C-A8B9CC?logo=c&logoColor=white)
![Language](https://img.shields.io/badge/C++-00599C?logo=cplusplus&logoColor=white)
![Language](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Platform](https://img.shields.io/badge/Embedded-007ACC)

---

## 개요

- **기간**: 2012 - 2022 (약 10년)
- **분야**: 케이블 TV 셋톱박스(STB) 미들웨어 개발 및 신규 단말 정합
- **규모**: 30여 건의 공식 프로젝트
- **대상 MSO**: TBroad, 제주방송, LGHV, 딜라이브, 충북방송(CCS), KCTV, HCN, JCN 등
- **업무 범위**: 신규 단말 정합 · UI/UX 서비스 개발 · CAS/XCAS 전환 · 클라우드 서비스 구축

### 소속 및 배경

- **알티캐스트** (Alticast, 2012-2019)
  - DVB-MHP, OCAP, ACAP 기반 미들웨어 세계 최초 상용화
  - 전 세계 25개+ 유료방송 사업자, 5,000만 대+ 디바이스에 플랫폼 공급
  - STB 미들웨어, SDP, UI/UX 솔루션, CAS/DRM, 방송 송출 시스템 등 유료방송 소프트웨어 전 영역 사업
- **알티미디어** (Altimedia, 2019-2025)
  - 알티캐스트에서 물적분할, 미디어 플랫폼 사업 전체 승계
  - 국내 + 유럽/아시아 해외 고객, 베트남 법인 운영
  - KT 그룹사 편입
- **KT 알티미디어** (KT Altimedia, 2025-현재)
  - 사명 변경

### UI/UX 플랫폼 진화

| 세대 | 플랫폼 | 방식 |
|:-----|:-------|:-----|
| 1세대 | **Windmill** | 저사양 STB에서 2D/3D 고품질 애니메이션을 구현하는 그래픽스 엔진 |
| 2세대 | **Wind3 / Command Cloud** | 클라우드 커맨드 기반 UI |
| 3세대 | **Image Cloud** | 클라우드 렌더링 + STB 경량 프레젠테이션 레이어 |

> 핵심 과제: 레거시 단말과 차세대 클라우드 서비스의 공존을 미들웨어 레벨에서 해결

---

## 주요 프로젝트

### Windmill / Wind3 UI/UX 서비스
- **TBroad Windmill**: Smart UI/UX 적용 프로젝트 (전 단말 대상, 2013-2015)
- **Windmill 고도화**: UI/UX 고도화 프로젝트 (전 단말 대상, 2013-2016)
- **제주방송 Windmill**: 통합UI 서비스 개발 (전 단말 대상, 2014-2015)
- **Wind3 (Command Cloud)**: CJ Cloud UI PoC 및 UI/UX 프로젝트 적용 (2015-2016)

### Image Cloud 서비스
- **제주방송 Image Cloud**: Cloud 구축 및 UHD STB 개발 (전 단말 대상, 2017-2019)
- **TBroad Image Cloud**: 클라우드 서비스 구축 (DP 대상, 2018-2019)
- **LGHV Image Cloud**: 일체화 프로젝트 (전 단말 대상, 2021-2022)
- **LGU+ 클라우드 UI**: 솔루션 구축 프로젝트, SDK 개발 (2020-2022)

### 신규 단말 정합
- **Humax UC1600 / UC2600**: KDMC용 XCAS STB 정합 (2012-2014)
- **LG SX730**: KDMC용 XCAS STB 정합 (2012-2013)
- **Samsung SMT5012**: KDMC / CCS 충북방송 XCAS STB 정합 (2013)
- **LG CNS AllinOne**: 딜라이브 UHD STB 개발 (2016-2017)
- **Humax U300**: TBroad향 UHD STB 개발 (2017)
- **Humax UC3300**: HCN / LGHV OCAP 임차망 개발 (2021-2023)
- **Manila MIRAELITE**: MHP 단말 성능 튜닝 및 이슈 지원 (2018-2019)

### 서비스 전환/고도화
- **JCN STB MW 및 EPG CAS/XCAS 전환**: LGHV 신호 전환 (JCN 전 단말 대상, 2017-2019)
- **충북방송 CCS 전환**: LGHV 신호 전환 (전 단말 대상, 2021)
- **TBroad 서비스 고도화**: SKB CI/BI 변경 및 SKB 서비스 적용 (2020)
- **8VSB 양방향 STB 개발**: 아날로그 수신기 대체 8VSB 수신 기능 정합 (2017)
- **신규 RCU 서비스 정합**: 신규 리모컨 정합 (전 단말 대상, 2019)

---

## 아키텍처

OCAP 기반 케이블 STB 소프트웨어의 일반적인 레이어 구조입니다.

```
┌──────────────────────────────────────────────────────────────┐
│                    Java Applications                          │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────────┐ │
│  │  EPG   │ │  VOD   │ │  Push  │ │ Market │ │  Test App  │ │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────────┘ │
├──────────────────────────────────────────────────────────────┤
│                 Middleware (OCAP / MHP)                 ◀ 담당 │
│  ┌──────────────────────────────────────────────────────┐    │
│  │  Core Modules                                        │    │
│  │  ┌──────────┐ ┌──────────┐ ┌────────┐ ┌───────────┐ │    │
│  │  │ Windmill │ │  Wind3   │ │ Image  │ │ CAS/XCAS  │ │    │
│  │  │  (UI)    │ │(CloudUI) │ │ Cloud  │ │  Module   │ │    │
│  │  └──────────┘ └──────────┘ └────────┘ └───────────┘ │    │
│  │  ┌──────────┐ ┌──────────┐ ┌────────┐ ┌───────────┐ │    │
│  │  │  DVB-SI  │ │ Channel  │ │ Tuner  │ │  Network  │ │    │
│  │  │  Parser  │ │ Manager  │ │ Control│ │  Manager  │ │    │
│  │  └──────────┘ └──────────┘ └────────┘ └───────────┘ │    │
│  └──────────────────────────────────────────────────────┘    │
├──────────────────────────────────────────────────────────────┤
│                    Porting Layer (PL)                          │
├──────────────────────────────────────────────────────────────┤
│                   Manufacturer SDK                            │
│         (Humax / Samsung / LG / MIRAE / ...)                 │
├──────────────────────────────────────────────────────────────┤
│                      Drivers                                  │
├──────────────────────────────────────────────────────────────┤
│                      Hardware                                 │
│         (SoC, Tuner, HDMI, RF, Smartcard, ...)               │
└──────────────────────────────────────────────────────────────┘
```

주요 업무 범위: M/W 모듈 개발, 신규 단말 Bring-up, 테스트 애플리케이션 작성, 정합 가이드 제공, 이슈 선제적 확인 및 조치

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **언어** | C, C++, Java |
| **플랫폼** | Linux (임베디드), OCAP, MHP |
| **CAS** | XCAS, CAS 정합 |
| **프로토콜** | DVB-SI, 8VSB, RF Overlay |
| **UI 엔진** | Windmill, Wind3 (Command Cloud), Image Cloud |
| **빌드** | Makefile, Jenkins CI |

- **OCAP** (OpenCable Application Platform) — CableLabs 정의, Java 기반 케이블 STB 미들웨어 표준. DVB-MHP 기반 북미 확장
- **MHP** (Multimedia Home Platform) — DVB 인터랙티브 디지털 TV 오픈 미들웨어 표준 (ETSI TS 102 796). Java VM 기반 하드웨어 독립 실행 환경
- **XCAS** (eXchangeable CAS) — 다운로드 가능 제한수신 시스템. 양방향 케이블 네트워크 통한 CAS S/W 다운로드·갱신 (한국 표준)
- **DVB-SI** (Service Information) — DVB 비트스트림 서비스 정보 표준 (ETSI EN 300 468). EPG 및 수신기 자동 튜닝

---

## 해결한 문제

### 1. 다종 단말 플랫폼 대응
**문제**: Humax, Samsung, LG 등 제조사별로 상이한 하드웨어/소프트웨어 환경에서 동일 서비스 제공 필요

**해결**: 플랫폼 추상화 레이어를 설계하여 미들웨어 코어와 단말별 포팅 레이어를 분리, 신규 단말 정합 기간 단축

### 2. 다수 MSO 서비스 커스터마이징
**문제**: TBroad, 제주방송, LGHV, 딜라이브 등 사업자별 상이한 서비스 요구사항

**해결**: 설정 기반 서비스 분기 구조를 적용하여 공통 코드베이스에서 사업자별 서비스 차별화 구현

### 3. CAS/XCAS 신호 전환
**문제**: JCN, 충북방송 등 기존 CAS에서 XCAS로 전환 시 전 단말 호환성 유지 필요

**해결**: 단계적 전환 전략과 하위 호환성 레이어를 적용하여 서비스 중단 없는 전환 달성

### 4. UI/UX 세대 전환
**문제**: Windmill → Wind3 (Command Cloud) → Image Cloud로 UI 기술 세대가 변화하면서 기존 서비스와의 공존 필요

**해결**: 각 세대별 UI 엔진을 모듈화하고 미들웨어 레벨에서 유연하게 전환 가능한 구조 설계

---

## 역할 및 기여

- 신규 단말(Humax, Samsung, LG 등) 미들웨어 정합 및 포팅
- Windmill / Wind3 / Image Cloud UI/UX 서비스 개발
- CAS/XCAS 전환 프로젝트 수행
- MSO별 서비스 커스터마이징 및 배포
- PoC 개발 (CJ Cloud, Charter Demo, Turk Demo)
- 전 단말 대상 공통 기능 개발 (8VSB, RCU, RF Overlay)
- 팀 Jenkins 빌드 환경 구성

---

## 프로젝트 이력 (시간순)

| 기간 | 프로젝트 | 설명 |
|:-----|:---------|:-----|
| 2012.11 - 2013.04 | Humax XCAS STB 정합 (KDMC) | UC1600/UC2600 단말 개발 / 정합 |
| 2012.12 - 2013.05 | LG XCAS STB 정합 (KDMC) | SX730 단말 개발 / 정합 |
| 2013.02 - 2014.02 | TBroad Smart UI/UX 개발 | Windmill UI/UX 적용 (전 단말) |
| 2013.03 - 2013.06 | Samsung XCAS STB 정합 (KDMC) | SMT5012 단말 개발 / 정합 |
| 2013.08 - 2013.12 | CCS 충북방송 XCAS STB 정합 | SMT5012 단말 정합 |
| 2013.09 - 2014.01 | TBroad SO Integration | Windmill 정합 이슈 지원 |
| 2013.12 - 2015.07 | Windmill 고도화 | UI/UX 고도화 (전 단말) |
| 2014.02 - 2014.06 | UC2600 STB Integrator & QA | UC2600 단말 개발 / 정합 |
| 2014.06 - 2015.09 | 제주방송 Windmill | 통합UI 서비스 개발 (전 단말) |
| 2015.04 - 2015.08 | CJ Cloud UI PoC | Wind3 (Command Cloud) PoC |
| 2015.06 - 2016.06 | Humax UHD STB 개발 | 신규 UHD 개발 |
| 2015.09 - 2016.04 | Windmill 고도화 (2015 하반기) | Wind3 적용 UI/UX (전 단말) |
| 2016.05 - 2017.06 | 딜라이브 AllinOne UHD STB | AllinOne UHD 단말 개발 / 정합 |
| 2016.10 - 2017.04 | 딜라이브 마켓 시범서비스 | 신규 Application 정합 |
| 2017.02 - 2017.12 | TBroad Humax UHD STB | U300 단말 개발 / 정합 |
| 2017.05 - 2017.10 | 8VSB 양방향 STB 개발 | 아날로그 수신기 대체 8VSB 정합 |
| 2017.11 - 2019.02 | 제주방송 Image Cloud | Cloud 구축 및 UHD STB 개발 |
| 2017.12 - 2019.03 | JCN CAS/XCAS 전환 | LGHV 신호 전환 (JCN 전 단말) |
| 2018.04 - 2019.04 | TBroad 클라우드 서비스 구축 | Image Cloud 서비스 (DP 대상) |
| 2018.05 - 2018.07 | UHD STB RF Overlay 개발 | RF Overlay 정합 이슈 지원 |
| 2018.08 - 2019.09 | MIRAE Lite | MHP 단말 성능 튜닝 및 이슈 지원 |
| 2019.07 - 2019.12 | 신규 RCU 서비스 정합 | 신규 리모컨 정합 (전 단말) |
| 2020.02 - 2020.07 | TBroad 서비스 고도화 | SKB CI/BI 변경 및 서비스 적용 |
| 2020.09 - 2022.07 | LGU+ 클라우드 UI 솔루션 | Image Cloud SDK 개발 |
| 2021.01 - 2021.03 | Humax HD STB 개발 | UC3300 정합 |
| 2021.03 - 2021.05 | LGHV OCAP 임차망 개발 | UC3300 LGU+ 임차망 서비스 |
| 2021.06 - 2022.07 | LGHV 일체화 프로젝트 | Image Cloud 적용 (전 단말) |
| 2021.07 - 2021.12 | 충북방송 CCS 전환 | LGHV 신호 전환 (전 단말) |
| 2021.08 - 2022.07 | KCTV 제주방송 TV App 고도화 | 신규 Application 개발 정합 |

---

*약 10년간 30여 건의 케이블 TV 셋톱박스 미들웨어 프로젝트를 수행하며, 신규 단말 정합부터 클라우드 서비스 구축까지 STB 소프트웨어 개발의 전 영역을 경험했습니다.*
