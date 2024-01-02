---
layout: post
title: Hate Plus 한국어화 작업일지 - 6
date: '2014-08-03T06:08:00+09:00'
tags:
- hate plus
- hate plus 한국어화 작업일지
tumblr_url: https://blog.iamghost.kr/post/93618874278/hateplus-korean-diary-6
redirect_from:
- /post/93618874278/hateplus-korean-diary-6
---
2014년 8월 3일

전에 말했던 스크롤 다이얼로그 작업을 좀 쉽게 하기 위해 글자 크기, 텍스트박스 사이즈, 워드랩을 흉내내는 프로그램을 만들어봤다.

[http://code.activestate.com/recipes/577946-word-wrap-for-proportional-fonts/](http://code.activestate.com/recipes/577946-word-wrap-for-proportional-fonts/)

가변 폰트 크기를 적용 가능한 스니펫이 있어서 이걸 사용했다. 여기에 글자별 폰트 사이즈는 fontforge 라이브러리를 사용해 실제 게임에서 쓰는 폰트의 글자 크기를 그대로 가져다 쓰게끔 했다.

![image](/tumblr_files/tumblr_inline_pk3pufuyN91sh674j_540.png)

이제 이걸 기반으로 텍스트들을 뽑아내고 보면서 비교하는 노가다만 하면 된다.

![image](/tumblr_files/tumblr_inline_pk3pugIasc1sh674j_540.png)

…라고 생각했는데 이거 뭔가 이상하다.

최대한 비슷하게 흉내낸다고 흉내냈지만 실제 게임에서 출력되는것과 다르게 나온다.

제길…

![image](/tumblr_files/tumblr_inline_pk3pugcBXd1sh674j_540.png)

하는 수 없이 게임을 뜯어고쳐서 스크롤 정보를 화면에 뜨게 했다.

진작에 이럴걸… 이제 게임 두개 띄워놓고 비교하면서 기록만 잘 하면 된다.

![image](/tumblr_files/tumblr_inline_pk3puhhZq31sh674j_540.png)

게임 진행하는게 귀찮아서 내부 설정으로 모든 로그를 언락시키는 코드도 끼워넣었다.

![image](/tumblr_files/tumblr_inline_pk3puhkD871sh674j_540.png)

\*뮤트의 Block 13 로그들을 읽을때 하이퍼링크가 제대로 표시되지 않고, \*뮤트 AI 활성화 상태에서 읽을시 튕겨버리는 문제를 발견했다.

최신버전은 어떤지 모르겠는데 Ren'Py의 Traceback 시스템은 최악이다. 제대로 된 에러 정보를 주지 않는다.

이건 도저히 모르겠으니 크리스틴님한테 고쳐달라고 해야지…

