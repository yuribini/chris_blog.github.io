---
layout: post
title: "Synology -> Xpenology 이동하며 겪은 문제들"
subtitle: "근 7,8년 잘 사용한 시놀로지 ds218+를 새로운 H/W로 교체하게 됨"
date: 2024-11-24 20:01:00 +0900
background: '/img/posts/nas/nas-bg.jpg'
categories: [NAS, Xpenology]
tags: [Synology, Xpenology, NAS, Migration]
---

## Synology -> Xpenology 이동하며 겪은 문제들

근 7,8년 잘 사용한 시놀로지 ds218+를 새로운 H/W로 교체하게 됨.
이유는 HDD 교체 주기가 다가오기도 했고 photos와 같은 앱들의 성능의 답답함을 많이 느낌.

지금껏 사용해 온 경험으로 시놀로지에 대해 어느정도 잘 알게 되었다고 판단함.
해보고는 싶었지만 여러가지 이유로 시도하지 못했던 Xpenology를 도전해보기로 함.

### 준비물

1. 하드웨어
   - CPU: i3-12100 (12세대)
   - M/B: ASUS PRIME B660M-K D4
   - RAM: 삼성 DDR4-3200 16GB
   - SSD: WD Blue SN570 500GB
   - HDD: WD Red Plus 4TB x 2
   - CASE: 3RSYS L530
   - PSU: 시소닉 FOCUS GOLD GM-550 Modular

2. 소프트웨어
   - Xpenology 7.1 Loader
   - DSM 7.1.1-42962 Update 4
   - VMware Workstation 17 Player

### 설치 과정

1. VMware에 Xpenology 설치
   - VMware에서 새로운 가상머신 생성
   - Xpenology loader ISO 마운트
   - 가상머신 부팅 후 시리얼 넘버 확인

2. 실제 하드웨어로 이전
   - USB에 Xpenology loader 설치
   - BIOS에서 부팅 순서 변경
   - DSM 설치 진행

### 발생한 문제들

1. RAID 구성 문제
   - 기존 RAID1 배열을 그대로 가져오려 했으나 실패
   - 새로운 RAID1 구성 후 데이터 복사 진행

2. 네트워크 설정
   - VMware에서는 정상 동작했으나 실제 하드웨어에서 인식 안됨
   - 드라이버 수동 설치로 해결

3. USB 인식 문제
   - 외장 하드 연결 시 간헐적으로 인식 안되는 현상
   - USB 포트 변경으로 임시 해결

4. Photos 라이브러리 이전
   - 단순 복사로는 메타데이터 손실 발생
   - Hyper Backup으로 해결

### 해결 방법

1. RAID 재구성
```bash
# 기존 디스크 백업
dd if=/dev/sda of=/path/to/backup.img bs=4M

# 새 RAID 구성
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
```

2. 네트워크 드라이버
```bash
# 드라이버 설치
insmod /lib/modules/intel_e1000e.ko

# 네트워크 재시작
synoservicectl --restart pkgctl-NetworkInterface
```

3. Hyper Backup 이전
   - 소스 NAS에서 백업 작업 생성
   - 대상 NAS에서 복원 작업 수행
   - 메타데이터 포함하여 복원

### 성능 비교

1. 파일 전송 속도
   - DS218+: 약 110MB/s
   - Xpenology: 약 180MB/s

2. Photos 인덱싱
   - DS218+: 약 3시간
   - Xpenology: 약 40분

3. Docker 컨테이너 실행
   - DS218+: 평균 30초
   - Xpenology: 평균 10초

### 장단점

장점:
- 하드웨어 선택의 자유로움
- 성능 대폭 향상
- 확장성이 좋음

단점:
- 초기 설정이 복잡함
- 안정성이 상대적으로 떨어짐
- 업데이트가 까다로움

### 결론

Xpenology로의 이전은 복잡하고 시간이 많이 소요되는 작업이었지만,
성능면에서 큰 향상을 얻을 수 있었음.
하지만 안정성과 기술지원 면에서는 공식 시놀로지보다 부족한 점이 있으므로,
이점을 충분히 고려한 후 결정하는 것이 좋음. 