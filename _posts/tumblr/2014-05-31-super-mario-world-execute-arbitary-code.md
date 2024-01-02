---
layout: post
title: Super Mario World에서 임의 코드 실행하기
date: '2014-05-31T04:09:00+09:00'
tags:
- code injection
- security
- buffer overflow
tumblr_url: https://blog.iamghost.kr/post/87319268263/super-mario-world-execute-arbitary-code
redirect_from:
- /post/87319268263/super-mario-world-execute-arbitary-code
---
<iframe frameborder="0" height="315" src="//www.youtube.com/embed/OPcV9uIY5i4" width="420"></iframe>

[http://youtu.be/OPcV9uIY5i4](http://youtu.be/OPcV9uIY5i4)

위 동영상은 Super Mario World에서 임의의 코드를 실행하는 동영상이다. 제작자는 masterjun, 1:42부터 Super Mario World의 사운드/스프라이트를 사용한 Pong, Snake 게임을 볼 수 있다.

Buffer-overflow 같은 프로그램의 버그를 사용해&nbsp;임의의 코드를 실행되게 하는 것은 흔한 공격 기법이다. iPhone 탈옥, PS Vita eCFW 같은 것들이 대표적인 활용 예이다.

동영상 중반까지 발작을 하는것은 [Stun 버그](http://tasvideos.org/forum/viewtopic.php?p=299597#299597)를 일으키기 위한 것이다. 이 버그를 쓰면 화면상에 임의의 스프라이트를 소환하는것이 가능하다.

스프라이트 중에서도 [0xFA id를 가진 스프라이트를 소환](http://tasvideos.org/3957S.html)하는게 핵심인데, 이 스프라이트는 게임에 실제로 쓰이지는 않았는데, 게임의 $0322 메모리로 코드가 분기하게 되는 특징을 가지고 있다.

$0322 메모리는 [Object Attribute Memory (OAM)](http://www.smwiki.net/wiki/OAM)&nbsp;영역이다. 이 메모리에는 게임에 사용되는 스프라이트들의 정보(좌표, ID 등…)가 담겨있는데 OAM 영역으로 점프가 가능하단 것은 스프라이트의 위치를 바꾸거나 소환 순서를 조절함으로써 임의 코드 삽입이 가능하단 것을 의미한다.

masterjun은 이곳에 컨트롤러 입력 데이터 영역으로 분기하는 코드를 삽입했다. 그런 뒤 컨트롤러를 이용해 게임 부분에 대한 추가 코드를 입력했다. 1:39 정도부터 컨트롤러 2개가 마구 입력이 되고 그뒤 8개로 늘어나 입력을 하는것을 볼 수 있다. 제작자는 멀티탭에 연결된 8개의 컨트롤러를 모두 사용해 코드를 전송했다.

> ![image](/tumblr_files/tumblr_inline_pk3mprCqM41sh674j_540.jpg)
>
> 슈퍼 패미콤용 컨트롤러 멀티탭 사진, 실제 기기에서도 이걸 2개 꽂음으로써 최대 8개의 컨트롤러 연결이 가능하다.

이 버그는 [Awesome Games Done Quick 2014에서 실 기기에서 테스트](http://www.youtube.com/watch?v=Uep1H_NvZS0#t=1910)를 함으로써 에뮬레이터가 아니라 실제 기기에서도 똑같이 작동한다는 것이 증명되었다. 실제 기기에선 Raspberry Pi가 컨트롤러 대신 사용되었다.

