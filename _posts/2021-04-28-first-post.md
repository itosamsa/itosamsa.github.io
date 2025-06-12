---
title: GitHub Blog 생성
date: 2021-04-28 00:28:00 +000
categories: [Etc, Blog]
tags: [Blog]
---



## 1. GitHub Repository 생성
**{GitHub 이름}.github.io**  
Repository를 생성하면 자동으로 GitHub에서 정적웹사이트 호스팅을 지원해줍니다.

Repository 이름 = GitHub블로그 주소

접속하면 제목만 있는 README파일의 내용이 사이트에 그대로 노출이 됩니다.
보다 쉽게 사이트를 만들기 위해 Jekyll을 이용합니다.


## 2. 테마 고르기
[https://github.com/topics/jekyll-theme](https://github.com/topics/jekyll-theme)  
[http://jekyllthemes.org/](http://jekyllthemes.org/)  
[http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)  
[https://jekyllthemes.io/](https://jekyllthemes.io/)

위 사이트에 접속하면 다양한 Jekyll 테마를 볼 수 있습니다.  
저는 GitHub Topic 랭킹에서 마음에 드는 지금의 테마를 골라 지금 블로그에 적용했습니다.


## 3. 테마 적용
Jekyll 테마를 적용하는데 크게 세가지 방법이 있습니다.
- Remote
- Fork
- 직접 다운로드

저는 마지막 방법으로 했기때문에 다운로드 해서 하는 방법만 설명하겠습니다.  
(Fork는 Github 대시보드에 잔디가 안심어진다는 글을 봐서 안해봤고, Remote는 이전에 한번 만들어봤는데 원하는대로 설정하는게 오히려 더 복잡해보여서 지우고 다시 만들었습니다.)

1. 로컬 환경에 위에서 생성한 본인 깃블로그 Repository Clone
2. 선택한 테마를 Git 사이트에서 다운로드
3. 다운받은 테마를 본인의 깃블로그 Repository 에 복사


## 4. Ruby 설치
Push 를 하면 거의 바로 실제 사이트에 적용이 되지만 로컬에서 먼저 확인할 수 있도록 환경구성을 위해 Ruby를 먼저 설치합니다.

우선 로컬에 Ruby 가 설치되어 있는지 아래 명령으로 확인합니다.
```shell
ruby -v
```
저는 Mac 을 사용하고 있기 때문에 현재 상용버전보다 낮은 버전이 설치되어 있었고 명령어를 날렸을때 Permission 오류가 발생해서 이 해결방안까지 포함하여 내용을 작성하겠습니다.

Window 환경이라면 [https://www.ruby-lang.org/ko/downloads/](https://www.ruby-lang.org/ko/downloads/) 사이트에 접속해서 설치.

(Homebrew 를 이미 설치한 환경)  
(이미 설치를 마치고 글을 작성하기 때문에 중간과정은 없습니다.)

```shell
brew install rbenv ruby-build 

#  rbenv를 bash에 추가 
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile source ~/.bash_profile ruby -v 

# 설치 당시 안정버전이 3.0.1 이었음
rbenv install 3.0.1
rbenv global 3.0.1
rbenv rehash

# 제대로 설치됐는지 버전 확인
ruby -v

# bundler 설치
gem install jekyll bundler

```

```shell
# 서버 실행
bundle exec jekyll serve

# localhost:4000 으로 접속하면 확인할 수 있음!!
```



## 5. _config.yml 파일 수정 
내용을 보면 수정할 곳이 보이기 때문에 본인에 맞춰서 각자 수정하면 됩니다.


## 6. 첫 번째 포스트 작성 
