--- 
layout: post
title:  "[Jekyll] 깃허브 블로그 만들기"
categories: jekyll
tags: [Blog, jekyll, Github, Git]
---

## 0. Jekyll 블로그 테마 고르기

- 지킬 테마 제공 사이트

    직접 블로그를 디자인할 수도 있지만 오픈 소스로 제공되는 많은 지킬 테마들을 본인의 입맛에 맞게 선택하면 간단히 블로그를 구축할 수 있을 것이다. 아래 사이트들은 무료로 테마를 제공하고 있으니 원없이 구경하고 선택하면 된다.

    - https://jekyll-themes.com/free/
    - http://themes.jekyllrc.org/
    - http://jekyllthemes.org/

    참고) 필자는 [Yat](https://jekyll-themes.com/jekyll-theme-yat/) 테마를 선택했다.

## 1. 테마 적용하기

### 1.1. 자신이 정한 테마 다운받기

### 1.2. 다운받은 폴더 압축을 해제하고 모든 파일을 본인의 github.io 폴더에 붙여넣기

### 1.3. 터미널에 **bundle install** 입력하기

- 다운받은 테마에 필요한 번들을 다운받을 수 있다.
- 가끔 Gemfile이 없는 테마가 있는데 이를 그냥 push하면 제대로 테마가 적용되지 않는다. 필자는 해결방법을 몰라서 그냥 Gemfile이 있는 테마만 이용하였다.

### 1.4. 터미널에 **bundle exec jekyll serve** 입력하기

- 로컬 서버를 띄워 브라우저를 열어 주소를 입력한다.

## 2. 블로그 수정하기

Jekyll 디렉토리 구조를 수정하여 다운받은 테마를 본인에게 맞게 수정할 수 있다. 변경해야 하는 부분을 필요에 맞게 명시하였으나 본인이 적용하고 싶은 테마에 따라 달라지므로 테마의 설명을 꼭 확인하기 바란다.

### 2.1. 반드시 변경
- featured_tags/ : 카테고리 대분류 폴더
- featured_categories/ : 카테고리 소분류(태그) 폴더
- data/ : 개발자 및 운영자, 기타 정보 폴더 (author.yml 수정이 필요)
- config.yml : 가장 중요한 환경변수 설정 파일
- README.md : GitHub 프로젝트 애서 소개하게 될 글
- favicon.ico : 블로그 접속 시 브라우저 주소창에 표시되는 대표 아이콘
- about.md : About 메뉴 클릭 시 나타나는 블로그에 대한 소개글

### 2.2. 필요시 변경(디자인, 기능 등 수정)
- assets/ : 이미지, CSS 등을 저장 폴더
- _layouts/ : 포스트를 감싸기 위한 레이아웃 정의 폴더(페이지, 구성요소 등 UI변경 시 수정)
- _includes/ : 재사용을 위한 기본 페이지 폴더
- Gemfile.lock : Gemfile에 기록한 레일 기반 라이브러리를 설치 후 기록하는 파일(중복설치 방지)
- Gemfile : 필요한 레일 기반 라이브러리를 자동으로 설치하고 싶을 때 명시하는 설정 파일
- .gitignore : GitHub에 올리고 싶지 않은 파일들은 이 파일에 경로지정 가능(예: _site 산출물, 환경설정, 개인정보, 작성중인 글 등)
- sitemap.xml : 테마의 사이트맵
- search.html : Tipue Search 설치 시, 검색결과를 출력하는 페이지로 활용
- robots.xml : 구글 웹로봇 등 검색엔진 수집 등에 대한 정책을 명시하는 설정파일
- posts.md : 포스트 작성 관련 설정파일

### 2.3. 변경 필요없음(참고)
- _posts/ : 포스트를 저장하는 폴더
- .git/ : GitHub 연동을 위한 상태정보가 담긴 폴더
- _site/ : Jekyll 빌드 생성 결과물 폴더(실제 GitPages에서 WEB으로 보여지는 산출물)
- .sass-cache/ : 레일 엔진에서 사용하는 캐시 저장폴더(변하지 않는 산출물들에 대한 파싱을 하지 않아 속도보장)
- _sass/ : 일종의 CSS 조각파일 저장 폴더
- _js/ : JavaScript 저장 폴더
- _plugins/ : 플로그인 저장 폴더(크롬 정책상 어차피 사용안함)
- LICENSE.md : 테마 개발자의 라이센스 설명
- index.html : 블로그 최초 접속 페이지
- googlea0d1f22cc8208170.html : 구글 검색엔진에 블로그를 등록하는 과정의 소유권 확인 파일
- feed.xml : RSS Feed 활용을 위한 XML
- browserconfig.xml : 윈도우8 이상 IE11 접속 시 클라이언트가 요청하는 환경설정 파일
- 404.md : 404 Not Found Page(블로그에 없는 페이지 요청 시 등장하는 페이지)
- .eslintrc : EcmaScript Lint(자바스크립트 협업 개발을 위한 규칙 정의) 환경설정 파일
- .eslintignore : EcmaScript Lint 무시할 규칙 지정(전역변수 에러표시 예외처리 등)
- .babelrc : Babel(자바스크립트 컴파일러) 설정파일

## 3. 수정사항 적용하기

깃허브 서버와 연결하여 원격으로 Push하면 된다. 차례대로 터미널에 입력하면 된다.

    git add .
    git commit -m "커밋 메세지"
    git push origin master

## References

- [블로그 테마(Themes) 고르기 및 환경설정](https://theorydb.github.io/envops/2019/05/02/envops-blog-theme/)
- [왕초보를 위한 Github 블로그 만들기](https://zeddios.tistory.com/1223)
- [깃허브(Github) 블로그를 생성해 보자](https://ansohxxn.github.io/blog/i-made-my-blog/)

