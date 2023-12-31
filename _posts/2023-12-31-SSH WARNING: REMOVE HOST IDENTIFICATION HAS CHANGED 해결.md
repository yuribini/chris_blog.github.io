---
title: SSH 접속 오류 WARNING REMOVE HOST IDENTIFICATION HAS CHANGED! 해결
date: 2023-12-31 04:20:00 +09:00
categories: [Linux, Linux_Trouble]
tags: [Linux, 리눅스, Mac, Unix, SSH]
---

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
```

RaspberryPi SD Card를 포멧하고 OS를 다시 설치하였는데.
SSH 접속시 위와 같은 메세지가 발생하며 접속이 되지 않았다.
ß
## 원인

**첫번째 SSH 접속시 클라이언트(접속자)는 서버의 호스트 키를 받아 로컬 PC에 저장** 하는데 나의 `MAC` 에 등록된 RaspberryPi의 호스트 키가 포멧으로 인해 바뀌었기 때문에 발생한 문제이다.

## 해결방법

```bash
ssh-keygen -R 192.168.xx.xxx
```

나의 경우에는 `/usr/bin/ssh-keygen` 이라는 위치에 SSH 키를 생성하고 관리하는 프로그램이 위치하고 있었다.
파일 내용을 보면 등록된 것들을 볼 수 있을 줄 알았으나, 바이너리 파일로 되어 있었다.
