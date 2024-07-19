---
layout: post
title: PS Vita - 보안, VHBL, eCFW
date: '2014-06-11T03:15:00+09:00'
tags:
- code injection
- buffer overflow
- security
tumblr_url: https://blog.iamghost.kr/post/88392170873/ps-vita-%EB%B3%B4%EC%95%88-vhbl-ecfw
redirect_from:
- /post/88392170873/ps-vita-%EB%B3%B4%EC%95%88-vhbl-ecfw
---
2011년 소니 보안부서를 뒤흔들어놓은 사건이 하나 있다. iPhone 해킹으로 유명한 [GeoHot이 PS3의 루트 키를 얻어내는데 성공](http://kotaku.com/5723105/hacker-claims-to-have-the-ps3s-front-door-keys)한 사건이다.

루트 키를 사용하면 허가되지 않은 비공식 프로그램(Homebrew)를 별도의 보안 무력화 절차 없이 마음대로 실행할 수 있게 된다.

![image](/tumblr_files/tumblr_inline_pk0m78UrAN1sh674j_540.jpg)

이런 중요한 루트 키가 유출된것엔 이유가 있다. 소니 엔지니어가 매우 귀찮았는지 임의의 정수를 반환해야 하는함수에 무조건 4를 반환하게 해놓은 것이다. 그&nbsp;결과 [무작위 대입에 필요한 경우의 수가 획기적으로 줄어 간단하게 키를 얻어낼](http://www.exophase.com/20540/hackers-describe-ps3-security-as-epic-fail-gain-unrestricted-access/) 수 있었다.

PlayStation 3 얘기를 하자면 PS3의 루트 키가 공개되면서 동일한 방법으로 PSP의 키도 공개가 되었다. 이를 이용해 모든 PSP 기기에서 허가받지 않은 프로그램을 실행하는 것이 가능해졌다. 게다가 PSP는 업데이트를 중단하지 오래 되었고 현재 시점에선 생산도 중단되었기 때문에 사실상 완벽히 뚫린 기기이다.

<!-- more -->

PSP가 이렇게 엉망진창으로 뚫리기 전 3000번대 Slim PSP는 무적의 기기였던 시점이 있다. 이때 해커들이 홈브류 프로그램을 실행하기 위해 사용했던 방법이 있는데 바로 [Grip Shift라는 게임에서 Buffer-overflow](http://youtu.be/i6IMjCCEOz0)를 일으키는 것이다. 같은 방법으로 Patapon 2 Demo를 이용한 홈브류 실행도 가능하단게 밝혀졌고 이를 사용해 각종 홈브류를 쉽게 실행할 수 있는 로더인 [HBL(Half-Byte Loader)](http://wololo.net/half-byte-loader-for-patapon-2-up-to-ofw-6-20/)가 나왔다.

C언어를 공부해본 사람이라면 ‘널 문자(0x00)'에 대해 들어본적이 있을 것이다. C언어의 문자열 처리는 시작 지점에서 널 문자가 나올때까지 탐색하는 방식으로 구현되어 있다.&nbsp;

0 1 2 3 4 5

H E L L O 0x00

위와 같은 문자열이 있다고 하면. 0번부터 시작하여 널 문자가 나올때까지 계속 탐색을 한다. 5번에서 0x00이 발견되었으므로 문자열은 0~4의 값인 HELLO가 되는 것이다.

그럼 널 문자가 없어지면 어떨까? 문자열 출력시에는 문자열의 끝을 찾지 못해 메모리 경계를 넘어서 이상한 값을 마구 출력할 것이고, 문자열 복사 등의 연산은 **할당된 메모리를 벗어난 영역의 값을 수정** 할 수 있게 된다.

컴퓨터에는 값을 임시로 저장하는 버퍼 메모리가 있는데 이런 취약점을 사용하면 버퍼 메모리를 넘어 시스템의 메모리를 변조하는 것이 가능하다. 이런 공격 기법을 버퍼 오버플로우 공격이라 한다.

![image](/tumblr_files/tumblr_inline_pk0m78Vkgy1sh674j_540.jpg)

위 사진은 Grip Shift 세이브데이터를 수정한 모습이다. 이름의 글자는 제한되어 있지만 널 문자를 제거한뒤 마구 데이터를 삽입하였다.

![image](/tumblr_files/tumblr_inline_pk0m79vwfS1sh674j_540.jpg)

그 결과 게임은 에러를 내면서 뻗어버리는데 에러가 난 이유는 다음 실행될 코드의 주소가 담긴 ra(return address)의 주소값이 이상하게 변경되어 버렸기 때문이다.

return address의 변경이 가능했다는 것은 세이브 데이터에 임의의 코드를 삽입한뒤 해당 코드가 시작되는 부분으로 주소를 변경해주면 해커가 임의로 삽입한 프로그램을 실행할 수 있다는 것을 의미한다.

그럼 대체 왜 제목에는 Vita 라고 적어놓고 지금 와서 이런 얘기를 하고 있는걸까?

PS3과 PSP에서 각종 공포의 쓴맛을 맛본 소니는 정신을 차리고 Vita 이후 기기에 보안을 대폭 강화하였다.&nbsp;현재까지 Sony Vita에서 네이티브 코드를 실행할 수 있는 취약점은 발견되지 않았다. (즉 안 뚫렸다.)&nbsp;

현재 Vita에는 여러 종류의 보안 기술들이 들어가있다.

- 서명된 패키지만 LiveArea에 표시됨
- 서명된 실행파일만 실행 가능
- 대부분의 앱이&nbsp;[Sandbox](http://ko.wikipedia.org/wiki/%EC%83%8C%EB%93%9C%EB%B0%95%EC%8A%A4_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EB%B3%B4%EC%95%88))화 되어있음
- PSN과 통신시 SSL 접속 사용
- SSL 통신시 사용하는 인증서가 펌웨어 버전별로 달라진다.[&nbsp;즉 네트워크 변조를 통해 버전을 속여](https://github.com/iAmGhost/VitaUpdateBlocker)도 구버전 펌웨어에선 통신 자체가 불가능해진다.&nbsp;
- PSP와 달리 파일시스템에 직접 접근할 수 없다.
- 컨텐츠 전송을 하는 CMA는 중간에서 모든 파일을 암호화한다.
- 개발자 킷 단속을 잘 하고 있다.

정말로 Vita의 보안이 매우 견고한 것인지 실력있는 해커가 없는것인진 모르겠지만 현재로썬 무적이다. 그러나 해커들은 여기서 한가지 취약점을 발견한다. 바로 PSP 게임의 Buffer-overflow이다.

PS Vita는 PSP와 매우 유사한 구조를 가졌고, PSP와 동일한 환경도 구성되어 있다. UMD Drive는 없지만 PSN에서 PSP 게임을 다운로드 받아 플레이 하는것도 가능하다.

위에 적은대로 패키지 서명/CMA 암호화 등이 있기 때문에 임의로 게임을 집어넣는건 불가능하지만 PSN에서 PSP 게임을 받는것은 가능하고, Vita의 PSP 구동 환경은 실제 PSP와 거의 동일하기 때문에 [PSP 모드로 한정되어 있지만 홈브류를 구동](http://youtu.be/2VQbDd9iLJI)하는 것이 가능해졌다. 그리고 위에서 말한 HBL의 Vita 최적화 버전인&nbsp;[VHBL(Vita Half-Byte Loader)](http://wololo.net/vhbl/)가 나왔다.

이 사태를 인지한 소니는 황당하게도 PSN에서 취약점이 있는 게임을 삭제한다. 삭제하고 나면 구매도 불가능해지고 이미 구매한 사람도 다운로드를 할 수 없게 된다.&nbsp;이후에도 해커들은 같은 방법으로 다른 게임들을 해킹해 나갔고 소니는 게임들을 삭제해나갔다. 취약점을 차단한뒤 다시 게임을 올리기도 했다.

막고 뚫는 창과 방패의 싸움이 반복되는 도중 해커 Total\_Noob은 PSP및 Vita에 사용되는 인증서 관련 모듈인 certloader에서 단순히 추가 프로그램을 돌리는게 아닌 시스템 전체(PSP 환경 한정이지만)를 장악할 수 있는 Kernel Exploit을 발견하게 된다. 심지어는 이를 사용해 [Vita에서 XMB 기반의 커스텀 펌웨어를 실행하는 eCFW(TN-V)](http://youtu.be/BnkjQr2ehTo)를 릴리즈 한다. 이를 이용하면 PSP CFW에서 가능했던 모든 것들을 Vita에서도 할 수 있게 된다.

소니는 여기서도 창과 방패 싸움을 계속하다 결국 3.02 펌웨어를 기점으로 PSP 환경 자체를 고쳐 certloader 및 각종 VHBL 구동 가능 취약점을 차단했고 삭제된 게임들도 다시 전부 복구시켰다.

여기까지가 현재 진행된 PS Vita 해킹의 전부이다. 이 이후 [해커들과 소니는 다시 VHBL과 관련된 이용한 창과 방패 싸움](http://wololo.net/2014/05/29/exploit-game-mystylist-got-removed-from-the-playstation-store/)을 하고 있고, [조만간 eCFW를 구동 가능하게 하는 커널 취약점이 또 공개될거란 기대](http://wololo.net/2014/06/06/will-there-be-a-new-release-of-a-ps-vita-ecfw-in-near-future/)도 있다. 그러나 아직까지도 Vita 환경에서 비허가 코드를 실행한 사람은 존재하지 않는다.

