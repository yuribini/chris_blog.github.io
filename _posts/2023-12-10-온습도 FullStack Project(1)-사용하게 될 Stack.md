---
title: 온습도 FullStack Project-각 Stack에 대해
date: 2023-12-09 23:58:00 +09:00
categories: [Raspberry Pi, Project]
tags:
  [
    라즈베리파이,
    프로젝트,
    온습도,
    DHT22,
    AM2302,
    Raspberry Pi
  ]
---

# 온습도 FullStack Project-각 Stack에 대해

## 1. Hardware
- RaspberryPi Model3 B
  - 프로젝트의 물리적 기반으로 센서, LED 등의 여러가지 장치를 연결하고 제어한다.
- DHT22 or AM2302
  - 온습도 측정 센서. 라즈베리파이와 연결하여 온습도 데이터를 계측한다.

## 2. OS
- Raspbian OS Lite (레거시)
  - 하드웨어 관리, 사용자와 소프트웨어 간의 인터페이스 역할을 수행한다.

## 3. Web Framework
- Flask
  - 웹 앱을 쉽고 빠르게 개발할 수 있고, 복잡한 백엔드 로직을 간소화 할 예정이다.

## 4. Application Server
- uWSGI
  - 웹 서버와 Flask 앱 간의 통신을 중계, 복잡한 네트워크 요청을 처리한다.

## 5. Web Server
- Nginx
  - 사용자 요청을 받아들이고, 앱 서버로 전달하는 역할을 한다.

## 6. Virtual Environment
- 파이썬 가상 환경
  - 파이썬 버전과 라이브러리를 관리하는 역할을 한다.

## 7. Database
- SQLite3
  - 경량 데이터베이스. 서버 없이 작동이 가능하며 단일 파일로 관리하기 때문에 설정이 간단하고 관리가 쉽다.
  - 온습도 데이터와 같은 시계열 데이터를 효과적으로 저장 및 검색이 가능하다.
  - SQL 표준을 대부분 지원한다.