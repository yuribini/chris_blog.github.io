---
layout: post
title: "React.lazy 화면 지연 개선"
subtitle: "React.lazy에 대한 공부 기록"
date: 2024-12-06 03:45:00 +0900
background: '/img/posts/react/react-bg.jpg'
categories: [React, React_Basic]
tags: [React, React.lazy, 성능최적화, 지연로딩]
---

## React.lazy에 대한 공부 기록

React로 웹사이트를 만들면, 컴포넌트들이 한번에 로드됨.
만약 화면이 너무 많거나 복잡하면 처음에 로드하는 데 시간이 오래걸리는 문제가 발생함.

React.lazy는 이때 사용되는 유용한 도구임.
필요한 컴포넌트만 그때그때 로드시켜주는 기능을 제공함.

### 기본 사용법
```javascript
const MyComponent = React.lazy(() => import('./MyComponent'));
```

### Suspense와 함께 사용
React.lazy는 반드시 Suspense 컴포넌트 내부에서 사용해야 함.
```javascript
import React, { Suspense } from 'react';

const MyComponent = React.lazy(() => import('./MyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <MyComponent />
    </Suspense>
  );
}
```

### 주의사항

1. 서버 사이드 렌더링
   - React.lazy는 클라이언트 사이드 렌더링에서만 사용 가능
   - SSR에서는 @loadable/component를 사용해야 함

2. 에러 처리
   ```javascript
   <Suspense fallback={<div>Loading...</div>}>
     <ErrorBoundary>
       <MyComponent />
     </ErrorBoundary>
   </Suspense>
   ```

3. 네트워크 상태 고려
   - 느린 네트워크에서는 로딩 시간이 길어질 수 있음
   - 적절한 로딩 UI를 제공하는 것이 중요함

### 성능 최적화 팁

1. 적절한 분할 포인트 선택
   - 너무 작은 컴포넌트는 분할하지 않는 것이 좋음
   - 사용자 경험을 고려하여 분할 포인트를 결정해야 함

2. 프리로딩 활용
   ```javascript
   const MyComponent = lazy(() => import('./MyComponent'));

   // 마우스가 버튼 위에 올라갔을 때 미리 로드
   function onMouseOver() {
     const componentPromise = import('./MyComponent');
   }
   ```

3. 로딩 상태 관리
   ```javascript
   <Suspense
     fallback={
       <div className="loading-spinner">
         <Spinner />
         <p>컴포넌트를 불러오는 중...</p>
       </div>
     }
   >
     <MyComponent />
   </Suspense>
   ```

React.lazy는 대규모 애플리케이션의 성능을 최적화하는 데 매우 유용한 도구임. 
초기 로딩 시간을 줄이고, 필요한 시점에 필요한 컴포넌트만 로드함으로써 사용자 경험을 개선할 수 있음. 
하지만 무분별한 사용은 오히려 성능 저하를 일으킬 수 있으므로, 적절한 사용이 중요함. 