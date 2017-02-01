---
layout: post
title:  "macOS에서 WiFi On/Off 단축키 만들기"
date:   2017-02-01 17:00:00 +0900
category: macOS
---

## macOS에서 WiFi On/Off 단축키 만들기
개인적인 사정으로 WiFi와 Local망을 번갈아가면서 사용한다.  
해당 명령어는 단축키가 없어서 매번 마우스로 클릭해줘야 했다.  
하지만 Automator를 사용한다면?!  


## Terminal 명령어 작성하기

먼저 자신의 WiFi 이름이 무엇으로 지정되어 있는지 확인하자.  

```Terminal
networksetup -listnetworkserviceorder
```

따로 손대지 않았다면 아래 스크린샷과 같이 en1로 되어 있을 것이다.  

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/1.png)  

아래의 명령어를 통해 WiFi On/Off를 토글할 수 있다.  

```Terminal
networksetup -getairportpower en1 | grep "On" && networksetup -setairportpower en1 off || networksetup -setairportpower en1 on
```

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/2.png)  

해당 명령어를 실행할 때마다 WiFi가 On/Off 된다면 절반은 성공한 것이다.  


## Automator Workflow 생성하기  
Automator를 실행해서 **서비스**를 선택하자.  

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/3.png)  

**서비스가 받는 항목**을 **입력 없음**으로 설정하고, **선택 항목 위치**를 **모든 응용 프로그램으**로 선택하자.  

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/4.png)  

그리고 목록에서 **쉘 스크립트 실행**을 마우스 더블 클릭하거나 오른쪽 창으로 드래그하자.

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/5.png)  

그리고 아래 창에 위에서 작성했던 커맨드를 넣고, 우측 상단의 실행을 눌러보자.  

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/6.png)  

Cmd+S를 눌러 해당 Workflow를 저장하자. 저장되는 경로는 아래와 같다.    
```path
/Users/{username}/Library/Services
```

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/7.png)  

시스템 환경설정 > 키보드 > 단축키 > 서비스로 진입하면 위에서 저장한 이름의 Workflow가 보일 것이다.  
(만약 보이지 않는다면 재부팅을 한 번 해보자. 오래 전에 설정해서 기억이 가물가물하다..)  
이를 선택하고 단축키를 지정하자. 필자의 경우에는 Cmd+Shift+Ctrl+W로 하였다. 이제 잘 동작하는지 확인해보자.  

![]({{site.baseurl}}/assets/2017-02-01-Create_shortcut_WiFi_On_Off/8.png)  


## 참고 사이트
[How to create shortcut to turn on/off Wifi in Snow Leopard](https://discussions.apple.com/thread/5077807#25858327)