---
layout: post
title:  "Alfred workflow를 이용한 Chrome history 검색"
date:   2021-02-23
category: Alfred
---

## Alfred workflow를 이용한 Chrome history 검색
Link: https://github.com/tupton/alfred-chrome-history

사용법은 위 링크에 설명되어 있다.

일단 Releases에서 최신 workflow를 다운로드 받는다.  
현재 기준 [Alfred Chrome History v0.7.0](https://github.com/tupton/alfred-chrome-history/releases/download/0.7.0/alfred-chrome-history.alfredworkflow)  

설치 후 Alfred > Workflows > Google Chrome History > Script Filter를 눌러보면 스크립트가 나온다
```
PROFILE="~/Library/Application Support/Google/Chrome/Default"
PATH="env/bin:$PATH"
python chrome.py "${PROFILE}" "{query}"
```

나 같은 경우에는 해당 경로에 Default 폴더가 없고, Profile 1, Profile 2가 있어서 해당 경로에 맞게 수정해 주었다.
`PROFILE="~/Library/Application Support/Google/Chrome/Profile 1"`

명령어는 ch {query} 인데, 현재 한글이 인덱싱이 제대로 안되어있는지 되는 것도 있는데 대부분 잘 안된다.

시간 날때 코드를 살펴보도록 하자.
