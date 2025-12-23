# MakeReleaseNote

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Set-top Box Software Release Note PDF Auto-generation Tool

![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-lightgrey)
![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Swing](https://img.shields.io/badge/Swing-007396?logo=java&logoColor=white)

---

## Overview

**MakeReleaseNote** is a Java desktop application that automatically generates release notes in PDF format for cable TV set-top box software.

It reads previous release note PDFs to automatically parse version information and generates standardized release notes with new changes added.

---

## Key Features

### PDF Generation
- **iText Library**: Standardized release note PDF generation
- **Korean Font Support**: Built-in Nanum Gothic font
- **Auto Version Increment**: Automatic MW/Glue version management

### Automation
- **PDF Parsing**: Auto-extract info from previous release notes
- **Drag & Drop**: Easy file loading via drag and drop
- **Auto Filename**: Version-based automatic filename generation

### Multi-site Support
- Multiple cable TV operators supported
- Site-specific template application

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    MakeReleaseNote v1.5                      │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │                   Java Swing UI                         │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │ │
│  │  │  Site/Model  │  │  Version     │  │  Changelog   │  │ │
│  │  │  Selection   │  │  Input       │  │  Editor      │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  │ │
│  └────────────────────────────────────────────────────────┘ │
│                              │                               │
│         ┌────────────────────┴────────────────────┐         │
│         ▼                                         ▼         │
│  ┌──────────────────┐                 ┌──────────────────┐  │
│  │   PDF Parser     │                 │   PDF Generator  │  │
│  │   (iText Read)   │                 │   (iText Write)  │  │
│  └──────────────────┘                 └──────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Java |
| **UI** | Swing (AWT) |
| **PDF** | iText 5.5.7 |
| **I/O** | Apache Commons IO 2.4 |
| **Build** | JAR, EXE (JSmooth) |

---

## Challenges and Solutions

### 1. PDF Text Parsing
**Challenge**: Needed to accurately extract version info and changelog from existing PDFs

**Solution**: Implemented pattern-based parsing logic using iText's PdfTextExtractor for text extraction

### 2. Korean PDF Generation
**Challenge**: Korean characters were broken with default fonts

**Solution**: Embedded Nanum Gothic TTF font in JAR for Korean rendering support

### 3. Version Management Automation
**Challenge**: Human errors from manual version management

**Solution**: Parsed version from filename and PDF content for auto-increment and consistency validation

---

## Role & Contributions

- Java Swing desktop application design and development
- iText PDF generation/parsing module implementation
- Drag and drop interface development
- Windows EXE packaging (JSmooth)

---

## System Requirements

| Item | Requirement |
|------|-------------|
| **Java** | JRE 8 or later |
| **OS** | Windows, macOS |

---

*This project was developed to improve efficiency in cable TV set-top box software release management.*
