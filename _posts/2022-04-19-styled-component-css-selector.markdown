---
layout: post
title: "[Styled-component] Pseudo Selectors"
date: 2022-04-18 08:00:00 +0530
categories: Styled-component
---

Styled component 자식 선택자 활용하기

## Styled component 자식 선택자 활용하기

styled component의 큰 장점 중 하나인 자식 선택자입니다.

자식 선택자를 잘 활용하면 크게 도움이 될 수 있습니다.

> 중복되는 코드를 방지하는 styled-component의 adapting & extending까지 예제를 통해 보겠습니다.

<br>

```javascript

import styled from "styled-component"

...

return (
    <Box>
        <Pseudo>span</Pseudo>
    </Box>)

...

const Box = styled.div`
    height: 200px;
    width: 200px;
    justify-content: center;
    align-items: center;
    span {
        font-size: 30px;
    }
`
    // 이런 식으로 하면 더욱 직관적이고 쉬울 수 있으나 사실 별로 안좋은 방법입니다. span 태그가 바뀐다면 코드를 다시 바꾸어 주어야 하기 때문이죠.

    // 때문에 더 좋은 방법은

const Box = styled.div`
    height: 200px;
    width: 200px;
    justify-content: center;
    align-items: center;
    ${Pseudo} {
        font-size: 100px;
    }
`

// 이 방법은 Pseudo tag를 참조하기 때문에 Pseudo가 어떤 html tag를 가지고 있는지 상관이 없습니다.

// 재활용이 훨씬 더 쉬워지는 장점이 있습니다.

const Pseudo = styled.span`
    font-size: 30px;
`

```

> 다음 styled-component 포스트 : adapting & extending
