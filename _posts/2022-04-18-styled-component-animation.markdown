---
layout: post
title: "[Styled-component] Animation Effect with styled-component"
date: 2022-04-18 08:00:00 +0530
categories: Styled-component
---

## Styled component로 애니메이션 효과 적용하기

어렵지 않습니다.

styled component의 장점 중 하나입니다.

css와 비교하면서 보면 더 편합니다.

react-native에서는`상대적으로` 무거은 styled-component를 쓰기 쉽진 않지만 웹에서는 유용하게 쓰이는 라이브러리입니다.

```javascript
import styled, { keyframes } from "styled-components"

...

return <Box />

...

const percentAnimation = keyframes`
  0% {
    transform:rotate(0deg);
    border-radius:0px;
  }
  50% {
    border-radius:100px;
  }
  100%{
    transform:rotate(360deg);
    border-radius:0px;
  }
`;

const rotationAnimation = keyframes`
  from {
      transform: rotate(0deg);
  }
  to {
      transform: rotate(360deg);
  }
`;

const Box = styled.div`
  height: 200px;
  width: 200px;
  animation: ${rotationAnimation} 1s linear infinite;
`;

```

`keyframes` 속성을 이용해서 할 수 있습니다.

props 방식으로 건네지는 고급 애니메이션 사용 스킬은

```javascript

const Box = ({children, ...rest}) => {
  return (
    <StyledWrapper {...rest}>
     {children}
    </StyledWrapper>
  );
};

...

<Box active />

...

const StyledWrapper = styled.div`
  width: 100px;
  height: 100px;
  background: #00bfb2;
  ${(props) => props.active &&`
   animation: ${boxFade} 2s 1s infinite linear alternate;
  `}
`;
// 추가적으로 props로 속성을 건네받을 수 있습니다

```

> 여러가지 옵션들은 추가해보시고 빼보시고 하면서 하시는 것이 도움이 많이 됩니다. 옵션에 대해 궁금하면 빼보고 실행시켜보세요.

<br>

> 참고문헌 [리액트 styled components 애니메이션 구현 https://zeddios.tistory.com/1222](https://zeddios.tistory.com/1222)

> 다음 포스트 : 자식선택자
