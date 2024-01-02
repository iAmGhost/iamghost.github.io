---
layout: post
title: Super Mario World에서 임의 코드 실행하기 (더 짧은 버전!)
date: '2014-06-13T17:15:00+09:00'
tags:
- code injection
- security
tumblr_url: https://blog.iamghost.kr/post/88652193418/super-mario-world-execute-arbitary-code-faster
redirect_from:
- /post/88652193418/super-mario-world-execute-arbitary-code-faster
---
<iframe frameborder="0" height="315" src="//www.youtube.com/embed/FkQdwUns7H8" width="420"></iframe>

[http://youtu.be/FkQdwUns7H8](http://youtu.be/FkQdwUns7H8)

[이전 글](http://blog.iamghost.kr/post/87319268263/super-mario-world)에서 화면에 출력되는 스프라이트가 저장되는 OAM 메모리를 사용해 임의 코드를 삽입하는 것에 대해 쓴 적이 있는데, 해당 영상을 만든 동일 인물인 [Masterjun](http://youtu.be/FkQdwUns7H8)이 더 빠른 방법을 찾아냈다. 바로 요시로 Chuck을 먹는 것이다.

Super Mario World에는 마리오의 상태를 바꾸는 스프라이트들이 있다.(버섯, 불버섯, 망토 등…) 근데 이런 스프라이트는 요시가 먹어도 마리오에 적용되어야 한다.

![image](/tumblr_files/tumblr_inline_pk02j51sm81sh674j_540.png)

위 그림에 나오는 몬스터가 Chuck인데 Chuck도 어떤 이유에서인진 모르겠지만 같은 속성을 가지고 있다. 그러나 특별한 속성 하나가 더 붙어 위와같이 요시의 혀로 건드릴 수 없어 먹지 못한다.

![image](/tumblr_files/tumblr_inline_pk02j6nDin1sh674j_540.png)

이 장면에서 초록 등껍질을 불로 녹이면서 동전이 생기는데, 동전을 몸으로 건드려 먹자마자 혀로 건드렸다. 원래대로라면 혀에 동전이 붙고 먹게 되겠지만 몸으로 건드렸으니 없어져버린다. 이때 레벨을 조금 더 전진하면 소환되는 스프라이트인 Chuck이 혀에 대신 붙게되고 먹을 수 있게 되는 것이다.

Chuck은 먹는 아이템으로 디자인되지 않았으니 엉뚱하게 동작할 것인데, Open Bus 영역인&nbsp;$014A13로 분기하게 된다. 이 영역은 ROM이나 RAM에 매핑되어 있지 않기때문에 데이터 버스에 남아있던 마지막 코드를 실행시키게 되는데 이 타이밍에 컨트롤러로 데이터를 입력함으로써 컨트롤러 영역인&nbsp;$4219으로 이동한다.

그 뒤엔 이전과 같은 방식으로 코드를 삽입한다. 엔딩 상태로 바뀌는 코드를 삽입하여 42초만에 엔딩을 보게 된다.

