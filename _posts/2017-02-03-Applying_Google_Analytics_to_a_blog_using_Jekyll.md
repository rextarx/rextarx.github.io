---
layout: post
title:  "Jekyll을 사용한 blog에 Google Analytics 적용하기"
date:   2017-02-03 10:29:00 +0900
categories: Jekyll
---

## Jekyll을 사용한 blog에 Google Analytics 적용하기

Jekyll로 생성한 blog에 Google Analytics(이하 GA)를 적용해보자.
일단 Google 계정이 없다면 [Google부터 가입](https://accounts.google.com/SignUp)한 뒤, [GA에 가입](https://analytics.google.com/analytics/web/?authuser=0#provision/SignUp/)하자.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/1.png)  

가입은 간단하다. 아래와 같이 작성하면 된다.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/2.png)  

전부 작성 후 국가를 자신의 거주 국가로 맞춘 다음 약관 동의를 하자.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/3.png)  

가입이 완료 된 후에 관리 메뉴로 들어가면 우리가 사용해야 할 추적 ID가 발급되어 있는 것을 확인할 수 있다.  
이를 이용하여 Jekyll 프로젝트에 적용하면 된다.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/4.png)  

만약 적용한 Jekyll 프로젝트에 _config.yml 파일이 있다면, 해당 파일에서 g-analytics 항목을 찾아서 해당 추적 ID로 변경하면 된다.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/5.png)  

_config.yml 파일이 없다면, _includes폴더 아래에 analytics.html 파일과 같이 설정 파일이 있을 텐데, 그쪽 코드를 변경하면 된다.  
아래 코드에서 `{{ site.g-analytics }}`를 발급받은 추적 ID로 변경하자.  

```html
<script>
   (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
   (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
   m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
   })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
 
   ga('create', '{{ site.g-analytics }}', 'auto');
   ga('send', 'pageview');
 
 </script>
```

그리고 default.html 파일을 찾아서 아래 스크린샷과 같이 analytics.html 파일이 실행되도록 `{% include analytics.html %}`를 추가해주자.  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/6.png)  

적용을 모두 마친 후, 수정 사항을 모두 Push하고 스마트폰이나 기타 다른 Device에서 접근을 하고 GA에서 확인해보자.  
확인은 **실시간** 메뉴에서 해야 한다.  
~~대시보드에서도 실시간으로 취합되는 줄 알고 삽질한 건 안자랑~~  

![]({{site.baseurl}}/assets/2017-02-03-Applying_Google_Analytics_to_a_blog_using_Jekyll/7.png)  
