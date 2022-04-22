---
layout: post
title: "[ERROR] `require': cannot load such file -- webrick (LoadError)"
date: 2022-04-14 08:00:00 +0530
categories: Blog Error
---

Github blog 생성기

### Github blog 생성기

## **[ERROR] `require': cannot load such file -- webrick (LoadError)**

<br />

> bundle exec jekyll serve로 로컬에서 jekyll 서버를 구동하려고 하면 webrick을 로드하지 못했다는 오류가 발생할 수 있습니다

![blog3](https://user-images.githubusercontent.com/89245389/163506229-b314c421-9ee9-42e6-863a-12b7b7e79375.png)

<br />

이런 경우에

```bash
bundle add webrick
```

webrick을 추가해주면 됩니다.

ruby 3.0.0 부터 webrick이 기본으로 포함된 gem에서 빠졌기 때문이라고 하네요.

[**문제해결 참고링크**](https://junho85.pe.kr/1850) https://junho85.pe.kr/1850
