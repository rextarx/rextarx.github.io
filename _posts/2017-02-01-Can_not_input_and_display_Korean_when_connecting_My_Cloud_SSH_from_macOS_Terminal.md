---
layout: post
title:  "macOS Terminal에서 MyCloud SSH 접속시 한글 입력/표시 안되는 문제"
date:   2017-02-01 23:38:00 +0900
categories: macOS
---

## macOS Terminal에서 MyCloud SSH 접속시 한글 입력/표시 안되는 문제

MyColud는 기본적으로 한글 지원을 하지 않습니다... 아래와 같이 ???로 표시가 되죠.  

![]({{site.baseurl}}/assets/2017-02-01-Can_not_input_and_display_Korean_when_connecting_My_Cloud_SSH_from_macOS_Terminal/1.png)  

자, 이제 이걸 수정해보죠.  

## MyCloud 언어 설정
Mac Terminal로 SSH 접속을 합니다.  

```Terminal
ssh {id}@{MyCloud ip}  
ex> ssh root@192.168.0.6
```

아래 명령어로 bashrc을 열어줍니다.  

```Terminal
nano ~/.bashrc  
```

![]({{site.baseurl}}/assets/2017-02-01-Can_not_input_and_display_Korean_when_connecting_My_Cloud_SSH_from_macOS_Terminal/2.png)  

위 스크린샷에서 export LC_ALL=c를 ko_KR.UTF-8로 변경합니다.  
그리고 control+o, control+x로 나오면 됩니다.  

이제 bashrc를 reload해야 하는데요. 아래 명령어를 실행하면 됩니다.  

```Terminal
source ~/.bashrc
```

이제 이렇게 하면 아래와 같이 한글이 제대로 표시가 됩니다.  

![]({{site.baseurl}}/assets/2017-02-01-Can_not_input_and_display_Korean_when_connecting_My_Cloud_SSH_from_macOS_Terminal/3.png)  

하지만, 여전히 한글 입력은 되지 않습니다....  

## 한글 입력
아래 명령으로 inputrc 파일을 엽니다.  

```Terminal
nano /etc/inputrc  
```

![]({{site.baseurl}}/assets/2017-02-01-Can_not_input_and_display_Korean_when_connecting_My_Cloud_SSH_from_macOS_Terminal/4.png)  

항목중에 set convert-meta off를 찾아서 앞에 #를 제외해줍니다.  
그리고 위와 마찬가지로 control+o, control+x로 저장하고 종료해줍니다.  

이제 Terminal를 **재시작**해주면 제대로 적용되어 있음을 확인하실 수 있습니다.  

![]({{site.baseurl}}/assets/2017-02-01-Can_not_input_and_display_Korean_when_connecting_My_Cloud_SSH_from_macOS_Terminal/5.png)  
