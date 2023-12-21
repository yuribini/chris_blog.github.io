---
title: JavaScript 문법-변수선언, 네이밍 규칙
date: 2023-12-21 23:12:00 +09:00
categories: [JavaScript, JS_Basic]
tags:
  [
    JavaScript,
    JavaScript문법,
    JavaScript기초,
    const,
    let,
    네이밍규칙
  ]
---

![JavaScript](/images/JavaScript.png)

# JavaScript 기초 문법 - 변수 선언과 네이밍 규칙
>JavaScript의 아주 기본적이면서 필수적인 변수 선언과 네이밍 규칙에 대해 알아보았다.

<br>
<br>

## 1. 'let'을 사용한 변수 선언
JavaScript에서 변수를 선언할 때 'let' 키워드를 사용한다. 예를 들어, 

```javascript
let number = 10;
```
과 같이 작성하면, 'number'라는 이름의 변수가 생성되고 값 '10'이 할당된다.
- 사용 시점:값이 변경되지 않는 변수를 선언할 때
- 특징:'let'으로 선언된 변수는 나중에 값을 변경할 수 있다.

<br>

## 2. 'const'를 사용한 상수 선언
>상수는 한 번 할당되면 그 값이 변하지 않는 변수를 의미한다.

'const' 키워드를 사용하여 상수를 선언할 수 있다. 예를 들어,
```javascript
const PI = 3.14;
```
는 'PI'라는 상수에 3.14 값을 할당한다.
- 사용 시점:값이 변경되지 않는 변수를 선언할 떄
- 특징:'const'로 선언된 변수는 재할당이 불가능하다.

<br>

## 3. 네이밍 규칙
- 변수 : 변수를 선언할 때 명명 규칙을 따르는 것이 중요한데, 첫 번째 글자는 소문자를 사용하고, 이후 연결되는 단어의 첫 글자는 대문자를 사용하는 카멜케이스(CamelCase) 방식이 일반적이다. 예를 들어,
```javascript
let myVariableName
```
과 같이 착성한다.

- 상수 : 상수는 일반적으로 대문자로 선언한다. 특히 값이 변경되지 않고 프로그램 전반에 걸쳐 고정적으로 사용되는 상수에 대문자를 사용한다. 예를 들어, 원주율'PI'와 같은 수학적 상수나 환경 설정 값 등이 이에 해당된다.
  - 대문자와 언더스코어(_)를 사용하여 단어를 구분하는 스네이크 케이스(Snake Case) 방식으로 작성하면, 상수임을 더욱 쉽게 인식할 수 있다.

```javascript
const PI = 3.14;
const MAX_USER_COUNT = 100;
```