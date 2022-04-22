---
layout: post
title: "[Styled-component] Change tag with styled-component"
date: 2022-04-16 08:00:00 +0530
categories: Styled-component
---

## Styled component를 사용하여 html tag 바꾸기

<br />

> styled-component를 이용해서 html tag 바꾸는 것은 어렵지 않습니다.

웹 환경에서는 주효하게 쓰는 라이브러리라서 사용을 잘 하는 것이 중요합니다.

```javascript
//styled-component

const Title = styled.h1`
  color: #111;
`;
```

```javascript
//html

//<Title>제목</Title>

<Title as="header">제목</Title>
```

위 처럼 as attribute로 바꿔주면 h1에서 header로 바뀝니다.

styled-component의 장점 중 하나입니다.

<br>

> 다음 포스트는 styledcomponent의 attr tag, 자식 선택자, animation 효과에 대해 다루겠습니다.
