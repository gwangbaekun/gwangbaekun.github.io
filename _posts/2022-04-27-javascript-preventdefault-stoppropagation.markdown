---
layout: post
title: "[javascript] e.stopPropagation, e.preventDefault"
date: 2022-04-20 08:00:00 +0530
categories: Javascript
---

e.stopPropagation과 e.preventDefault의 차이를 분석하고 해석한 포스트입니다. js의 이벤트 버블링을 같이 다루었습니다.

## e.preventDefault()와 e.stopPropagation

 <br>

### e.preventDefault()

<hr />
<br>

> e.preventDefault()는 element의 기본 행동을 막습니다.

form element에서는 submit을 막고

a href element에서는 navigating을 막습니다.

a tag로 만든 것을 클릭해도 URL을 여는 것을 막아주는 것입니다.

```javascript

    <div id="parent">
        <a id="child" href="example.com">
    </div>

    var child = document.getElementById("child")

    child.onclick = function(e) {
        e.preventDefault();
        console.log('a 태그 방지됨!')
    }
    // 부모 노드를 클릭하면 아래 콘솔이 출력됩니다.
    child.parentNode.onClick = function(e) {
        console.log('자식이 클릭되었다!')
    }

```

### e.stopPropagation()

<hr />
<br>

> e.stopPropagation()은 이벤트의 버블링이나 캡쳐링을 막습니다.

```javascript

    <div id="parent">
        <a id="child" href="example.com">
    </div>

    var child = document.getElementById("child")

    child.onclick = function(e) {
        e.stopPropagation();
        console.log('요건 보이지만 event bubble을 막아줘!')
    }
    // 부모 노드를 클릭하면 아래 콘솔이 출력됩니다.
    child.parentNode.onClick = function(e) {
        console.log('절대 안보입니다.')
    }

```

부모 요소의 div와 자식 요소의 div가 각기 서로 다른 event를 가져야할 때 유용합니다.

예를 들어 onClick 이벤트가 버블링 될 시에 부모 요소의 onClick 이벤트는 발동하지 않습니다.
