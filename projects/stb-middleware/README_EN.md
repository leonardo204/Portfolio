# STB Middleware Integration & Development

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Cable TV Set-Top Box Middleware Development & Device Integration (2012-2022)

![Language](https://img.shields.io/badge/C-A8B9CC?logo=c&logoColor=white)
![Language](https://img.shields.io/badge/C++-00599C?logo=cplusplus&logoColor=white)
![Language](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Platform](https://img.shields.io/badge/Embedded-007ACC)

---

## Overview

- **Period**: 2012 - 2022 (~10 years)
- **Domain**: Cable TV Set-Top Box (STB) middleware development & device integration
- **Scale**: 30+ formal projects
- **Target MSOs**: TBroad, Jeju Broadcasting, LGHV, DLive, CCS, KCTV, HCN, JCN, etc.
- **Scope**: New device integration · UI/UX service development · CAS/XCAS migration · Cloud service deployment

### Affiliation & Background

- **Alticast** (2012-2019)
  - First in the world to commercialize DVB-MHP, OCAP, and ACAP middleware
  - Platform deployed on 50M+ devices across 25+ pay-TV operators globally
  - Full-stack pay-TV software: STB middleware, SDP, UI/UX solutions, CAS/DRM, broadcast systems
- **Altimedia** (2019-2025) — Spun off from Alticast, inherited full media platform business (domestic + Europe/Asia clients, Vietnam subsidiary). Joined KT Group
- **KT Altimedia** (2025-Present) — Rebranded

### UI/UX Platform Evolution

| Generation | Platform | Approach |
|:-----------|:---------|:---------|
| 1st | **Windmill** | Graphics engine enabling 2D/3D high-quality animation on low-spec STBs |
| 2nd | **Wind3 / Command Cloud** | Cloud command-based UI |
| 3rd | **Image Cloud** | Cloud rendering + lightweight presentation layer on STB |

> Core challenge: Enabling coexistence of legacy devices and next-gen cloud services at the middleware level

---

## Key Projects

### Windmill / Wind3 UI/UX Services
- **TBroad Windmill**: Smart UI/UX deployment (all devices, 2013-2015)
- **Windmill Advanced**: UI/UX enhancement project (all devices, 2013-2016)
- **Jeju Broadcasting Windmill**: Unified UI service development (all devices, 2014-2015)
- **Wind3 (Command Cloud)**: CJ Cloud UI PoC and UI/UX project deployment (2015-2016)

### Image Cloud Services
- **Jeju Broadcasting Image Cloud**: Cloud deployment and UHD STB development (all devices, 2017-2019)
- **TBroad Image Cloud**: Cloud service deployment (DP target, 2018-2019)
- **LGHV Image Cloud**: Unified project (all devices, 2021-2022)
- **LGU+ Cloud UI**: Solution deployment project, SDK development (2020-2022)

### New Device Integration
- **Humax UC1600 / UC2600**: XCAS STB integration for KDMC (2012-2014)
- **LG SX730**: XCAS STB integration for KDMC (2012-2013)
- **Samsung SMT5012**: XCAS STB integration for KDMC / CCS (2013)
- **LG CNS AllinOne**: DLive UHD STB development (2016-2017)
- **Humax U300**: TBroad UHD STB development (2017)
- **Humax UC3300**: HCN / LGHV OCAP leased network development (2021-2023)
- **Manila MIRAELITE**: MHP device performance tuning and support (2018-2019)

### Service Migration & Enhancement
- **JCN CAS/XCAS Migration**: LGHV signal transition (all JCN devices, 2017-2019)
- **CCS Broadcasting Transition**: LGHV signal transition (all devices, 2021)
- **TBroad Service Enhancement**: SKB CI/BI changes and service deployment (2020)
- **8VSB Bidirectional STB**: Analog receiver replacement with 8VSB reception (2017)
- **New RCU Service Integration**: New remote control integration (all devices, 2019)

---

## Architecture

General layer structure of OCAP-based cable STB software.

```
┌──────────────────────────────────────────────────────────────┐
│                    Java Applications                          │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────────┐ │
│  │  EPG   │ │  VOD   │ │  Push  │ │ Market │ │  Test App  │ │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────────┘ │
├──────────────────────────────────────────────────────────────┤
│                 Middleware (OCAP / MHP)              ◀ My Role │
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

Key responsibilities: M/W module development, new device bring-up, test application development, integration guides, proactive issue identification & resolution

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | C, C++, Java |
| **Platform** | Linux (Embedded), OCAP, MHP |
| **CAS** | XCAS, CAS integration |
| **Protocol** | DVB-SI, 8VSB, RF Overlay |
| **UI Engine** | Windmill, Wind3 (Command Cloud), Image Cloud |
| **Build** | Makefile, Jenkins CI |

- **OCAP** (OpenCable Application Platform) — CableLabs-defined Java-based cable STB middleware standard. Extended from DVB-MHP for North American cable
- **MHP** (Multimedia Home Platform) — DVB open middleware for interactive digital TV (ETSI TS 102 796). Hardware-independent runtime on Java VM
- **XCAS** (eXchangeable CAS) — Downloadable conditional access system. CAS S/W download & renewal over bidirectional cable networks (Korean standard)
- **DVB-SI** (Service Information) — Service information standard for DVB bitstreams (ETSI EN 300 468). EPG and automatic receiver tuning

---

## Challenges and Solutions

### 1. Multi-vendor Device Support
**Challenge**: Needed to deliver consistent services across vastly different hardware/software environments from Humax, Samsung, LG, and other manufacturers

**Solution**: Designed a platform abstraction layer separating the middleware core from device-specific porting layers, significantly reducing integration time for new devices

### 2. Multi-MSO Service Customization
**Challenge**: Each MSO (TBroad, Jeju Broadcasting, LGHV, DLive) had different service requirements

**Solution**: Implemented configuration-based service branching to enable per-operator service differentiation from a shared codebase

### 3. CAS/XCAS Signal Migration
**Challenge**: Required backward compatibility across all devices during CAS to XCAS migration for JCN and CCS Broadcasting

**Solution**: Applied phased migration strategy with backward compatibility layer, achieving zero-downtime transitions

### 4. UI/UX Generation Transition
**Challenge**: UI technology evolved through Windmill → Wind3 (Command Cloud) → Image Cloud generations, requiring coexistence with legacy services

**Solution**: Modularized each UI engine generation with flexible switching at the middleware level

---

## Role & Contributions

- New device (Humax, Samsung, LG, etc.) middleware integration and porting
- Windmill / Wind3 / Image Cloud UI/UX service development
- CAS/XCAS migration project execution
- Per-MSO service customization and deployment
- PoC development (CJ Cloud, Charter Demo, Turk Demo)
- Common feature development across all devices (8VSB, RCU, RF Overlay)
- Team Jenkins build environment setup

---

## Project History (Chronological)

| Period | Project | Description |
|:-------|:--------|:------------|
| 2012.11 - 2013.04 | Humax XCAS STB Integration (KDMC) | UC1600/UC2600 device development / integration |
| 2012.12 - 2013.05 | LG XCAS STB Integration (KDMC) | SX730 device development / integration |
| 2013.02 - 2014.02 | TBroad Smart UI/UX Development | Windmill UI/UX deployment (all devices) |
| 2013.03 - 2013.06 | Samsung XCAS STB Integration (KDMC) | SMT5012 device development / integration |
| 2013.08 - 2013.12 | CCS Broadcasting XCAS STB Integration | SMT5012 device integration |
| 2013.09 - 2014.01 | TBroad SO Integration | Windmill integration issue support |
| 2013.12 - 2015.07 | Windmill Advanced Features | UI/UX enhancement (all devices) |
| 2014.02 - 2014.06 | UC2600 STB Integrator & QA | UC2600 device development / integration |
| 2014.06 - 2015.09 | Jeju Broadcasting Windmill | Unified UI service development (all devices) |
| 2015.04 - 2015.08 | CJ Cloud UI PoC | Wind3 (Command Cloud) PoC |
| 2015.06 - 2016.06 | Humax UHD STB Development | New UHD development |
| 2015.09 - 2016.04 | Windmill Advanced (2H 2015) | Wind3 UI/UX deployment (all devices) |
| 2016.05 - 2017.06 | DLive AllinOne UHD STB | AllinOne UHD device development / integration |
| 2016.10 - 2017.04 | DLive Market Pilot Service | New application integration |
| 2017.02 - 2017.12 | TBroad Humax UHD STB | U300 device development / integration |
| 2017.05 - 2017.10 | 8VSB Bidirectional STB | 8VSB reception integration (all devices) |
| 2017.11 - 2019.02 | Jeju Broadcasting Image Cloud | Cloud deployment and UHD STB development |
| 2017.12 - 2019.03 | JCN CAS/XCAS Migration | LGHV signal transition (all JCN devices) |
| 2018.04 - 2019.04 | TBroad Cloud Service Deployment | Image Cloud service (DP target) |
| 2018.05 - 2018.07 | UHD STB RF Overlay Development | RF Overlay integration support |
| 2018.08 - 2019.09 | MIRAE Lite | MHP device performance tuning and support |
| 2019.07 - 2019.12 | New RCU Service Integration | New remote control integration (all devices) |
| 2020.02 - 2020.07 | TBroad Service Enhancement | SKB CI/BI changes and service deployment |
| 2020.09 - 2022.07 | LGU+ Cloud UI Solution | Image Cloud SDK development |
| 2021.01 - 2021.03 | Humax HD STB Development | UC3300 integration |
| 2021.03 - 2021.05 | LGHV OCAP Leased Network | UC3300 LGU+ leased network service |
| 2021.06 - 2022.07 | LGHV Unification Project | Image Cloud deployment (all devices) |
| 2021.07 - 2021.12 | CCS Broadcasting Transition | LGHV signal transition (all devices) |
| 2021.08 - 2022.07 | KCTV Jeju Broadcasting TV App | New application development / integration |

---

*Over approximately 10 years and 30+ cable TV set-top box middleware projects, gained comprehensive experience across the full spectrum of STB software development — from new device integration to cloud service deployment.*
