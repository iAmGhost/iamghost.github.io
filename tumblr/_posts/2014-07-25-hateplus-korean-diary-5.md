---
layout: post
title: Hate Plus 한국어화 작업일지 - 5
date: '2014-07-25T00:00:00+09:00'
tags:
- hate plus
- hate plus 한국어화 작업일지
tumblr_url: https://blog.iamghost.kr/post/93618420918/hateplus-korean-diary-5
redirect_from:
- /post/93618420918/hateplus-korean-diary-5
---
2014년 7월 25일

크리스틴님이 매우 바빴는지 한국어를 게임에 적용하는게 오늘에서야 끝났다.

게임이 다국어 지원이 쉽게 되게끔 만들어져있지 않았기 때문에 오래 걸릴게 대충 예상은 됐었다…

![image](/tumblr_files/tumblr_inline_pk0fszkw1r1sh674j_540.png)

이제 큰 일이 하나 남았는데 바로 스크롤 다이얼로그를 고치는 것이다.

이건 헤이트 플러스에서 새로 생긴 시스템인데, 로그를 스크롤하면 히로인이 스크롤 위치에 따라 대사를 치는 그런 시스템이다.

![image](/tumblr_files/tumblr_inline_pk0fszFygs1sh674j_540.png)

문제는 이게 “게임상에서 스크롤된 줄"을 기반으로 대사가 뜨게끔 되어있다.

원본 텍스트 데이터 파일과 실제로 표시되는게 다르기 때문에(글자 간격, 텍스트 창 크기, Word wrap 등으로 인해) 이걸 구현하는데는 엄청난 노가다가 들어갔을 것이다.

문제는 번역된 텍스트에서는 이 위치가 달라지기 때문에 나도 노가다를 해야 된다… orz

텍스트 내에 화면에는 보이지 않는 마커같은걸 넣어놓은뒤 해당 마커가 있는 텍스트가 출력될때를 감지하여 보여주는 식으로 했으면 더 편했을거 같은데…

