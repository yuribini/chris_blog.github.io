---
title: macOS(Linux) SD Card Backup 방법
date: 2023-12-12 23:57:00 +09:00
categories: [Linux, Linux_Basic]
tags:
  [
    macOS,
    Linux,
    SD Card Backup,
    SD 카드 백업,
    라즈베리파이 백업
  ]
---

# Mac에서 SD 카드 백업 방법

## 1단계: SD 카드 파티션 찾기
Mac에 SD 카드를 연결한 후 `diskutil list` 명령어를 사용해 모든 디스크와 파티션의 목록을 확인할 수 있다. SD 카드의 디바이스 경로(예: `/dev/disk8`)를 찾는다.

## 2단계: SD 카드 백업하기
`dd` 명령어를 사용하여 SD 카드의 백업 이미지를 생성한다. 이 명령어는 잘못 사용하면 데이터 손실을 일으킬 수 있다고 하므로 주의하여 입력하도록 한다.

예시:
```bash
sudo dd if=/dev/disk8 of=/Users/kwontaewoong/rpi_backup/2023/20231213.dmg
```
<br>

>❌ 주의사항
>- if (입력 파일)와 of (출력 파일) 경로가 정확한지 확인
>- SD 카드의 크기와 속도에 따라 백업 과정에 많은 시간이 소요되므로 명령어 실행 후 다른 무언가를 하길 권함

<br>
<br>

## 3단계(별첨) : dmg 이미지를 SD Card에 쓰기
```bash
sudo dd if=/Users/kwontaewoong/rpi_backup/2023/20231213.dmg of=/dev/disk8
```