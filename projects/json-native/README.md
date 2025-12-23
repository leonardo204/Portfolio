# JSON Native

🌐 **Language**: [한국어](./README.md) | [English](./README_EN.md)

> 경량 C 언어 JSON 파서 라이브러리 with JNI 지원

![Language](https://img.shields.io/badge/C-A8B9CC?logo=c&logoColor=white)
![Android](https://img.shields.io/badge/Android%20NDK-3DDC84?logo=android&logoColor=white)

---

## 개요

**JSON Native**는 임베디드 시스템 및 Android NDK 환경을 위해 개발된 경량 JSON 파서 라이브러리입니다.

최소한의 메모리 사용으로 JSON 파싱 및 생성을 지원하며, JNI를 통해 Java/Android 애플리케이션에서 직접 사용할 수 있습니다.

---

## 주요 기능

### JSON 파싱
- **완전한 JSON 지원**: Object, Array, String, Number, Boolean, Null
- **스트리밍 파싱**: 대용량 JSON 처리 가능
- **해시 기반 검색**: O(1) 키 검색 성능

### 크로스 플랫폼
- **JNI 바인딩**: Android/Java 네이티브 인터페이스
- **임베디드 지원**: 저사양 시스템 최적화
- **메모리 효율**: 커스텀 메모리 할당자

---

## API 구조

```c
// JSON 파싱
json_element_t* json_parse(const char* json_string);

// 값 접근
json_element_t* json_get(json_element_t* obj, const char* key);
const char* json_get_string(json_element_t* elem);
int json_get_int(json_element_t* elem);

// 메모리 해제
void json_free(json_element_t* elem);
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| **언어** | C (C99) |
| **빌드** | Makefile, NDK-build |
| **플랫폼** | Linux, Android, 임베디드 |
| **인터페이스** | JNI (Java Native Interface) |

---

## 해결한 문제

### 1. 메모리 제약 환경
**문제**: 셋톱박스/임베디드 환경의 제한된 메모리

**해결**: 커스텀 메모리 풀 및 효율적인 자료구조로 최소 메모리 사용

### 2. Java 연동
**문제**: C 라이브러리를 Android 앱에서 사용 필요

**해결**: JNI 래퍼 구현으로 Java에서 네이티브 JSON 파서 직접 호출 가능

---

## 역할 및 기여

- C 언어 JSON 파서 알고리즘 구현
- 해시 테이블 기반 오브젝트 검색 최적화
- JNI 바인딩 개발
- Android NDK 빌드 시스템 구성

---

*이 프로젝트는 셋톱박스 플랫폼의 고성능 JSON 처리를 위해 개발되었습니다.*
