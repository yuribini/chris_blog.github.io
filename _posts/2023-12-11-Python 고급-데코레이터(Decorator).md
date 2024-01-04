---
title: Python 고급-데코레이터(Decorator)
date: 2023-12-11 23:58:00 +09:00
categories: [Python, Python_Advanced]
tags:
  [
    Flask,
    Python,
    데코레이터,
    라즈베리파이,
    웹서버,
    Decorator,
  ]
---

# 데코레이터

## 1. 데코레이터(Decorator)란?
- 다른 함수를 입력으로 받고 그 함수를 감싸서(wrapper) 새로운 함수를 반환하는 함수
- 이 감싸는 함수는 원래 함수를 호출하기 전후에 추가적인 작업을 수행할 수 있음 

## 2. 사용 방법
- '@' 기호와 함께 함수 정의 바로 위에 작성한다. 해당 함수를 데코레이터 함수로 "감싸겠다"라는 의미이다.

## 3. 동작 방식
- 데코레이터가 적용된 함수(아래 'say_hello()')를 호출하면, 실제로는 데코레이터 내부의 감싸는 함수('wrapper()')가 먼저 호출된다.
- 'wrapper()' 함수 내부에서 원래의 함수 'hello'가 호출되기 전후로 추가 작업을 수행할 수 있다.
- 원래 함수의 동작은 그대로 유지하면서 추가적인 기능을 덧붙일 수 있다.

```python
def kt_decorator(func):
    def wrapper():
        print("안녕?")
        func()
        print("빠이")
    return wrapper

@kt_decorator
def hello():
    print("Hello!")

hello()
```
>위 예제에서 일어나는 일을 순서대로 나열해 보자면..
>1. 'hello()' 함수를 호출
>2. 데코레이터 'kt_decorator'가 적용되어 있으므로, 실제로는 'wrapper()' 함수가 먼저 호출된다.
>3. 'wrapper()' 함수 내에서 "안녕?" 이 출력된다.
>4. 'wrapper()' 함수 내에서 원래의 'hello()' 함수가 호출되어 "Hello!"가 출력된다.
>5. 'wrapper()'함수 내에서 "빠이"가 출력된다.



```python
def wrapper():
    # 데코레이터의 추가적인 작업
    func()  # 원래 함수 호출
    # 추가 작업 계속
```
### 🤖'func' 은 데코레이터 내부에서 사용되는 변수이고, 데코레이터에 감싸질 함수를 참조함

## 4. 실용적인 예제(Flask)
- 아래에 웹 페이지 요청이 들어올 때마다 간단한 메세지를 출력하는 웹 서버 예제를 살펴보자.
- 사용자가 웹으로 '(주소)/'에 접근하면, 'home' 함수가 호출되고 "Welcome to the Home Page!"라는 메세지를 보여준다.
- 'log_request' 데코레이터가 'home' 함수에 적용되어 'home'함수가 호출될 때 "Request received for:home"라는 로그 메세지가 콘솔에 출력된다.

```python
from flask import Flask

app = Flask(__name__)

def log_request(func):
    def wrapper(*args, **kwargs):
        print(f"Request received for: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@app.route('/')
@log_request
def home():
    return "Welcome to the Home Page!"

if __name__ == '__main__':
    app.run(debug=True)
```

### step1. Flask 초기화
  ```python
  app = Flask(__name__)
  ```
  - Flask 앱 생성
  - '__ _name___'은 현재 파일을 나타낸다.

### step2. 데코레이터 정의
  ```python
  def log_request(func):
    def wrapper(*args, **kwargs):
        print(f"Request received for: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper
  ```
  - 'log_request'가 데코레이터 함수. 다른 함수를 감싸고 있고, 추가적인 작업을 수행한다.
  - 'wrapper'함수는 실제로 데코레이터가 적용될 함수('home')을 실행한다.
  - '*args'와 '**kwargs'는 모든 종류의 인자를 받을 수 있도록 한다.

### step3. 라우트 설정, 데코레이터 적용
```python
@app.route('/')
@log_request
def home():
    return "Welcome to the Home Page!"
```
  - '@app.route('/')'는 Flask의 라우팅 데코레이터로, root URL('/')에 대한 요청을 'home()'함수로 연결한다.
  - '@log_request'는 'log_request' 데코레이터를 'home' 함수에 적용한다.

### step4. 앱실행
  ```python
  if __name__ == '__main__':
    app.run(debug=True)
```
- 스크립트가 직접 실행될 때만 Flask 서버를 시작하도록 한다.
- 'debug=True'는 디버그 정보를 제공하게 한다.