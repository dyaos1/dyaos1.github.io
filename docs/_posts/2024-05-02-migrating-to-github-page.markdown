---
layout: post
title:  "깃헙 페이지 사용하기 with Jekyll"
date:   2024-05-02 17:43:34 +0900
categories: diary
---
### 배경
개발노트로 원래는 노션을 사용했었는데, 무료 계정으로 쓸 수 있는 용량이 너무 적어서 쓸만한 블로그가 없는지 찾아보다가 깃헙 페이지에 대해 알게 되었다.
마크다운으로 작성할 수 있는 블로그를 찾고 있었으므로 깃헙 페이지가 최적이라 생각되어 깃헙 페이지로 이주를 결심하게 되었는데...


### 문제
지킬을 설치하려면 루비가 필요하고, 맥OS는 기본적으로 루비가 깔려 있는데 이 시스템 루비는 구버전이라서 지킬 설치에 적합하지 않다. 새로 루비를 깔게 되면 구버전과 신버전이 충돌을 일으키기 때문에 결국 루비 버전매니저를 깔고 신버전을 설치해야 한다.
물론 이 모든 작업을 하기 전에 홈브루는 설치되어 있어야 한다.


### 설치
https://jekyllrb.com/docs/installation/macos/

- chruby 설치하기 https://github.com/postmodern/chruby
`brew install chruby`


- ruby 설치하기
먼저 ruby-install을 설치한다. https://github.com/postmodern/ruby-install#readme
`brew install ruby-install xz`

ruby-install을 이용하여 ruby를 설치한다.
`ruby-install ruby`


- configuration
`brew info chruby` 를 입력하여 chruby.sh와 auto.sh의 경로를 얻는다.

`sudo vi ~/.zshrc` 로 .zshrc 파일을 열어서 조금 전에 얻은 경로를 추가한다.
`source /opt/homebrew/opt/chruby/share/chruby/chruby.sh`
`source /opt/homebrew/opt/chruby/share/chruby/auto.sh`


- 최신 루비로 바꾸기
`ruby -v` 를 입력하여 현재 버전을 확인하고, `chruby`를 입력하여 사용가능한 루비 버전을 확인한다.
`chruby $사용가능한루비버전`을 입력하여 루비 버전을 방금 설치한 버전으로 바꾼다.


- 지킬 설치
`gem install jekyll bundler`


### 깃헙 페이지 시작하기
https://docs.github.com/en/pages

- 닉네임.github.io라는 이름의 repository를 만든다.
- repository setting에서 Pages를 찾아 들어가서 Deploy from Branch를 선택하고, 퍼블리싱 소스는 docs를 선택한다(optional).
- 로컬에 repository와 연동할 폴더를 만들고, 안에 docs폴더를 만들고 jekyll을 시작한다.
{% highlight ruby %}
mkdir repository-name && cd repository-name
mkdir docs && cd docs
jekyll new --skip-bundle .
{% endhighlight %}

- 생성한 repository를 로컬에 연동한다.
repository 폴더로 이동 후(cd ..)
{% highlight %}
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/${username}/${username}.github.io.git
git push -u origin main
{% endhighlight %}

- 잘 되었는지 확인
repository Settings 로 이동하여 Pages 탭을 클릭, Visit site 링크가 생성 되면 클릭하여 지킬이 잘 실행 되는지 확인한다.