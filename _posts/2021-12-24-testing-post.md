--- 
    # 우선 위 아래에 --- 를 써서 머릿말 쓰는 영역을 구분해주어야 한다.
title:  "[Jekyll] 블로그 포스팅하는 방법"
    # 포스트의 제목을 큰 따옴표로 적어 준다. 이 title을 적어주지 않으면 .md 파일 이름으로 적어주었던 title 부분이 제목으로 업로드 된다.
excerpt: "md 파일에 마크다운 문법으로 작성하여 Github 원격 저장소에 업로드 해보자. 에디터는 Visual Studio code 사용! 로컬 서버에서 확인도 해보자. "
    # 포스트 목록에서 보여지는 블로그 소개 글로 들어가는 것 같다.

categories:
  - Blog
    # 이 포스트의 카테고리는 Blog로 정했다.
tags:
  - [Blog, jekyll, Github, Git]
    # 태그와 카테고리의 차이점은 카테고리는 sub url이 붙는 페이지가 있지만 태그는 없다는 것이다. 카테고리 보다 좀 더 세부적. [] 대괄호 안에서 , 콤마로 구분해주어 여러개의 태그를 이 포스트에 지정해 주었다.

toc: true
    # Table of Contents. 포스트의 헤더들만 보여주는 목차를 사용할 것인지의 여부. ture 로 해주면 포스트의 목차가 보이게 된다.
toc_sticky: true
    # true로 해주면 목차가 스크롤을 따라 움직이게 된다! 스크롤을 내리면 목차도 따라 내려오게 됨. 이 밖에도 이 포스트의 toc_icon, toc_label 도 설정할 수 있다.
 
date: 2021-12-24
    # 글을 처음 작성한 날짜. yyyy-mm-dd 형식으로 작성했다.
last_modified_at: 2021-12-24
    # 이 글을 수정한 날짜.

    # 이 밖에도 layout, permalink, published, author_profile 등등 머릿말에 쓰이는 여러 변수들이 있다. 내가 원하는 변수를 머릿말에 지정해서 사용할 수도 있다. 아직은 모르는 것이 많아서 차차 조사한 후 나중에 머릿말 전역 변수에 대해서 포스팅 해야겠다.

    # 머릿말에 쓰인 변수는 page Liquid 변수로 사용될 수 있다. 예를 들어 머릿말에 적힌 categories 변수 값은 “Blog”이므로 Liquid 언어로 “{{page.categories}}” 를 본문 내에 쓰면 “Blog”값이 출력될 것이다.

    # 머릿말이 ---로 끝난 이후부터는 포스트 본문 영역이다. jekyll은 HTML과 Markdown을 지원하는데 마크다운이 HTML보다 더 간략하고 편한 문법이다. 따라서 마크다운 문법으로 포스트를 작성해준다.
---

origin theme: https://jekyll-themes.com/jekyll-rtd/


