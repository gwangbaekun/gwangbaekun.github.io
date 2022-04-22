---
layout: post
title: "[Styled-component] Adapting & Extending"
date: 2022-04-20 08:00:00 +0530
categories: Styled-component
---

Styled Component adapting & extending

## Styled Component adapting & extending

> styled-component extends & adapting은 아주 쉬운 문법이고 편리하며 코드 양을 줄여줍니다.

```javascript

    <Box>
    <BoxTwo>
    <BoxThree>

...

const Box = styled.div`
width: 200px;
height: 200px;
`

// adopting
const Box = styled(Box)``

// extending
const BoxTwo = styled(Box)`
    width: 250px;
    display: flex;
    justify-content: center;
    align-items: center;
`

```

쉽고 편리한 adapting 과 extending 을 보았습니다.

만약 다른 컴포넌트에서 불러다 쓰고 싶다면

```javascipt

export const Box = styled.div`
    width: 200px;
    height: 200px;
`

// export 를 붙여주고 됩니다.

// 타 컴포넌트에서 불러주면 됩니다.

```

> 다음 styled-component 포스트 : theme
