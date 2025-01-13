---
layout: post
title: "React state immutability(불변성)"
subtitle: "React state에 대해 알아보던 중 immutability 개념이 이해가 잘 안되어 정리하면서 공부함"
date: 2024-11-27 09:43:00 +0900
background: '/img/posts/react/react-bg.jpg'
categories: [React, React_Basic]
tags: [React, State, Immutability, 불변성]
---

## React state immutability(불변성)

React state에 대해 알아보던 중 immutability 개념이 이해가 잘 안되어 정리하면서 공부함.

immutability 은 데이터를 직접 수정하지 않고, 수정이 필요한 경우 새로운 데이터를 만들어내는 방식임.

React에서 불변성을 유지하는 이유는 state가 변경되었음을 React가 감지하고 리렌더링을 하기 위함임.

### 잘못된 예시

```javascript
const user = { name: 'John', age: 25 };
user.name = 'Mike';  // 직접 수정 (X)
```

### 올바른 예시

```javascript
const user = { name: 'John', age: 25 };
const newUser = { ...user, name: 'Mike' };  // 새로운 객체 생성 (O)
```

### 배열의 불변성

1. 요소 추가
```javascript
// 잘못된 예시
const numbers = [1, 2, 3];
numbers.push(4);  // 직접 수정 (X)

// 올바른 예시
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4];  // 새로운 배열 생성 (O)
```

2. 요소 제거
```javascript
// 잘못된 예시
const numbers = [1, 2, 3];
numbers.splice(1, 1);  // 직접 수정 (X)

// 올바른 예시
const numbers = [1, 2, 3];
const newNumbers = numbers.filter(n => n !== 2);  // 새로운 배열 생성 (O)
```

3. 요소 수정
```javascript
// 잘못된 예시
const numbers = [1, 2, 3];
numbers[1] = 20;  // 직접 수정 (X)

// 올바른 예시
const numbers = [1, 2, 3];
const newNumbers = numbers.map(n => n === 2 ? 20 : n);  // 새로운 배열 생성 (O)
```

### 객체의 불변성

1. 속성 추가
```javascript
// 잘못된 예시
const user = { name: 'John' };
user.age = 25;  // 직접 수정 (X)

// 올바른 예시
const user = { name: 'John' };
const newUser = { ...user, age: 25 };  // 새로운 객체 생성 (O)
```

2. 속성 제거
```javascript
// 잘못된 예시
const user = { name: 'John', age: 25 };
delete user.age;  // 직접 수정 (X)

// 올바른 예시
const user = { name: 'John', age: 25 };
const { age, ...newUser } = user;  // 새로운 객체 생성 (O)
```

3. 속성 수정
```javascript
// 잘못된 예시
const user = { name: 'John', age: 25 };
user.age = 26;  // 직접 수정 (X)

// 올바른 예시
const user = { name: 'John', age: 25 };
const newUser = { ...user, age: 26 };  // 새로운 객체 생성 (O)
```

### 중첩된 객체의 불변성

```javascript
const user = {
  name: 'John',
  address: {
    city: 'Seoul',
    country: 'Korea'
  }
};

// 잘못된 예시
user.address.city = 'Busan';  // 직접 수정 (X)

// 올바른 예시
const newUser = {
  ...user,
  address: {
    ...user.address,
    city: 'Busan'
  }
};  // 새로운 객체 생성 (O)
```

### 불변성 유지의 장점

1. 예측 가능한 상태 관리
   - 데이터 변경 추적이 용이함
   - 디버깅이 쉬워짐

2. 성능 최적화
   - React의 가상 DOM 비교 알고리즘이 효율적으로 동작함
   - 불필요한 리렌더링을 방지할 수 있음

3. 부작용 방지
   - 의도하지 않은 데이터 변경을 방지함
   - 코드의 안정성이 높아짐

불변성을 지키는 것이 처음에는 번거로울 수 있지만, 
React 애플리케이션의 안정성과 성능을 위해서는 매우 중요한 개념임.
특히 상태 관리가 복잡해질수록 불변성의 중요성이 더욱 커짐. 