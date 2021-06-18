---
title: "[github.io] blog 생성!!"
date: '2021-03-26' # 18:26:28 -0400'
categories:
- blog
- github
# toc: true
# toc_label: My Table of Contents
# toc_sticky: true
---

블로그를 써보기로 함.
개발자들이 많이쓰는 블로그를 검색해본 결과 여러테마도 지원하고 github 네임밸류로 깃헙블로그를 만들어보기로함.
확실히 개발자 아니면 사용하기 힘들어보임. 그래도 ganzi나니까 나는 만듬.

## 저장소 만들기
github에서 저장소를 하나 판다. 저장소 이름을 나의 username뒤에.github.io 형식으로 만든다. 이렇게 만든 블로그는 username.github.io 도메인으로 접속가능!

## theme 선택 (jekyll)
jeckll-theme 라는 토픽으로 많은 템플릿이 공개되어있음. 블로그에 적용할 테마 선택해서 위에서 만든 내 저장소에 내려받는다.

## 로컬 개발 환경 세팅
jeckll는 Ruby로 생성되었기 때문에 ruby언어와 bundler를 설치하여야 한다.
gem은 루비 패키지 매니저
bundler는 루비프로젝트에 필요한 의존요소들의 올바른 버전을 추적하고 설치해서 일관된 환경을 제공한다.

mac(catalina) 개발환경에서는 ruby가 설치되어있음
```
cd ./username.github.io
gem install bundler
bundle install
```
ERROR
루비 패키지 매니저인 gem을 설치시 에러발생
```
$ gem install bundler
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.
```
cause : 시스템 ruby를 사용하기 때문에 권한이 없어 설치가 안된것.
sudo를 통해 root권한으로 설치가 가능하지만 보안상이유로 권장하지 않는 설치법

> 해결
https://jojoldu.tistory.com/288

서버구동
bundle exec jeckyll serve

localhost:4000 번으로 접속

## 프로젝트 세팅
#### _config.yml 설정
적용된 테마에다 customizing 학위해_config.yml을 수정.
https://mmistakes.github.io/minimal-mistakes/ 에 guide를 살펴보면 custom 방법이 나와있음


You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

### 소제목
​```코드블럭 python
def print_hi(name):
  print("hello", name)
print_hi('Tom')
​```

### 링크거는법
Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
