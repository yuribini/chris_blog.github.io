---
layout: post
title: "React 상태관리 setState"
subtitle: "React의 상태에 대해 알아보고 공부하며 setState에 대해 좀더 깊게 알고 싶어 작성하게 됨"
date: 2024-12-02 03:08:00 +0900
background: '/img/posts/react/react-bg.jpg'
categories: [React, React_Basic]
tags: [React, setState, 상태관리]
---

## React의 상태관리 setState

React의 상태에 대해 알아보고 공부하며 setState에 대해 좀더 깊게 알고 싶어 작성하게 됨.

state는 컴포넌트가 가지고 있는 동적인 데이터.
입력, 요청 결과, 클릭 등 변하는 데이터를 말함.
상태가 변경되면 React는 자동으로 다시 렌더링 하며 화면에 변경 사항을 반영함.

### setState 기본 사용법

```javascript
this.setState({ count: this.state.count + 1 });
```

### setState는 비동기적으로 동작함

```javascript
// 잘못된 예시
this.setState({ count: this.state.count + 1 });
this.setState({ count: this.state.count + 1 });
// 예상: count가 2 증가
// 실제: count가 1만 증가

// 올바른 예시
this.setState(prevState => ({
  count: prevState.count + 1
}));
this.setState(prevState => ({
  count: prevState.count + 1
}));
// count가 2 증가함
```

### setState 콜백 함수

상태 업데이트 후에 특정 작업을 하고 싶다면 콜백 함수를 사용함

```javascript
this.setState(
  { count: this.state.count + 1 },
  () => {
    console.log('상태가 업데이트됨');
    console.log(this.state.count);
  }
);
```

### setState 객체 병합

setState는 기존 상태와 새로운 상태를 얕은 병합(shallow merge)함

```javascript
// 초기 상태
state = {
  name: 'John',
  age: 25,
  location: 'Seoul'
};

// name만 업데이트
this.setState({ name: 'Mike' });
// 결과: { name: 'Mike', age: 25, location: 'Seoul' }
```

### 함수형 업데이트

이전 상태를 기반으로 업데이트할 때는 함수형 업데이트를 사용하는 것이 안전함

```javascript
// 객체 형태
this.setState({ count: this.state.count + 1 });

// 함수형 업데이트
this.setState(prevState => ({
  count: prevState.count + 1
}));
```

### 주의사항

1. state를 직접 수정하지 말것
   ```javascript
   // 잘못된 예시
   this.state.count = this.state.count + 1;
   
   // 올바른 예시
   this.setState({ count: this.state.count + 1 });
   ```

2. setState 호출은 비동기적임
   - 성능 최적화를 위해 여러 setState 호출을 배치 처리함
   - 즉시 상태가 업데이트되지 않을 수 있음

3. state 업데이트는 병합됨
   - 부분적인 업데이트가 가능함
   - 기존 상태와 새로운 상태를 얕은 병합함

### 성능 최적화

1. 불필요한 렌더링 방지
   ```javascript
   shouldComponentUpdate(nextProps, nextState) {
     return this.state.count !== nextState.count;
   }
   ```

2. 배치 처리 활용
   ```javascript
   // 여러 업데이트를 한번에 처리
   this.setState(prevState => ({
     count: prevState.count + 1,
     total: prevState.total + 1,
     average: (prevState.total + 1) / (prevState.count + 1)
   }));
   ```

React의 setState는 상태 관리의 핵심임.
비동기적 특성과 병합 방식을 이해하고 있어야 예상치 못한 버그를 방지할 수 있음.
특히 이전 상태를 기반으로 업데이트할 때는 함수형 업데이트를 사용하는 것이 안전함. 