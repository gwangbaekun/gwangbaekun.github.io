---
layout: post
title: "[JS] 브라우저 동작 방식"
date: 2022-04-30 08:00:00 +0530
categories: JS, CS
---

브라우저 동작 원리에 대해 탐구한 글입니다. 브라우저 주소창에 www.google.com을 치면 벌어지는 일들에 대한 글에서 심회된 글 입니다.

<br>

# 브라우저 동작 방식

먼저 선행하기 좋은 글입니다.

[브라우저 주소창에 www.google.com을 치면 벌어지는 일](https://gwangbaekun.github.io/cs/2022/04/20/what-happens-when-I-enter-www.google.com.html)

<br>

## 1. 브라우저의 구조

<br>

![](https://user-images.githubusercontent.com/76525368/129310978-457fe83d-5648-4219-871e-ddf38b9d3f39.png)

<br>

- UI `User Interface` 사용자 인터페이스
  홈 버튼, 새로고침 등 사용자와 상호작용하는 부분입니다.

- Browser Engine 브라우저 엔진
  사용자 인터페이스와 렌더링 엔진을 연결합니다.

- Rendering Engine
  요청한 콘텐츠를 브라우저 화면에 표시하는 엔진입니다.
  HTML과 CSS를 파싱하여 웹페이지를 화면에 표시합니다.

  - > `Rendering Engine`은 업데이트가 필요할 때, 효율적으로 렌더링을 할 수 있도록 자료구조를 생성합니다.
  - > react-dom은 rendering engine의 자바스크립트 업그레이드 버전이라고 생각하면 편합니다. 분명 다릅니다...!

- Networking 네트워크
  HTTP 요청과 같은 네트워크 호출에 사용, 각종 네트워크 요청을 수행, 서버와 통신

- JavaScript Interpreter 자바스크립트 해석기
  자바스크립트 코드를 실행하는 인터프리터
  Chrome의 경우 V8을 사용

  - > rendering engine이 HTML과 CSS를 처리하다가 <script>태그를 만나면 권한을 `Javascript Interpreter`에게 넘깁니다.

  - > react엔진은 jsx를 자바스크립트로 변환하여 출력합니다.

- `cookie`, `local stroage`, `indexed DB`

<br>

## 브라우저 렌더링 과정

### 1. DOM tree 생성

- 브라우저의 렌더링 엔진이 HTML 코드를 읽고 파싱하여 `DOM tree`를 생성합니다.
- 각 Node가 서로 연관성을 가지게 됩니다.

### 2. Render tree 생성

- CSS 파일이나 HTML에 inline으로 작성된 스타일 코드를 파싱하여 CSSOM을 구성합니다.
- document부터 각 Node를 순회하면서 각각에 맞는 CSSOM을 찾아 규칙을 적용합니다.

### 3. Layout(reflow)

- 정확한 위치와 크기를 결정
- %, em 등 상대적인 단위를 사용했을 때 px로 변환

### 4. Paint(repaint)

레이아웃을 픽셀로 그린다.

<br>

## 브라우저가 화면을 다시 그릴 때

1. `layout`이 달라질 때

요소의 크기나 위치가 바뀌거나 브라우저 창의 크기가 바뀌었을 때는 3, 4 번을 반복합니다.
창을 반복적으로 늘였다 줄일 때 브라우저가 버벅이는 현상을 경험할 수 있습니다.

> 반응형 spa를 만들 때 layout과정을 거칩니다.

2. 레이아웃이 변하지 않을 때

4번의 과정만 실행합니다.

3. 레이어의 합성만 다시 발생하는 경우

레이아웃은 그대로 있고 프린팅 과정에서 각각 그려준 다음에 하나의 비트맵으로 합성해서 페이지를 완성합니다.

[css최적화하기](https://csstriggers.com/)

> 1 > 2 > 3 순으로 시간이 오래 걸립니다.

<hr>

다음 포스트는 웹에서 js의 동작 원리에 대해 다루어 보겠습니다.

<hr><br>

참고
[https://bbangson.tistory.com/87#:~:text=%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EB%8A%94%20%EC%84%9C%EB%B2%84%EB%A1%9C%EB%B6%80%ED%84%B0%20HTML,%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A5%BC%20%EB%82%98%ED%83%80%EB%83%85%EB%8B%88%EB%8B%A4.](https://bbangson.tistory.com/87#:~:text=%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EB%8A%94%20%EC%84%9C%EB%B2%84%EB%A1%9C%EB%B6%80%ED%84%B0%20HTML,%EC%9B%B9%20%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A5%BC%20%EB%82%98%ED%83%80%EB%83%85%EB%8B%88%EB%8B%A4.)
[https://velog.io/@irisdew/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC](https://velog.io/@irisdew/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)
