# JSON Native

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> Lightweight C JSON Parser Library with JNI Support

![Language](https://img.shields.io/badge/C-A8B9CC?logo=c&logoColor=white)
![Android](https://img.shields.io/badge/Android%20NDK-3DDC84?logo=android&logoColor=white)

---

## Overview

**JSON Native** is a lightweight JSON parser library developed for embedded systems and Android NDK environments.

It supports JSON parsing and generation with minimal memory usage and can be used directly in Java/Android applications through JNI.

---

## Key Features

### JSON Parsing
- **Complete JSON Support**: Object, Array, String, Number, Boolean, Null
- **Streaming Parsing**: Large JSON file handling
- **Hash-based Lookup**: O(1) key search performance

### Cross Platform
- **JNI Binding**: Android/Java native interface
- **Embedded Support**: Low-spec system optimization
- **Memory Efficient**: Custom memory allocator

---

## API Structure

```c
// JSON Parsing
json_element_t* json_parse(const char* json_string);

// Value Access
json_element_t* json_get(json_element_t* obj, const char* key);
const char* json_get_string(json_element_t* elem);
int json_get_int(json_element_t* elem);

// Memory Free
void json_free(json_element_t* elem);
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | C (C99) |
| **Build** | Makefile, NDK-build |
| **Platform** | Linux, Android, Embedded |
| **Interface** | JNI (Java Native Interface) |

---

## Challenges and Solutions

### 1. Memory Constrained Environment
**Challenge**: Limited memory in set-top box/embedded environments

**Solution**: Custom memory pool and efficient data structures for minimal memory usage

### 2. Java Integration
**Challenge**: Need to use C library in Android apps

**Solution**: JNI wrapper implementation for direct native JSON parser calls from Java

---

## Role & Contributions

- C language JSON parser algorithm implementation
- Hash table-based object lookup optimization
- JNI binding development
- Android NDK build system configuration

---

*This project was developed for high-performance JSON processing on set-top box platforms.*
