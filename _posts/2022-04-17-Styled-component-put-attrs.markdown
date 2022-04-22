---
layout: post
title: "[Styled-component] Put attrs with styled components"
date: 2022-04-17 08:00:00 +0530
categories: Styled-component
---

Styled component를 사용하여 같은 태그에 같은 속성 집어넣기

## Styled component를 사용하여 같은 태그에 같은 속성 집어넣기

바로 코드를 보겠습니다.

```javascript

<Input />
<Input />
<Input />
<Input />
<Input />


const Input = styled.input``
```

위 코드에서 input tag에 required 속성을 주려면

> `<Input required="true"/>`

처럼 `required="true"`나 `required` 속성을 붙여주어야 합니다.

<br>

하지만 styled-component를 이용하면

```javascript
const Input = styled.input.attrs({ required: true })``;
```

의 형식으로 attribute를 일제히 붙여줄 수 있습니다.

<br>

> styled-component 다음 포스트 : tag 바꾸기, attrs, animation, 자식 선택자
