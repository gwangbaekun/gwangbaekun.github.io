---
layout: post
title: "[JS] 브라우저 이벤트 루프"
date: 2022-05-03 08:00:00 +0530
categories: Javascript, Browser
---

브라우저 이벤트 루프에 대해 참고한 글입니다. call stack이나 queue에 대한 설명, 비동기 처리에 대한 내용이 포함되어 있습니다.

## 브라우저 작동 원리

<hr>

자바스크립트 개발자는 브라우저의 작동과 밀접한 관련이 있기 때문에 브라우저의 작동원리를 세심하게 살펴보아야 합니다. 브라우저는 예전 보다 훨씬 복잡해졌습니다. `Webpack, Babel, ESLint, Mocha, Karma, Grunt`

자바스크립트는 싱글 스레드 언어로 한번에 `한 개의 업무`만 할 수 있고 `한 줄의 코드`만 읽을 수 있습니다.

> `single call stack`, `heap`, `queue`로 이루어져 Javascript Concurrency Model(흔히 V8엔진이라고 불리는)를 구성합니다.

![Javascript event loop](https://miro.medium.com/max/1400/1*-MMBHKy_ZxCrouecRqvsBg.png)

<br>

### 1. Call Stack

함수 호출을 저장하는 자료 구조입니다.

함수 실행을 호출하면 stack에 넣고, 맨 위에서 부터 차례대로 실행됩니다.

여담이지만 무한 루프에 빠져 함수를 여러번 한번에 호출하게 되면 (크롬의 경우) 스택은 16,000 frames로 제한되어 있어 `Max Stack Error Reached`라는 에러를 보게 됩니다.

<br>

### 2.Heap

메모리를 할당 받는 곳입니다. 데이터는 조각 모음으로 Heap에 저장됩니다.

<br>

### 3. Queue

콜백 함수를 담게 됩니다. 만약 콜 스택이 비어있다면 queue에서 메세지를 받아와 함수를 실행하게 됩니다.

쉽게 말해서 비동기 이벤트를 queue에 담고, 콜백 함수로써 생성되어 실행되는 것입니다.

> 비동기 처리는 결국 call stack이 쉴 때 실행된다는 점 입니다.

> 브라우저 엔진이 아닌 다른 곳에서의 비동기 처리 또한 같습니다. CPU가 쉴 때 콜백 함수로써 실행하게끔 만드는 것이 비동기 이벤트입니다.

<br>

### 4. Event loop

console.log() 함수는 빠르지만 for나 while문에서 백만개의 데이터를 출력하려면 당연히 오래 걸립니다. ~~P.S. 오래 걸리지도 않을 겁니다. call stack이 한번에 다 차버리기 때문이죠.~~

당연하게도 우리는 서버에서 받는 데이터의 크기가 큰 경우를 경계해야겠죠.

이 때 우리는 다행히도 Axios라는 라이브러리를 사용해서 비동기 처리로 데이터를 받습니다.

사진이나 동영상과 같은 파일들은 상당히 무거워서 오래 걸리겠죠. 등등 ...

위와 같은 상황에서 함수 코드를 저장해 놓았다가 콜백 함수로써 나중에 호출하는 것입니다.

그러던 와중에 다른 페이지로 가는 버튼을 누르면 어떻게 될까요?

다른 페이지로 가는 함수가 call stack 에서 바로 실행되면서 이벤트가 일어납니다.

> 만약 비동기 처리를 하지 않았다면 사진과 동영상 혹은 굉장히 큰 크기의 데이터를 다 받고 난 후에 다른 페이지로 가는 함수가 실행될 것입니다.

때문에 `get(),setTimeout(),setInterval(), Promises, etc.` 와 같은 함수들이 필요한 것입니다.

<br>

그렇다면 콜백 함수로 호출하는 함수들의 코드들은 도대체 어디로 갔다 오는 것일까요?

### Web api

브라우저가 생성한 `Browser Web APIs` 쓰레드는 비동기 이벤트, DOM 이벤트, http request, setTimeout을 실행하기 위해 존재합니다.

이 때문에 Javascript가 멀티쓰레드인 것처럼 보이는 것입니다.

사실은 브라우저가 생성한 쓰레드를 사용하고 있습니다.

Web Api는 스스로 call stack에 있는 함수를 동작하지 못합니다.

만약 Web Api에 있는 함수 실행이 끝나면 자연스럽게 queue에 call back 함수를 등록하게 됩니다.

 <br>

**이 과정에서 이벤트 루프는 stack 과 queue를 모두 관찰하고 stack이 비어있다면 queue에서 맨 앞의 함수를 꺼내와 stack에 넣어주는 역할을 합니다.**

> Call stack, Heap 브라우저의 이벤트를 동작하게 만드는 것들입니다. 여기서 브라우저는 `Web Api` 쓰레드를 생성해서 콜백 함수를 저장하고 실행하게 `callback queue`에 보내줍니다. call stack 과 queue를 연결해주는 `이벤트 루프` 또한 JS를 이해하는데 중요합니다.

<br>

![https://miro.medium.com/max/1400/1*MnRk2ZVl5acI5BFmmw7IRg.png](https://miro.medium.com/max/1400/1*MnRk2ZVl5acI5BFmmw7IRg.png)

<br>
<hr>

참고 문헌 : [https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec](https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec)
