---
layout: post
title: "[ERROR] Gem::FilePermissionError"
date: 2022-04-14 08:00:00 +0530
categories: Blog Error
---

### Github blog 생성기

## **Mac에서 Gem::FilePermissionError**

참고 링크

[**왕초보를 위한 Github 블로그 만들기 (1) - 레포지토리 만들기(with Jekyll)**](https://zeddios.tistory.com/1222)

[**왕초보를 위한 Github 블로그 만들기 (2) - 테마 적용(with Jekyll)**](https://zeddios.tistory.com/1223)

전체적인 레이아웃은 이 블로그를 보고 따라했다.

github 블로그 만들기 (2)에서 문제가 생겼다.

일단 국룰 테마 Jerkyll plainwhite를 적용하면서 생긴 문제

`bundle install`

Mac에서 Ruby의 패키지 매니저인 gem을 통해 설치를 진행하다가

&gt; $ gem install bundler
ERROR: While executing gem ... (Gem::FilePermissionError)
You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.

시스템 ruby를 이용하고 있기 때문에 권한이 없어 gem 설치가 안된 것이다.

sudo를 통해 root권한으로 실행하면 설치가 가능하지만, 보안상 이유로 권장하지 않는 설치법이다.

rbenv를 통해 문제를 해결했다.

## 문제 해결

---

**✔️ 1. brew를 통해 rbenv를 설치한다.**

```
brew update
brew install rbenv ruby-build
```

**rbenv 가 잘 설치되었는지 확인해보고**

```bash
rbenv versions
```

**✔️ 2.rbenv로 관리되는 Ruby를 설치!**

설치할 수 Ruby 버전은 다음 명령으로 확인

```bash
rbenv install -l
```

! [] (https://user-images.githubusercontent.com/89245389/163316340-009c5e42-aee3-4e8d-99ff-08159b12a1c6.png)

<img src="https://user-images.githubusercontent.com/89245389/163316340-009c5e42-aee3-4e8d-99ff-08159b12a1c6.png" />

```bash
rbenv install 3.1.2
```

아래와 같이 로그가 보이면서 설치가 완료됩니다.

```bash
Downloading ruby-3.1.2.tar.gz...
-> https://cache.ruby-lang.org/pub/ruby/3.1/ruby-3.1.2.tar.gz
Installing ruby-3.1.2...
ruby-build: using readline from homebrew
```

다시 rbenv로 버전을 확인해봅니다.

```bash
rbenv versions
```

여전히 `system`으로 되어있지만, 신규 추가된 2.6.4 버전도 함께 보입니다.

```bash
* system
  3.1.2
```

**✔️ 3. rbenv로 글로벌 버전을 3.1.2로 변경합니다.**

```bash
rbenv global 3.1.2
```

다시 버전을 확인하면 3.1.2가 선택되어있는 것을 확인할 수 있습니다.

```bash
  system
* 3.1.2
```

**✔️ 4. rbenv PATH를 추가하기 위해 본인의 쉘 설정 파일 (`..zshrc`, `.bashrc`) 을 열어**

```bash
vim ~/.zshrc
```

**✔️ 5. 다음의 코드를 추가합니다.  
저는 zsh를 사용하니 `.zshrc`에 추가합니다.**

```bash
[[ -d ~/.rbenv  ]] &amp;&amp; \
  export PATH=${HOME}/.rbenv/bin:${PATH} &amp;&amp; \
  eval "$(rbenv init -)"
```

> vim editor를 사용할 때 **`i`**를 누르면 편집 기능이 활성화되고

> `esc` + `:wq` + `enter` 저장 후 창 종료가 됩니다.

<br />

**✔️ 6. 코드를 추가하셨다면 `source`로 코드를 적용합니다.**

```bash
source ~/.zshrc
```

**그리고 다시 `gem install`을 수행해봅니다.**

```bash
gem install bundler
```

아래와 같이 정상적으로 실행되는 것을 확인할 수 있습니다.

```bash
Fetching bundler-2.0.2.gem
Successfully installed bundler-2.0.2
Parsing documentation for bundler-2.0.2
Installing ri documentation for bundler-2.0.2
Done installing documentation for bundler after 2 seconds
1 gem installed
```

[**문제해결 참고링크**](https://jojoldu.tistory.com/288) https://jojoldu.tistory.com/288
