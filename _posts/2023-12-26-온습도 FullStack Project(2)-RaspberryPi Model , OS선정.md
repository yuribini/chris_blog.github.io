---
title: 2023-12-29-온습도 FullStack Project(2)-RaspberryPi Model , OS선정
date: 2023-12-29 00:02:00 +09:00
categories: [Raspberry Pi, Project]
tags:
  [라즈베리파이, 프로젝트, 온습도, DHT22, AM2302, Raspberry Pi, 권태의TechLAB]
---

# Raspberry Pi Model 선정

## 👉🏻[(1편)사용할 Stack 정리](https://yuribini.github.io/posts/%EC%98%A8%EC%8A%B5%EB%8F%84-FullStack-Project-%EA%B0%81-Stack%EC%97%90-%EB%8C%80%ED%95%B4/)

<br>

![Hardware](/images/Hardware.png)

## 1. RaspberryPi Model

- 라즈베리파이 모델을 구매하기 전에 아래 표를 참고하여 선정해보자.
- 참고로 내 경우에는 우연히 아는 형에게 'Model 3B'를 얻게 되어 사용하게 되었고 'Model 3B'의 사양으로 해당 프로젝트를 진행하는데에 전혀 무리가 없는 수준이었다.

<br>

| 모델                    | 출시일      | CPU                                           | 메모리                    | 저장공간  | 영상출력                               | 가격    |
| ----------------------- | ----------- | --------------------------------------------- | ------------------------- | --------- | ---------------------------------------- | ------- |
| Raspberry Pi Zero       | 2015년 11월 | 1GHz ARM1176JZF-S (Broadcom BCM2835)          | 512MB                     | microSD   | Mini HDMI                                | $5      |
| Raspberry Pi Zero W     | 2017년 2월  | 1GHz ARM1176JZF-S (Broadcom BCM2835)          | 512MB                     | microSD   | Mini HDMI, 802.11n Wi-Fi, Bluetooth 4.1  | $10     |
| Raspberry Pi 3          | 2016년 2월  | 1.2GHz Cortex-A53 64-bit (Broadcom BCM2837)   | 1GB                       | microSD   | HDMI, 10/100Mbps 이더넷                  | $35     |
| Raspberry Pi 3 Model B+ | 2018년 3월  | 1.4GHz Cortex-A53 64-bit (Broadcom BCM2837B0) | 1GB                       | microSD   | HDMI, 10/100/1000Mbps 이더넷 (USB 2.0)   | $35     |
| Raspberry Pi 4          | 2019년 6월  | 1.5GHz Broadcom BCM2711 Quad-core             | 1GB, 2GB, 4GB, 8GB LPDDR4 | microSD   | 2개의 Micro HDMI, 10/100/1000Mbps 이더넷 | $35부터 |
| Raspberry Pi 4 Model B  | 2020년 10월 | 1.8GHz Broadcom BCM2711 Quad-core             | 2GB, 4GB, 8GB LPDDR4      | microSD   | 2개의 Micro HDMI, 10/100/1000Mbps 이더넷 | $35부터 |
| Raspberry Pi 400        | 2020년 11월 | 1.8GHz Broadcom BCM2711                       | 4GB LPDDR4                | 32GB eMMC | HDMI, 10/100/1000Mbps 이더넷             | $70     |
| Raspberry Pi Pico       | 2021년 1월  | 133MHz RP2040                                 | 264KB SRAM                | 없음      | 없음                                     | $4      |
| Raspberry Pi 5          | 2023년 10월 | 2.4Ghz ARM Cortex-A76 Quad-core | 4GB, 8GB LPDDR4X | MicroSD (고속 SDR104 모드 지원, UHS-I 지원) | 2개의 micro HDMI, 10/100/1000Mbps 이더넷 | $60 부터 |


## 2. OS

![RaspberryPiOS](/images/RaspberryPi_OS.png)

👉 [설치링크](https://www.raspberrypi.com/software/operating-systems/)

- RaspberryPi Lite OS (레거시)를 설치하였다.
- RaspberryPi Lite OS는 GUI가 없는 Headless OS 인데, 불필요한 OS 용량을 줄일 수 있으며 서버로 사용하기에 적합하다. (16GB SD Card를 사용할 예정이다. Headless는 보안, 속도, 안정성 등 그래픽을 포기하면 장점이 꽤 많다.)

