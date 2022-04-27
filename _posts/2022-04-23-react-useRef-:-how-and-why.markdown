---
layout: post
title: "[React] react-query 사용기"
date: 2022-04-20 08:00:00 +0530
categories: React
---

React의 대표적인 useRef 훅과 그 사용법을 알아보자. 기본적으로 useRef는 특정 DOM을 선택한다.

## [React] useRef hook

useRef훅은 javascript에서 `getElementById`, `querySelector`와 같은 역할을 대신합니다.

리액트를 사용할 때에는 특정 DOM에 접근해야만 하는 순간들이 있습니다. 스크롤 객체를 움직여야 한다던지(누르면 움직이는 navbar), 특정 element의 크기를 가져와야한다던지 할 때에는 DOM을 직접 선택하여야 합니다.

<br/>

> 즉, HTML 요소를 가져오기 위해서 useRef를 씁니다.

```javascript

    function Input() {
        const inputRef = useRef(null);
        const handleClick = () => {
            inputRef.current?.focus()
            setTimeout(() => {
                inputRef.current?.blur()
            }, 5000)
        };

        return (
            <>
                <input placeholder="ref" >
                <button onClick={handleClick}></button>
            </>);
    }

```

input 요소에서 접근을 해서 focus 이벤트가 발생하고, 5초 후에 blur 이벤트가 발생하는 간단한 로직입니다.

> HTML input 요소에 있는 methods에 직접 접근하여 `DOM API`를 호출해주어 상태를 변화시킬 수 있습니다.

<br>

[reference](https://react.vlpt.us/basic/10-useRef.html)
https://react.vlpt.us/basic/10-useRef.html
