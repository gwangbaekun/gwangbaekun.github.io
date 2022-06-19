---
layout: post
title: "npm yarn 그리고 yarn berry"
date: 2022-06-12 08:00:00 +0530
categories: NodeJS npm yarn
comments_id: 3
---

toss tech 블로그를 보고 yarn berry에 대한 내용과 node_module의 무거움 등에 대해 나름대로 정리한 글입니다. [node_modules로부터 우리를 구원해 줄 Yarn Berry](https://toss.tech/article/node-modules-and-yarn-berry)

## NodeJS의 시작

<hr>

![Node.JS](https://res.cloudinary.com/practicaldev/image/fetch/s--Lvl1ZNKy--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1ph7yc1i1vqqgwpxegw5.png)

근래 급부상하는 NodeJS는 많은 장점이 있습니다.

- Chrome V8 JavaScript 엔진 기반
  - 빠른 실행이 가능하다 정도로 염두에 두고 넘어가면 되겠습니다.
- 단일 쓰레드(Single Thread)와 이벤트 기반
  - JS의 특징입니다. 단일 쓰레드는 메모리 사용량과 시스템 리소스 사용량 변화가 많지 않은 대신에 쓰레드 하나가 무너지면 프로그램 전체에 문제가 발생합니다.
  - 멀티쓰레드라고 꼭 빠른 것은 아닌 이유가 쉽게 말해서 쓰레드를 어떻게 할당할지, 쓰레드 어떤 것을 써야할지, 어떤 쓰레드로 실행할지에 대한 연산 때문에 오히려 느릴 수도 있습니다.
  - 단, CPU사용률이 높은 어플리케이션에서는 Node.js 사용 권장하지 않습니다. (Ex 은행앱)
- 비동기 I/O 처리 (Non-Blocking I/O)
  - 브라우저가 동작하는 방식과 살짝 맞물립니다.
- 고성능 네트워크 서버
- 개발 생산성 향상
- `방대한 모듈 제공` (NPM)
  - 사실은 이 포스트의 주된 내용입니다.

<br>

> <br> **NOTE! Node.js의 Thread Pool**\
> <br>

    Node.js는 사용자의 요청은 단일 스레드로 처리하고, 실질적인 작업은 멀티쓰레드로 운용하여 결과를 구현합니다. Node.js가 스스로 thread pool을 구성하여 효율적으로 멀티쓰레드를 사용합니다.

<br>

### Node.js가 어울리는 서비스

- 간단한 로직
- 대량의 클라이언트가 접속하는 서비스(입출력 많음)
- 빠른 개발 요구
- 빠른 응답시간 요구
- 비동기 방식에 어울리는 서비스 (ex. 스트리밍 서비스, 채팅 서비스)

### Node.js가 어울리지 않는 서비스

- 단일 작업이 오래 걸리는 서비스

<br>

## node module의 한계

<hr>
<br>

### 1. Multi-Thread의 한계

Multi-Thread 방식은 쓰레드로 하여금 병렬 처리를 가능하게 합니다.\
다른 요청을 독립적으로 받을 수 있다는 것인데,\
IO Blocking을 해결하는 이상적인 모델로 보일 수 있습니다.\

<br>

> <br> \*\*NOTE! IO Blocking
> <br>

    서버에서 IO(input, output)를 처리하다가 지연이 발생하면 다른 요청은 처리되지 못하면 문제를 말합니다. 사용자의 요청을 쓰레드로 처리합니다.

<br>

## npm 패키지에 오류가 있다면? patches

## yarn berry
