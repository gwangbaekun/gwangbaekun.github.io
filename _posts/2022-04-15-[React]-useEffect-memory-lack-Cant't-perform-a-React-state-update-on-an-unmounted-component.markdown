---
layout: post
title: "[React] useEffect 메모리 누수 Can't perform a React state update on an umounted component"
date: 2022-04-15 08:00:00 +0530
categories: React, warning
---

### [React] useEffect 메모리 누수 Can't perform a React state update on an umounted component

<br>

### **React memory 누수 error**

<br>

```bash
Warning: Can't perform a React state update on an unmounted component.
This is a no-op, but it indicates a memory leak in your application.
To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
```

### 원인 및 해결 방법

useEffect 안에서 비동기로직을 실행할때 위와 같은 warning이 뜬다.

```javascript
useEffect(() => {
  function tick() {
    return setTimeout(() => setTime((time + 1) % 5), 500);
  }

  function stop() {
    if (time > 15) {
      clearTimeout(tick);
    }
  }
  tick();
  stop();
  // 해결방법.
  // 추가할 부분입니다.
  return () => {
    clearTimeout(tick);
  };
}, [time]);
```

useEffect의 cleanup 함수를 통해 오류를 해결했습니다.

<br />

> [참고문헌](https://juliangaramendy.dev/blog/use-promise-subscription) https://juliangaramendy.dev/blog/use-promise-subscription

<br />

### Wait! Is that it?

Unfortunately not. Our component "subscribes" to the promise, but it never "unsubscribes" or cancels the request. If for any reason, our component is unmounted before the promise resolves, our code will try to "set state" (calling setBananas) on an unmounted component. This will throw a warning:

```bash
Warning: Can't perform a React state update on an unmounted component.
This is a no-op, but it indicates a memory leak in your application.
To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
```

결국 promise를 구독하지만, `구독 해제하지는 않으니 구독 해제`가 필요하다.

Taking advantage of [closures][closures] we can keep an `isSubscribed` boolean inside useEffect.

`클로저의 특성을 활용하자`

```javascript
function BananaComponent() {

  const [bananas, setBananas] = React.useState([])

  React.useEffect(() => {
    //구독하고
    let isSubscribed = true
    fetchBananas().then( bananas => {
      if (isSubscribed) {
        setBananas(bananas)
      }
    })
    // 구독해제하고
    return () => isSubscribed = false
  }, []);

  ...
```

[closures]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
