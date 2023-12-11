---
title: Python 고급-데코레이터(Decorator)
date: 2023-12-11 23:58:00 +09:00
categories: [Advanced, Python]
tags:
  [
    Flask,
    Python,
    데코레이터,
    Decorator,
    권태의TechLAB
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

@kt_decorator
def hello():
    print("Hello!")

hello()
```
>위 예제에서 일어나는 일을 순서대로 나열해 보겠다.
>1. 'hello()' 함수를 호출
>2. 데코레이터 'kt_decorator'가 적용되어 있으므로, 실제로는 'wrapper()' 함수가 먼저 호출된다.
>3. 'wrapper()' 함수 내에서 "안녕?" 이 출력된다.
>4. 'wrapper()' 함수 내에서 원래의 'hello()' 함수가 호출되어 "Hello!"가 출력된다.
>5. 'wrapper()'함수 내에서 "빠이"가 출력된다.

### 🤖'func' 은 데코레이터 내부에서 사용되는 변수이고, 데코레이터에 감싸질 함수를 참조함