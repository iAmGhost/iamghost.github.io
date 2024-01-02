---
layout: post
title: 게임보이 Bivert 모드 없이 롬 해킹으로 팔레트 반전 시키기
date: '2015-03-15T04:28:44+09:00'
tags:
- gameboy
tumblr_url: https://blog.iamghost.kr/post/113620435108/gameboy-invert-palettes-instead-of-bivert-mod
redirect_from:
- /post/113620435108/gameboy-invert-palettes-instead-of-bivert-mod
---
게임보이 개조 방식중 Bivert 모드라는 것이 있다. 게임보이 LCD 뒤에는 편광 필름과 반사 필름이 있는데, 백라이트 설치를 위해서는 이 두 필름을 제거해야 한다.

이 때문에 백라이트를 달았더라도 반사필름을 제거했기 때문에 화면이 선명하게 나오지 않게 된다.

편광필름을 90도 돌리면 투과되는 빛이 차단되기 때문에 매우 선명한 화면이 나온다. 문제는 **화면의 색이 반전된다.** &nbsp;(까만 부분은 하얗게, 하얀 부분은 까맣게)

그래서 기판에 칩을 달아서 LCD로 들어가는 데이터 자체를 반전시켜서 선명하고 멀쩡한 화면을 나오게 하는것이 Bivert 모드이다.

![image](/tumblr_files/tumblr_inline_nl7vbrWQb31sh674j.jpg)

([http://www.reddit.com/r/Gameboy/comments/2uu8ru/](http://www.reddit.com/r/Gameboy/comments/2uu8ru/))

왼쪽이 Bivert 모드가 적용된 화면. 사진으로 찍을때 이정도니 실제로 보면 엄청난 차이.

저는 게임보이를 개조해서 칩튠 만드는 용도로 쓸 것이고, 제가 칩튠 만들때 쓰는 소프트웨어인 LSDJ는 소프트웨어 자체적으로 반전된 팔레트를 제공하기 때문에 굳이 기판에 칩을 다는 번거로운 일을 할 필요는 없다.

**하지만 나는 별의 카비가 하고싶었기 때문에 인버터 칩을 샀다.**

<!-- more -->
![image](/tumblr_files/tumblr_inline_nl7vj7eBYt1sh674j.jpg)

**너무 작아…………..**

크기 비교를 위해 백원짜리에 올려놓고 찍었는데 정말로 작다.

납땜 기술이 안 좋은데다가 납땜 부위가 너무 작아 결국 다는것을 포기했다.(진짜로 엄청 작아서 잘 하는 사람이라고 달 수 있을지는 모르겠지만)

결국 그냥 LSDJ나 제대로 쓰자 하고서 편광필름을 색 반전이 되게 해놓은 채로 조립을 했다.

**그러나 별의 카비가 미친듯이 하고싶었다.**

그래서 생각한게 어차피 색 반전만 되면 되는거니 소프트웨어 적으로 해결할 방법은 없을까? 하고 찾아봤다.

그렇게 찾아보니 LSDJ가 반전 팔레트 지원을 하지 않을때 [롬파일을 수정해서 색을 반전시키는 방법에 대한 글](http://blog.gg8.se/wordpress/2012/03/04/how-to-patch-lsdj-to-use-an-inverted-palette/)이 있었다.

[Pan Docs(게임보이 스펙에 대해 정리해놓은 글)](http://gbdev.gg8.se/files/docs/mirrors/pandocs.html#videodisplay)에 의하면 게임보이의 메모리에서 팔레트가 저장되는 부분은 다음과 같다.

- FF47 - 배경
- FF48 - 오브젝트1
- FF49 - 오브젝트2

LSDJ의 경우 배경 팔레트가 딱 한번만 지정되기 때문에 코드 한부분만 수정하면 색 반전의 효과를 얻을 수 있었다. 그러나 게임의 경우 팔레트가 다이나믹하게 변경되는 부분(페이드 인/아웃)도 있고 오브젝트 팔레트도 쓰이기 때문에 훨씬 복잡하다.

여기서부터는 위의 글에서 얻은 정보를 기반으로 별의 카비를 색반전 시키는 내용이다.

* * *

필요 도구:

- [BGB 게임보이 에뮬레이터](http://bgb.bircd.org/)
- 색반전시킬 게임의 롬파일

##

## 1. 에뮬레이터 설정

BGB를 실행시키면 네모난 화면만 나온다. F11키를 누르면 설정창이 뜨는데, System 탭에서 Gameboy로 설정해주자.(이렇게 해야 게임보이랑 똑같이 코드가 실행되기 때문에 디버깅이 조금 더 쉬워진다.)

##

## 2. 롬파일 구동 및 디버거 실행

이제 네모난 화면에서 ESC키를 누르면 디버거가 실행된다. 먼저 File-Load ROM으로 롬파일을 불러와준다.

##

## 3. 팔레트 설정부 찾기

원래 글에서는 배경 팔레트 메모리 영역인 FF47에 값이 쓰일 경우에 Breakpoint를 걸고 코드를 진행시켜 어느 부분에서 팔레트를 바꾸는지를 찾았지만 게임의 경우 팔레트가 바뀌는 부분이 너무 많아 이렇게 찾을수는 없다.

대신 디버거에서 Ctrl+F키를 눌러 뜨는 검색창에&nbsp;“pal” 이라고 검색하여 팔레트 설정 코드를 찾을 수 있다. 이 코드와 바로 전에 실행되는 코드를 기록해주자. 중요한 부분은 롬파일상에서의 주소와 명령어이다.

ROMX:#### \<- #### 부분이 주소이다.

안타깝게도 데이터 카피만 가능하고 화면 그대로를 기록해주는 기능은 없어서 직접 타이핑했다.

기록하고 검색하고를 반복하다 보면 ROMX가 아닌 다른게 뜨는데 이 순간부터는 기록할 필요가 없다.

    018A 3E E4 ld a,E4018C E0 49 ld (ff00+49), a ;obj pal 101F2 FA 80 D0 ld a,(d080)01F5 E0 47 ld (ff00+47), a ;bg pal1E09 FA 80 D0 ld a,(d080)1E0C E0 47 ld (ff00+47), a ;bg pal1E1E 3E E4 ld a,E41E20 CB DE set 3,(hl)1E22 E0 47 ld (ff00+47), a ;bg pal1F4F EA 80 D0 ld (d080),a1F52 E0 47 ld (ff00+47), a ;bg pal1F54 E0 49 ld (ff00+49), a ;obj pal 11F72 EA 81 D0 ld (d081),a1F75 E0 48 ld (ff00+48), a ;obj pal 01F8B EA 80 D0 ld (d080),a1F8E E0 47 ld (ff00+47), a ;bg pal1F90 E0 49 ld (ff00+49), a ;obj pal 11FA5 EA 81 D0 ld (d081),a1FA8 E0 48 ld (ff00+48), a ;obj pal 0

이것이 정리한 코드. 중간에 왜 바로 전 코드가 아닌 전전코드까지 기록한것도 섞여있는지는 밑에서 설명할 예정이다.

##

## 4. 직접 값 반전시키기

여기서부터는 어셈블리 형식의 코드를 읽을 줄 아는것이 편하다. [Pan Docs에 보면 Instruction Set 문서가 잘 정리되어 있다.](http://gbdev.gg8.se/files/docs/mirrors/pandocs.html#cpuinstructionset)&nbsp;

먼저 018A 번지의 코드를 고쳐보자. Ctrl+G를 눌러 해당 번지로 이동이 가능하다.

    018A 3E E4       ld a,E4018C E0 49       ld (ff00+49), a ;obj pal 1

위 코드는 레지스터 a에 값 E4를 넣고, 레지스터 a의 값을 FF49에 넣는, 즉 FF49=E4 를 하는 코드이다.

이렇게 직접 값을 대응시키는 경우는 반전된 값을 입력하는 것으로 쉽게 팔레트 반전이 가능하다.

(없을 것 같지만)비 프로그래머인데 이 글을 보고 따라하는 사람을 위해 16진수 값을 쉽게 반전시키는 법도 설명함:

1. 계산기를 실행한다.
2. 보기-프로그래머용 으로 바꾼다.
3. Hex에 체크하고 E4를 입력한다.
4. Xor를 누르고 FF을 입력한뒤 엔터를 친다.
5. 1B가 되는데 이게 반전된 값이다.

디버거 화면에서 018A 줄이 선택된 상태에서 아래의 코드를 입력한다.
(코드 입력은 그냥 치기 시작해도 되고 우클릭해서 Modify code/data 메뉴로 창을 열어도 된다)

    ld a,1B

별의 카비의 경우 이렇게 직접 값을 대응시키는 경우가 하나 더 있다.

    1E1E 3E E4       ld a,E41E20 CB DE       set 3,(hl)1E22 E0 47       ld (ff00+47), a ;bg pal

단계 3에서 설명 안한것과 어셈블리를 읽을 줄 아는것이 편하다고 했던게 이런 경우인데, 이것도 값 E4를 직접 대응시키는 코드이다. 단지 중간에 뭔가 섞여있을 뿐인데 이&nbsp;“뭔가”가 영향을 미칠지 안 미칠지를 파악하려면 코드를 읽을 줄 알아야 한다.

이번 단계는 봐도 잘 모르겠다, 애매하다 싶으면 건너뛰어도 된다. 단지 나중에 할 일이 많아질 뿐이다…

##

## 5. 동적으로 값 반전시키기

    #Group 101F2 FA 80 D0    ld a,(d080)01F5 E0 47       ld (ff00+47), a ;bg pal1E09 FA 80 D0    ld a,(d080)1E0C E0 47       ld (ff00+47), a ;bg pal#Group 21F4F EA 80 D0    ld (d080),a1F52 E0 47       ld (ff00+47), a ;bg pal
    1F54 E0 49       ld (ff00+49), a ;obj pal 1

    1F8B EA 80 D0    ld (d080),a
    1F8E E0 47       ld (ff00+47), a ;bg pal
    1F90 E0 49       ld (ff00+49), a ;obj pal 1

    #Group 3
    1F72 EA 81 D0    ld (d081),a
    1F75 E0 48       ld (ff00+48), a ;obj pal 0

    1FA5 EA 81 D0    ld (d081),a
    1FA8 E0 48       ld (ff00+48), a ;obj pal 0

단계 4에서 쳐낸 두부분을 제외하고 이 코드들이 남았다. 이 코드들을 위처럼 “팔레트 변경 코드 바로 전에 실행하는 코드가 같은것들 끼리 묶는다.

이제부터 롬의 빈 영역에 값을 반전시키는 코드를 삽입하고 이것을 call 명령어를 통해 호출하는 것이다.

롬의 빈 영역을 찾는 방법은 nop 명령어-00이 연속으로 있는 부분(가끔 rst 38-FF)이 빈 영역인데 이번의 경우 0000번부터 빈 공간이 꽤 있기때문에 이부분을 사용한다. 묶어놓은 그룹의 갯수만큼 다른 코드가 필요하다.

또 지금부터는 코드의 길이도 잘 봐야 한다.

    #Group 1
    01F2 FA 80 D0    ld a,(d080)
    01F5 E0 47       ld (ff00+47), a ;bg pal

이 경우 FA 80 D0의 길이는 3바이트 인데 call 명령어도 3바이트를 차지하기 때문에 딱 적당한 경우이다. 별의 카비의 경우 4번 단계를 잘 했다면 전부 딱 들어맞기 때문에 매우 쉽다.

0000 부분에 다음과 같은 코드를 입력해주자. (여러줄을 한번에 입력하고 싶다면 Shift-Enter를 누르면된다)

    ld a,(D080)
    xor a,FF
    ret

그리고 01F2번지의 코드를 이렇게 바꿔주자.

    call 0000

그러면 이런 형태가 될것이다.

    #새로 입력한 부분
    0000 FA 80 D0 ld a,(d080)
    0003 EE FF xor a,FF
    0005 C9 ret

    #고친 부분
    01F2 C0 00 00    call 0000
    01F5 E0 47       ld (ff00+47), a ;bg pal

새로 입력한 부분에서 고친 부분의 코드를 입력해준 이유와 그룹으로 묶었던 이유는 위 코드가 설명해준다.&nbsp;사실 값 반전은 xor a,FF 한줄 뿐이지만 원래 코드를 살리면서 값을 반전하는 코드도 끼워넣어야 하기 때문에 이런 복잡한 과정을 거쳐야한다.

그룹2, 3에 대해서도 첫 줄만 원본을 유지하면서 똑같이 만들어준다. 그러면 아래와 같이 된다.

![image](/tumblr_files/tumblr_inline_nl7vczSstj1sh674j.png)

그룹 2에 해당하는 첫 줄들은 call 0006, 3은 call 000C로 바꿔치기 하면 된다.

이 경우는 바꿔치기할 명령어의 크기가 3바이트로 동일했기 때문에 쉬웠는데, 아닌 경우에는 다르게 해야한다. 단계4에서 봤던 코드를 다시 보자.

    1E1E 3E E4       ld a,E4
    1E20 CB DE       set 3,(hl)
    1E22 E0 47       ld (ff00+47), a ;bg pal

1E20번지의 명령어가 2바이트로 이대로 call 명령어를 입력한다면 1E22번지의 명령어 1바이트가 덮어써지게 된다. 이런 경우는 이렇게 해야한다.

    #새로 입력한 부분
    0012 3E E4     ld a,E4
    0014 CB DE       set 3,(hl)
    0016 EE FF       xor a,FF
    0018 C9          ret

    #고친 부분
    1E1E C0 12 00    call 0012
    1E1E 00    nop
    1E22 E0 47       ld (ff00+47), a ;bg pal

nop은 아무것도 안 하는 명령어이기 때문에 빈 공간을 채우는데 활용하면 된다.

##

## 6. 끝!

![image](/tumblr_files/tumblr_inline_nl7vdqZrJp1sh674j.png)

이제 Run-Reset 메뉴를 눌러 초기화를 한뒤 화면 부분을 클릭하면 이렇게 반전된 화면이 뜨는것을 확인할 수 있다.

File-Save as를 눌러 롬파일을 저장하면 된다.

![image](/tumblr_files/tumblr_inline_nl7vr8QNzF1sh674j.jpg)

이 사진은 실제 기기에서 실행한 사진이다.

##

## 7. 기타 게임의 경우

- Super Mario Land: 코드 끼워넣기 없이 값 변경으로만도 가능함
- Kirby’s Dream Land 2: 디버거 검색 기능으로 못 찾는 부분이 있음. FF47, FF48, FF49 write시 breakpoint를 걸어 찾아야함
- Cosmo Tank: 동굴 들어갈때까지 진행해야 잡히는 팔레트 변경 코드도 있음
- Beatmania GB: 매우 어렵다. 얼마나 어려운지는 아래를 보면 됨

비트매니아 GB

바꿔치기로 변경한 부분 다수 + 코드 많이 끼워넣어야 함

끼워넣은 코드:

![image](/tumblr_files/tumblr_inline_nl81lfy10B1sh674j.png)

바꾼 부분들:

![image](/tumblr_files/tumblr_inline_nl81mapSXZ1sh674j.png)

![image](/tumblr_files/tumblr_inline_nl81mgyiv71sh674j.png)

![image](/tumblr_files/tumblr_inline_nl81mky3j01sh674j.png)
