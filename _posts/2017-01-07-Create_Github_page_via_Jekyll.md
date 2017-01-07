---
layout: post
title:  "macOS에서 Jekyll을 사용하여 GitHub Pages 만들기"
date:   2017-01-07 23:11:39 +0900
categories: Development
---
 
블로그를 개설하려고 생각만 했었다.  
T사... N사.. 많은 블로그가 있었지만, 그냥 GitHub에 살림을 차리기로 했다.

## GitHub 가입 & Repository 생성
일단 GitHub에 페이지를 생성하려면 GitHub 계정이 있어야 한다.  
[가입](https://github.com/)을 완료하고 [Create a new repository](https://github.com/new)를 실행하면 된다.  
Repository name에 {username}.github.io라고 적으면 된다.  

## GitHub에 Push 하기
repository를 생성 한 후에는 해당 공간에 파일을 Push 해야 하는데 그러기 위해서는 Local로 Git source를 Clone해야 한다.  

```terminal
git clone https://github.com/{username}/{username}.github.io  

ex> git clone https://github.com/rextarx/rextarx.github.io
```

그 전에, 만약 Git profile에 Name과 email 설정을 하지 않았다면 아래와 같이 설정하자.  

```terminal
git config --global user.name "{username}"  
git config --global user.email "{email}"  

ex> git config --global user.name "Gyu"  
ex> git config --global user.email "rextarx@gmail.com"  
```
 
이제 해당 폴더에 들어있는 README.md 파일을 수정하여 Push 해보자.  
일단 README.md 파일을 열어서 아래와 같이 수정한다.

```
# rextarx's page  
Hello, World
```

그리고 터미널에 아래와 같이 작성한다.  

```terminal
git init  
git add README.md  
git commit -m "first commit"  
```

대충 이렇게 찍히면 된다.

```log
[master 39b8331] Change README
1 file changed, 2 insertions(+), 3 deletions(-)
```

> git push -u origin master  

```log
Counting objects: 3, done.
Writing objects: 100% (3/3), 278 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/rextarx/rextarx.github.io.git
   39b8331..613a183  master -> master
Branch master set up to track remote branch master from origin.
```

만약 아래와 같은 에러가 떴다면 SSH 접속 관련 설정을 찾아보자. 회사에서 방화벽을 막았다던가...  

```log
fatal: unable to access 'https://github.com/rextarx/rextarx.github.io.git/': Server aborted the SSL handshake
```

자, 이제 해당 페이지로 이동해보자.  

```terminal
> {username}.github.io  

> ex> rextarx.github.io  
```

아래와 같이 제대로 표시되고 있다.  

## Jekyll 설치  
Jekyll은 정적 블로그 웹사이트를 만들어주는 툴이다.  

> Jekyll 은 아주 심플하고 블로그 지향적인 정적 사이트 생성기입니다. Jekyll 은 다양한 포맷의 원본 텍스트 파일을 템플릿 디렉토리로부터 읽어서, (Markdown 등의) 변환기와 Liquid 렌더러를 통해 가공하여, 당신이 즐겨 사용하는 웹 서버에 곧바로 게시할 수 있는, 완성된 정적 웹사이트를 만들어냅니다. 그리고 Jekyll 은 GitHub Pages 의 내부 엔진이기도 합니다. 다시 말해, Jekyll 을 사용하면 자신의 프로젝트 페이지나 블로그, 웹사이트를 무료로 GitHub 에 호스팅 할 수 있다는 뜻입니다.  
([정식 사이트에서 발췌](http://jekyllrb-ko.github.io/docs/home/))


Jekyll을 사용하기 위해서는 일단 RVM부터 설치해야 한다.  

```terminal
sudo curl -sSL https://get.rvm.io | bash -s stable  --ruby  
```

설치하고나면 .bash_profile에 아래와 같이 rvm관련 코드가 추가되어 있을 것이다.  

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/1.png)

이를 아래 명령어로 재시작 해줘야한다.  

> source ~/.bash_profile

이제 rvm이 제대로 설치되었는지 확인해보자.  

> rvm -v  

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/2.png)

버전이 낮다. 2.1.1로 올려보자.

> rvm install 2.1.1

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/3.png)  

에러 발생...ㅠ_ㅠ

Homebrew를 업데이트 해보자.  

> homebrew update  

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/4.png)

시키는대로 권한 설정 다시 하고 업데이트...  

> sudo chown -R $USER /usr/local
> brew update

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/5.png)  

다시 돌아가서 rvm update 해보자.  

> rvm install 2.1.1  

잘된다! 로그를 보니 brew update...관련 로그도 있는 걸로 봐서..그냥 위에서 /usr/local 설정만 바꿔도 될 것 같기만 하다.  
설치까지는 시간이 조금 걸린다.  

조금 의아스러운 점은 rvm -v로 확인해봐도 ruby는 2.2.1로 업데이트 되는데, rvm 버전은 1.28.0으로 나온다...  ruby 버전을 올리는건가...?

## Gemfile 생성 및 실행
아래 명령어를 이용해서 Gemfile을 생성해보자.  
jekyll 버전은 [Gem](https://rubygems.org/search?page=9&query=jekyll&utf8=%E2%9C%93)에서 확인해서 해당 버전을 적으면 된다.  

> vi Gemfile  

```git
-------------------------------
source 'https://rubygems.org'

gem 'github-pages'
gem 'jekyll', '3.1.6'
-------------------------------
```

vi종료 방법은 esc를 한번 누른 다음 :wq(파일 저장 후 종료)를 입력해주면 된다.  
설정한 gem을 실행해보자.  

> bundle install

만약 bundle 명령어가 먹히지 않는다면 깔아준 다음 다시 실행하자.  

> gem install bundler  
> bundle install  

혹시 모르니 bundle update도 한번...

> bundle update  


## 일단 Jekyll을 구동시켜 보자!  

> jekyll new . --force  
> jekyll serve

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/6.png)  

감격이다... 몇시간 삽질끝에 드디어 띄웠다.  
이제 테마 적용을 해 보자.  


## Theme 적용

자, [Jekyll Theme](http://jekyllthemes.org/)를 찾아보자.  
[Shiori](http://jekyllthemes.org/themes/shiori/)로 정했다.  
해당 파일을 다운로드 받은 후 폴더에 붙여넣기한다. 다만 Gemfile, Gemfile.lock은 제외하고 복사해야 에러가 발생하지 않는다.  

다시 Jekyll을 실행해보자.

> jekyll serve  

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/7.png)  

적용이 됐다!!  

## GitHub에 Push하기  
자, 이제 올려보자.  

> git add *  
> git commit -m "Adjust Jekyll"  
> git remote set-url origin https://github.com/rextarx/rextarx.github.io.git  
> git push origin master

## 혹시 아래와 같은 에러가 발생한다면??
```mail
The page build failed with the following error:

A file was included in `about.md` that is a symlink or does not exist in your `_includes` directory. For more information, see https://help.github.com/articles/page-build-failed-file-is-a-symlink.

For information on troubleshooting Jekyll see:

  https://help.github.com/articles/troubleshooting-jekyll-builds

If you have any questions you can contact us by replying to this email.
```

그러면 jekyll 버전을 3.1.6으로 내려서 다시 해보자.  
Gemfile 생성부터 다시~  

> sudo gem uninstall jekyll  
> sudo gem install jekyll:3.1.6
> jekyll new . --force  
> jekyll serve  
> git add *
> git commit -m "Adjust Jekyll"  
> git remote set-url origin https://github.com/rextarx/rextarx.github.io.git  
> git push origin master

자, 완성!  

![](/assets/2017-01-07-Create_Github_page_via_Jekyll/8.png)


## 첫 포스팅 작성
Jekyll에서는 _posts에 Markdown 파일을 넣으면 자동으로 정적페이지로 만들어준다.  
([자세한 내용](http://jekyllrb-ko.github.io/docs/posts/))  
**파일 이름은 YYYY-MM-dd-{영문제목}.md 형태로 만들어야 한다. 한글 안된다.**  
그리고 Markdown 글의 맨 위에 [머리말](http://jekyllrb-ko.github.io/docs/frontmatter/)을 삽입해줘야 한다.

| 변수 | 설명 |
| ---------- | :--------- |
| layout    | 사용할 레이아웃 파일을 지정한다. 레이아웃 파일명에서 확장자를 제외한 나머지 부분만 입력한다. 레이아웃 파일은 반드시 _layouts 디렉토리에 존재해야 한다. |
| permalink | 생성된 블로그 포스트 URL 을 사이트 전역 스타일 (디폴트 설정: /year/month/day/title.html)이 아닌 다른 스타일로 만드려면, 이 변수를 사용하여 최종 URL 을 설정하면 된다. |
| published | 사이트가 생성되었을 때 특정 포스트가 나타나지 않게 하려면 false 로 설정하라.|
| category, categories | 포스트를 특정 폴더에 넣지 않고, 포스트가 속해야 하는 카테고리를 하나 또는 그 이상 지정할 수 있다. 사이트가 생성될 때, 포스트는 그냥 평범하게 이 카테고리들에 속한 것처럼 동작한다. 두 개 이상의 카테고리들을 지정할 때에는 YAML 리스트 또는 쉼표로 구분된 문자열을 사용한다. |
| tags | 카테고리와 유사하게, 하나 이상의 태그를 포스트에 추가할 수 있다. 또 카테고리와 동일하게, YAML 리스트 또는 쉼표로 구분된 문자열로 지정할 수도 있다. |

본 글은 아래와 같이 작성했다.  

```
---
layout: post
title:  "macOS에서 Jekyll을 사용하여 GitHub Pages 만들기"
date:   2017-01-07 23:11:39 +0900
categories: Development
---
```

만약 포스트에 로컬 이미지가 들어가야 한다면, 프로젝트의 루트 디렉토리에 assets 나 downloads 라는 이름의 디렉토리를 만들고, 이미지와 다운로드 파일, 그 밖의 다른 자원들을 보관해야 한다.  
나같은 경우에는 assets/{post name}/ 에 저장을 해뒀다.  