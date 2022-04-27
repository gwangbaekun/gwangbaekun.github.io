---
layout: post
title: "[React] 리액트 불변성이 필요한 이유"
date: 2022-04-20 08:00:00 +0530
categories: React
---

리액트에서 불변성이라는 단어는 React를 관통하는 핵심 키워드이다.
리액트는 불변성을 지켜주어야만 상태가 업데이트됐음을 감지할 수 있고 이에 따라 필요한 렌더링을 합니다.

## 리액트와 불변성

<br>
<hr>

> 리액트에서는 불변성을 지켜야한다.

리액트는 불변성을 지켜주어야만 상태가 업데이트됐음을 감지할 수 있고 이에 따라 필요한 렌더링을 합니다.

리액트는 상태 객체에 대한 요소를 하나하나 비교하지 않고 얕은 비교 [shallow compare](https://ideveloper2.tistory.com/159)를 통해서 성능 최적화를 합니다.

**간단하게 말해서 값이 같은지 다른지만 판단하는 방법**

<br>

> 얕은 복사와 깊은 복사

1. 복사가 아님

```javascript
const video = { time: 20, title: "title" };
const copyVideo = video;
//배열의 복사가 아니라 같은 참조값을 가짐
user.age += 1;
```

<br>

2. 얕은 복사 `call by reference`

spread operator를 이용한 얕은 복사 입니다.

```javascript
const video = { time: 20, title: "title" };
const copyVideo = { ...video };

// 이 때에는 video가 copyVideo와 같지 않습니다.

// 하지만

video === copyVideo; //false

video.time === copyVideo.time; // true
```

객체 내부의 값은 동일한 것을 볼 수 있습니다.

> spread operator는 얕은 복사를 하게 되어 새로운 객체를 할당 받았기 때문에 객체의 참조 값 자체는 다르게 되어 video의 `값 변경은 불변성`을 지키게 됩니다.

<br>

3. 깊은 복사 `call by copy`

> 방식은 복사와 같지만 데이터를 더 활용해서 새로운 객체를 만듭니다.

원래의 값이 보존되어 역시 불변성을 지킬 수 있고 얕은 복사보다 더 안전합니다.

메모리 사용량이 늘어난다는 단점이 있습니다.

> 흔히 불변성을 유지하기 위해 사용하는 `immer`는 깊은 복사를 합니다.

<br>

결론

#### **리액트 컴포넌트의 불필요한 재렌더링을 막기 위해서 `shallow compare`를 도와주어 앱의 최적화를 도모할 수 있습니다.**

#### **또한 `call by reference`로 최적화된 불변성 유지와 `call by copy`로 복잡한 구조의 데이터의 불변성을 유지할 수 있습니다.**
