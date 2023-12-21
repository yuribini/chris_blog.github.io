---
title: Python 표준 라이브러리 - datetime 모듈
date: 2023-12-20 21:01:00 +09:00
categories: [Python, 표준라이브러리]
tags:
  [
    PYTHON,
    표준라이브러리,
    datetime,
    권태의TechLAB,
    datetime.date,
    datetime.time,
    datetime.datetime,
    datetime.timedelta
  ]
---

![PythonStandardLibrary](/images/python표준라이브러리.png)

>이미지 출처:(https://ajaytech.co/what-are-python-libraries/)


# datetime 모듈
> 데이터를 조작할 때, 분석할 때, 웹 애플리케이션등 정말 많은 분야에 정말 많이 사용되는 모듈이다...⭐️x100
- datetime 모듈은 날짜와 시간을 다루기 위한 클래스와 함수를 제공한다.
- time 모듈은 시간만을 단독으로 사용하는 반면 datetime 모듈은 날짜와 시간을 함께 다룰 때 주로 사용한다.

## 1. 'datetime.date' Class
- 날짜를 표현하는 클래스. 
- 날짜 관련 정보를 다루는 데 필수적.
- 날짜계산, 비교, 포맷팅 등 다양한 작업에 사용된다.
- 글로 표현하는 것 보다 코드로 이해하는게 빠르다. 아래에 예시를 참고하자.

```python
from datetime import date

# 날짜 생성
d = date(2024, 1, 1)  # 날짜 생성 2024년 1월 1일


# 날짜 얻기
today = date.today()  # today 메서드를 사용해 현재 날짜 얻기


# 'year','month','day' 속성을 통해 각각 연,월,일 정보에 접근
year = d.year       # 연도
month = d.month     # 월
day = d.day         # 일


# 날짜 포멧팅
date_str = d.strftime("%Y-%m-%d")  # '2024-01-01'


# 날짜 연산
from datetime import timedelta

tomorrow = d + timedelta(days=1)  # 하루 후
yesterday = d - timedelta(days=1)  # 하루 전


# 날짜 비교
is_today = d == date.today()  # 오늘 날짜인지 확인

```

## 2. 'datetime.time' Class
- 시간을 다루는 데 사용되는 클래스.
- 시, 분, 초, 마이크로초와 같이 시간 정보를 다룰 때 사용한다. (날짜는 포함x)
- 글로 표현하는 것 보다 코드로 이해하는게 빠르다. 아래에 예시를 참고하자.

```python
from datetime import time

t = time(12, 30, 45, 123456)  # 12시 30분 45초 123456마이크로초

# 속성 접근
hour = t.hour           # 시
minute = t.minute       # 분
second = t.second       # 초
microsecond = t.microsecond  # 마이크로초

# 시간 포멧팅
time_str = t.strftime("%H:%M:%S.%f")  # '12:30:45.123456'

# 시간 비교
is_noon = t == time(12, 0)  # 정오인지 확인

# 자정(00:00:00.00)을 나타내는 객체 생성
# time()을 인자 없이 호출하면 자정을 나타내는 객체가 생성된다.
midnight = time()  # 자정

```


## 3. 'datetime.datetime' Class
- 날짜와 시간을 함께 다루는 데 사용된다.
- 'datetime.date', 'datetime.time'의 기능을 모두 포함하며, ***날짜와 시간 관련 작업에 가장!! 많이 사용되는 클래스이다.***
- 글로 표현하는 것 보다 코드로 이해하는게 빠르다. 아래에 예시를 참고하자.

```python
from datetime import datetime

# 날짜와 시간 생성
dt = datetime(2024, 1, 1, 12, 30, 45, 123456)  # 2024년 1월 1일 12시 30분 45초 123456마이크로초


# 날짜와 시간 얻기
now = datetime.now()  # 현재 날짜와 시간


# 속성 접근
year = dt.year
month = dt.month
day = dt.day
hour = dt.hour
minute = dt.minute
second = dt.second
microsecond = dt.microsecond


# 날짜와 시간 포멧팅
dt_str = dt.strftime("%Y-%m-%d %H:%M:%S.%f")


# 날짜와 시간 연산
from datetime import timedelta

tomorrow = dt + timedelta(days=1)
yesterday = dt - timedelta(days=1)

# 날짜와 시간 비교
is_past = dt < datetime.now()

# 문자열 파싱으로 날짜와 시간 생성
dt_from_str = datetime.strptime("2023-01-01 12:30", "%Y-%m-%d %H:%M")

```


## 4. 'datetime.timedelta' Class
- timedelta 클래스는 두개 날짜, 두개 시간 사이의 차이(기간)를 표현하는 데 사용된다.
- ***정말 헷갈리고 암산하기 힘든 날짜계산, 시간계산에 사용하는 데 개꿀이다.***
- 글로 표현하는 것 보다 코드로 이해하는게 빠르다. 아래에 예시를 참고하자.

```python
from datetime import timedelta

# 1일 차이
one_day = timedelta(days=1)

# 1시간 30분 차이
one_hour_thirty_minutes = timedelta(hours=1, minutes=30)


# 날짜와 시간 연산
# 현재 시간
now = datetime.now()

# 1일 후
tomorrow = now + one_day

# 1시간 30분 전
one_hour_thirty_minutes_ago = now - one_hour_thirty_minutes

# 기간 비교
is_longer = one_hour_thirty_minutes > one_day  # False

# 기간의 총 시간 계산
total_seconds = one_hour_thirty_minutes.total_seconds()  # 5400.0 초


# 속성 접근
days = one_day.days             # 1
seconds = one_hour_thirty_minutes.seconds  # 5400
```

## 한줄평
- 오늘 공부한 내용은 정말 자주 사용하고 있으면서도 검색하고 찾느라 번거로운 내용이였는데.. 정리를 싹 해 놓으니 속이 다 후련하네.🌚