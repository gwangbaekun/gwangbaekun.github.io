---
layout: post
title: "[Mac] Mac developer configuration"
date: 2022-05-04 08:00:00 +0530
categories: Mac + M1
---

Mac, M1 개발자 환경 설정부터 react 구동까지 다루었습니다.

## Mac 개발자 환경설정

<hr>

M1 애플 프로덕트의 등장은 엄청나게 파워풀하지만

> `ARM-based`라는 점 때문에 개발 환경을 구축하는 일이 그 전과 비교해서 상당히 달라졌습니다.

> 이 포스트는 M1칩 기준에서 개발 환경을 구축하는 것을 다루었습니다.

<br>

### Step 0) Rosetta 2

<hr>

터미널에서 아래 코드를 실행하세요

```terminal
/usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

arm base로 구축되지 않은 앱들을 실행할 수 있게 해줍니다.

<br>

### 1) Xcode

<hr>

```terminal
xcode-select --install
```

react-native 개발자라면 Xcode를 먼저 설치하는 것을 추천합니다. ~~되게 오래걸려요~~

<br>

### 2) Homebrew

<hr>

> 참고하세요: 모든 homebrew앱이 m1을 지원하지는 않습니다. 2개의 버젼의 homebrew를 설치하여야 합니다.

<br>

version --1

```terminal
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

<br>

version --2

![rosetta setting](https://miro.medium.com/max/1400/1*tOL98VeOe10If22z1rzVKg.gif)

> Go to your “Applications” folder on Finder → right click Terminal in the “Utilities” folder → Duplicate → rename to “Rosetta Terminal” → Get Info → Open using Rosetta

위의 커맨드를 다시 입력하면 2개의 버전의 설치가 가능합니다.

<br>

Homebrew mac의 package manager로 필수입니다!

`pacman`,`apt-get`, `chocolately`와 같은 리눅스 계열, 윈도우 계열의 패키지 관리 툴과 비슷합니다.

> 참고하세요: 그냥 app store에 가서 깔면 vshrc 파일이나 bash파일에 평소 쓰던 커맨드를 따로 환경설정을 해주어야하나, homebrew를 이용해서 앱을 설치하면 자동으로 환경변수가 등록됩니다!

<br>

### 3)iTerm2

<hr>

![iTerm2](https://miro.medium.com/max/512/0*weLHeLzAWx7YizKr.png)

```code
brew install --cask iterm2
```

<br>

### 4) Zsh and Oh-My-Zsh

<hr>

![Zsh and Oh-My-Zsh](https://miro.medium.com/max/1400/1*kqijhIQ81fsaeGyn_8GpRw.png)

> **Oh My Zsh**

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

> Zsh 설정 + Theme

필수는 아니나 꼭 하시는 것을 추천합니다.
zsh를 쓰는 이유이기도 합니다.

- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) : 내가 전에 입력했던 커맨드를 자동으로 제안해줍니다.
  사용해본 커맨드인데 `기억이 안날 때` 특히 유용합니다.
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) : 커맨드를 하이라이팅 해주는 기능입니다. 커맨드 오타 감지에 특히 유용합니다.
- [powerlevel10k](https://github.com/romkatv/powerlevel10k) : 단순히 theme의 기능보다도 더 빠르게 만들어줍니다.

> ~/.zshrc 환경변수 등록하기
> 위의 추천 3가지 설정을 하셨다면 zshrc 파일에 많은 변화가 있었을 것입니다. zshrc 파일에 3가지 기능을 추가하는 것을 권장합니다.

- `alias brewr="arch -x86_64 /usr/local/bin/brew $@`[^1]

- `alias leg="arch -x86_64 $@` [^2]
- `bindkey -v ; export KEYTIMEOUT=1`[^3]

[^1]:
    1note
    arch-x86_64 라는 커맨드를 입력하는 대신에

    brewr install [package 이름]

    을 실행하면 intel 앱들을 바로 설치할 수 있습니다.

[^2]:
    2note
    "Rosetta"에서 호환된 모든 명령줄을 실행할 수 있습니다.

[^3]:
    3note
    Vim 바인딩을 합니다.

<br>

### 5) 프로그래밍 언어

<hr><br>

> NVM, Node.js

<mark color="red">WARN: NVM의 설치를 위해서 Homebrew를 사용하지 마세요.</mark>

`NVM`(Node Version Manager) 설치

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

`Node.js`설치

```
nvm install node
```

> Python

```
brew install miniconda

or

brew install anaconda
```

python이 설치되어 나오긴 하나 python의 라이브러리들이 호환되지 않는 것이 많습니다. miniconda의 python은 `rosetta 버전`에서 실행됩니다.

<br>

### VSC

<hr><br>

```
brew install --cask visual-studio-code
```

<hr>

참고 및 번역 : [Richard So > My Ultimate M1 Mac Developer Setup](https://codeburst.io/my-ultimate-m1-mac-developer-setup-cfdb2daeed2d)

comments_id: 35
