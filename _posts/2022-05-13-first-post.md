---
title: "github 블로그 만들기 ~ 포스팅 작성"
excerpt: "github 블로그를 생성, 테마 적용, jekyll 서버 설치 및 가동, 카테고리와 태그 등록, 포스팅 작성"

categories:
    - til
tags:
    - github

toc: true

date: 2022-05-13
last_modified_at: 2022-05-13
---

참고 링크

https://honbabzone.com/jekyll/start-gitHubBlog/
https://ansohxxn.github.io/blog/category/
https://devinlife.com/howto%20github%20pages/category-tag/#3-tags-%EB%93%B1%EB%A1%9D%ED%95%98%EA%B8%B0
https://devyurim.github.io/development%20environment/github%20blog/2018/08/07/blog-6.html

<br>

# 깃헙 블로그 만들기 ~ 포스팅까지
## 깃헙 블로그 만들기

### 1. 리포지토리를 생성한다.

(본인 깃헙 아이디).github.io
    
Add a README file 옵션을 체크
    
※ settings -> pages -> your site is published at (본인 깃헙 아이디).github.io가 녹색 불로 뜨는지 확인

<br>

### 2. 본인의 리포지토리를 데스크탑에 clone한다.

내 경우에는 open with github desktop을 사용했다.

이 경우 

c:Users:(사용자명):Documents:GitHub:(본인 깃헙 아이디).github.io

여기에 리포지토리 폴더가 생성된다. github desktop에서 마찬가지로 commit, push 모두 손쉽게 할 수 있다.


<br>

### 3. 테마를 받는다.

http://jekyllthemes.org/

본인 마음에 드는 테마를 고르면 된다.

zip파일로 다운로드받은 후 그 안에 있는 내용물을 내 리포지토리 폴더에 붙여 넣는다.

<br>

### 4. Ruby를 설치한다.

https://rubyinstaller.org/downloads/

여기서 Ruby + Devkit을 받아서 설치한다.

설치가 완료되었다면 

` ruby --version`

을 입력해서 제대로 설치가 되었는지 확인한다.

<br>

### 5. cmd를 열어 리포지토리 디렉토리로 이동한 후 아래의 명령어를 차례대로 실행한다.

```
gem install bundler
bundle
jekyll serve
```

jekyll serve는 jekyll 서버를 여는 명령어라고 생각하면 된다. 앞으로 지킬 서버를 열 때는 리포지토리 디렉토리로 이동 -> jekyll serve로 서버 연결 이 순을 따르게 된다.

<br>

### 6. localhost:4000 에서 페이지가 정상적으로 로딩되는지 확인

이후에는 git에 commit - push하는 과정 없이도 파일이 변경된 후의 상태를 바로 반영해서 볼 수 있다.

<br>

### 7. _config.yml 파일 수정
당장 필요한 부분 위주로 수정했다. 이후에 설정값은 변경될 수 있다.
```yml
# Site Settings
locale                   : "ko-KR"
title                    : "programming blog"
title_separator          : "-"
subtitle                 : # site tagline that appears below site title in masthead
name                     : "조주연"
description              : "Today I learned (java, spring framework, db, network, algorithms)"
url                      : "https://yeonleaf.github.io" # the base hostname & protocol for your site e.g. 
baseurl                  : # the subpath of your site, e.g. "/blog"
repository               : "yeonleaf/yeonleaf.github.io" # GitHub username/repo-name e.g. 
teaser                   : # path of fallback teaser image, e.g. "/assets/images/500x300.png"
logo                     : # path of logo image to display in the masthead, e.g. "/assets/images/88x88.png"
masthead_title           : "배우기 위한 기록들" # overrides the website title displayed in the masthead, use " " for no title
# breadcrumbs            : false # true, false (default)
words_per_minute         : 200
```

```yml
# Site Author
author:
  name             : "조주연"
  avatar           : # path of avatar image, e.g. "/assets/images/bio-photo.jpg"
  bio              : "꾸준히 공부하는 개발자입니다. <br> 매일 매일 공부한 기록들을 올립니다."
  location         : "Republic of Korea"
  email            : "hcjy97@naver.com"
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: hcjy97@naver.com
    - label: "Notion"
      icon: "fas fa-fw fa-link"
      url: "https://erratic-leo-4a8.notion.site/Juyeon-Jo-863edd2bf15442088e657c59b4eb867a"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/yeonleaf"
```

```yml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
  # _pages
  - scope:
      path: "_pages"
      type: pages
    values:
      layout: single
      author_profile: true
```


## 카테고리와 태그

0. _data -> navigation.yml 파일 수정

이곳에는 nav 부분에 들어가는 카테고리를 넣을 수 있다.

```yml
main:
  - title: "알고리즘 문제풀이"
    url: /categories/algorithm/
  - title: "TIL(Today I Learned)"
    url: /categories/til
```

하지만 이 상태에서 url 링크로 들어가면 아직 카테고리를 연결하지 않았기 때문에 404 페이지가 뜬다.

1. _pages폴더를 생성한다.
2. _pages 폴더 하위에 카테고리 md파일을 생성한다.

상위 카테고리의 경우 (categories는 모든 category를 총괄하는 개념으로 보면 될 듯)

```
---
title: "Posts by Category"
layout: categories
permalink: /categories/
author_profile: true
---
```
하위 카테고리의 경우

```
---
title: "알고리즘 문제풀이"
layout: category
permalink: /categories/algorithm
author_profile: true
taxonomy: algorithm
---
```

이렇게 세팅해 놓고 포스트를 작성할 때 포스트마다 해당되는 카테고리와 태그를 적으면 자동으로 반영된다.

태그는 _pages에 카테고리와 동일한 방법으로 생성할 수 있는데, 굳이 그렇게 하지 않아도 게시물에 넣고 싶은 태그를 넣으면 새로 생성할 수 있다.

<br>

## 포스트 작성

포스트는 _posts라는 폴더를 만들어서 그 안에 markdown 파일을 생성하는 식으로 작성한다.

이름 양식은 (생성일)-제목 양식을 맞춰야 한다.

본문을 적기 전에 메타데이터를 먼저 입력해야 한다.

```
---
title: "github 블로그 만들기 ~ 포스팅 작성"
excerpt: "github 블로그를 생성, 테마 적용, jekyll 서버 설치 및 가동, 카테고리와 태그 등록, 포스팅 작성"

categories:
    - til
tags:
    - github

toc: true

date: 2022-05-13
last_modified_at: 2022-05-13
---
```

이렇게 하고 본문을 아래에 markdown 문법을 지켜서 적으면 포스트를 작성할 수 있다.