---
layout: post
title:  "macOS에서 숨김파일 표시하기"
date:   2017-02-01 23:36:00 +0900
categories: macOS
---

## macOS에서 숨김파일 표시하기

터미널에서 아래 명령어를 실행하면 된다.  

```Terminal
defaults write com.apple.finder AppleShowAllFiles -bool true
```

적용되기 위해서는 Finder를 재시작해야 한다. 터미널에 아래 명령어도 실행하자.  

```Terminal 
killall Finder
```