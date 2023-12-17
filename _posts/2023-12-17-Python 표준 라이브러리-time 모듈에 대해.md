---
title: Python 표준 라이브러리 - time 모듈
date: 2023-12-17 22:01:00 +09:00
categories: [Python, 라이브러리]
tags:
  [
    PYTHON,
    표준라이브러리,
    time,
    time모듈,
    파이썬time,
    권태의TechLAB,
    time.time(),
    time.strftime,
    time.strptime,
    time.localtime,
    time.gmtime
  ]
---

# time 모듈
- Python 을 사용하다 보면 time이라는 모듈을 자주 사용하게 되는데 이에 대한 개념을 정확히 다지려고 한다.

## 1. 'time.sleep()'
- 'time' 모듈에서 가장 많이 사용되는 매우 중요한 함수.
- 프로그램을 지정된 시간 동안 일시정지 시키는 데 사용된다.
- 프로세스 지연, 네트워크 요청 지연 등의 과부하를 방지하기 위한 일시적은 지연을 생성하는데 많이 사용된다.

[기본구조]
```python
time.sleep(seconds)
```
>여기서 'seconds'는 프로그램이 일시 중지될 시간을 초 단위로 입력한다.

<br>

[간단 예제]
```python
import time

for i in range(5):
    print(f"메시지 {i+1}")
    time.sleep(1)  # 1초 동안 프로그램을 일시 중지
```

## 2. 'time.time()'
- 'time.time()' 함수는 현재 시간을 Unix 타임스탬프 형식으로 반환한다. (Unix 타임스탬프는 1970년 1월 1일 00:00:00 UTC(협정 세계시)부터 현재까지 경과한 시간을 초 단위로 나타낸 값)
- 성능 측정, DB에 타임스탬프 기록 등에 사용된다.

[간단 예제]
```python
import time

start_time = time.time()  # 시작 시간 기록

# 시간이 걸리는 어떤 작업을 수행
for i in range(1000000):
    pass

end_time = time.time()  # 종료 시간 기록
run_time = end_time - start_time  # 경과 시간 계산

print(f"코드 실행에 걸린 시간: {run_time}초")
```

> 이 코드는 'start_time'에 작업 시작 전의 시간을 기록하고, 'end_time'에 작업이 끝난 후의 시간을 기록하여 두 시간의 차이를 계산한다.


## 3. 'time.strftime()'
- time tuple을 문자열로 변환할 때, time 구조체를 특정 형식의 문자열로 변환할 때 사용한다.
- 쉽게말해 time.localtime() 등의 함수로부터 반환값으로 얻은 time 구조체를 다른 형식의 문자열로 변환하고 싶을 때 사용한다.
- 사용법 : 'time.strftime(원하는 포멧, 변환할 time 구조체)
- 'strftime' 에서 'f'는 "format"의 약자이다. 즉, "string format time"의 줄임말이다.

[간단 예제]
```python
import time

current_time = time.localtime()  # 현재 시간 구조체
formatted_time = time.strftime("%Y-%m-%d %H:%M:%S", current_time)
print("현재 시간:", formatted_time)
```
>이 코드는 'time.localtime()' 함수로 현재 시간을 'time tuple' 형태로 반환하고, 'time.strftime()' 함수로 "YYYY-MM-DD HH:MM:SS" 형식의 문자열로 변환하여 출력한다.


## 4.time.strptime()
- 문자열을 해석하여 'time' 구조체로 변환한다.
- 사용법 : 'time.strptime(파싱할 문자열(string), 포멧)
- "string parse time"의 줄임말로 문자열을 파싱해서 시간데이터로 변환하는 기능이다.

[간단 예제]
```python
import time

time_string = "2023-12-17 15:30:00"
time_struct = time.strptime(time_string, "%Y-%m-%d %H:%M:%S")
print("해석된 time tuple:", time_struct)
```
