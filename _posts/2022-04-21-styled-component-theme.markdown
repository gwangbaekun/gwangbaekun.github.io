---
layout: post
title: "[Styled-component] Theme"
date: 2022-04-20 08:00:00 +0530
categories: Styled-component
---

Styled Component Theme 적용하기

## Styled Component Theme 적용하기

> 제가 개인적으로 생각하는 styled component 의 강점은 자식에게 쉽게 속성을 전해줄 수 있다는 점입니다.

때문에 theme 적용도 상당히 편리합니다.

바로 코드를 통해 보시죠

**index.js**

```javascript

...

import { ThemeProvider } from "styled-components"

const darkTheme = {
  textColor: "whitesmoke",
  backgroundColor: "#111",
};

const lightTheme = {
  textColor: "#111",
  backgroundColor: "whitesmoke",
};

...

<ThemeProvider theme={darkTheme}>
    <App />
</ThemeProvider>

```

**App.js**

```javascript
// 각기 다른 컴포넌트에서 theme 을 적용한 스타일을 보여주면 됩니다.

const Title = styled.h1`
  color: ${(props) => props.theme.textColor};
`;
```

Theme 적용으로 완성된 서비스를 만들어 보세요.

전역변수로 관리해주고 토글 버튼을 클릭할 때마다 darkTheme 과 lightTheme을 적용해주면 되겠죠.

> 다음 포스트 : windows linux 적용 error들에 관해서 쓸 예정입니다.
