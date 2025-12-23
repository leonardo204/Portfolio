# Android NAT-PMP

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> NAT-PMP (NAT Port Mapping Protocol) Implementation Library for Android Set-top Box

![Platform](https://img.shields.io/badge/platform-Android-3DDC84)
![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)

---

## Overview

**Android NAT-PMP** is a NAT-PMP protocol implementation library for NAT traversal in Android set-top box environments.

It enables set-top boxes behind NAT gateways (routers) to obtain external IP addresses and perform UDP/TCP port mapping for bidirectional communication.

---

## Key Features

### NAT-PMP Protocol
- **External IP Acquisition**: Query public IP from gateway
- **Port Mapping**: Automatic UDP/TCP port mapping
- **Lifetime Management**: Automated mapping renewal and release

### Network Management
- **Network State Monitoring**: Connection/disconnection event detection
- **Auto Reconnection**: Mapping reset on network recovery
- **Gateway Auto-detection**: RFC1918 address-based detection

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                 Android Set-top Box                      │
│  ┌───────────────────────────────────────────────────┐  │
│  │              NatPmpManager                         │  │
│  │  ┌─────────────┐  ┌─────────────┐                 │  │
│  │  │ External IP │  │ Port Mapper │                 │  │
│  │  │   Request   │  │  (UDP/TCP)  │                 │  │
│  │  └─────────────┘  └─────────────┘                 │  │
│  └───────────────────────────────────────────────────┘  │
│                          │                               │
│                    NAT-PMP (UDP)                         │
│                          │                               │
│                          ▼                               │
│  ┌───────────────────────────────────────────────────┐  │
│  │            NAT Gateway (Router)                    │  │
│  │         External IP: xxx.xxx.xxx.xxx              │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Platform** | Android (API 21+) |
| **Language** | Java |
| **Network** | UDP DatagramSocket |
| **Protocol** | NAT-PMP (RFC 6886) |

---

## Challenges and Solutions

### 1. Bidirectional Communication in NAT Environment
**Challenge**: Set-top boxes behind NAT are inaccessible from external networks

**Solution**: Request port mapping to router via NAT-PMP to secure externally accessible ports

### 2. Network State Change Handling
**Challenge**: Mapping information lost on network reconnection

**Solution**: Monitor network state via NetworkStateManager and automatically reset mappings on reconnection

---

## Role & Contributions

- NAT-PMP protocol client implementation
- Network state management system development
- Port mapping auto-renewal logic implementation
- Set-top box platform integration

---

*This project was developed to support IP VOD services for cable TV set-top boxes.*
