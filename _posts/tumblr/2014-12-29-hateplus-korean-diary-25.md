---
layout: post
title: Hate Plus 한국어화 작업일지 - 25 (마지막장)
date: '2014-12-29T22:31:00+09:00'
tags:
- hate plus 한국어화 작업일지
tumblr_url: https://blog.iamghost.kr/post/106508393503/hateplus-korean-diary-25
redirect_from:
- /post/106508393503/hateplus-korean-diary-25
---
2014년 12월 29일

아침 7시 30분

근 한달동안 소통이 되지 않았던 크리스틴 누나께서 이상한 메일을 보내왔다.

“세이브 관련 문제가 있어서 이전 버전으로 롤백할 것이고 한국어화 릴리즈는 조금 뒤로 미뤄야 할 거 같다” 라고…

막 깬 참이라 상황 이해가 안됐는데 이런 저런 정황을 조합해보니 자고있는 사이 이런 일이 일어난것이다.

1. 헤이트 플러스 한국어 데이터를 스팀판의 메인으로 업로드 했음.
2. 그러나 세이브 파일 마이그레이션(아날로그: 어 헤이트 스토리-\>헤이트 플러스) 문제가 있다.
3. 한국어 사용자 뿐만 아니라 영문판에게도 타격이 가는데다 고칠 시간이 없으니 임시로 롤백하겠다.

…………….

지금 한달만에 릴리즈가 될 기회가 됐는데 다시 롤백을 한다고!!!

그래서 일단 이렇게 보냈다.

1. 일단 베타 테스트때 썼던 베타 브랜치를 최신으로 업데이트 하고 비밀번호를 없애 공개로 바꿔서 베타 버전으로라도 릴리즈 하자.
2. 세이브 문제가 뭔지는 모르겠지만 해결하고 나서 최신 버전으로 합치자. 문제가 되는 세이브 파일들을 보내달라 직접 고쳐볼테니

이러고 나서 잠들었다.

오전 9시 23분

답장이 왔다.

“롤백을 했는데 우리가 전에 고쳤던 그 버그랑은 상관이 없는거 같다. 왜 이전에는 안 튀어 나왔는지 모르겠는데 아무튼 한국어를 뺀 버전을 올려놨다. 잠시 상황을 봐야겠다.”

뭔 소리야!!!!

아무튼 뭐 상황을 지켜본다니까 어쩔 수 없는거 같다.

그렇게 일단 이해한 상황에서 학교를 갔다.

오후 3시경

**한국어가 나온대!!!!!!!!!!!!!!!!!!!**

도저히 사태 파악이 안되서 이분 저분에게 물어본 결과 “한글 선택"만 막았고 데이터는 담긴 채로 릴리즈가 된 것 같다.

그리고 그런 상태로 모 게임 커뮤니티의 뉴스 소식에도 올라가게 되었다.

아 이게 뭐야… 이건 뭐 정식 릴리즈 한것도 아니고 안한것도 아니고…

오후 7시경

위에서 말한 "세이브 버그"가 아직도 존재한다는 것을 확실히 할 수 있었다. 일단 집에 가서 고쳐야 하니 세이브 파일들을 요청했는데 다행히 잘 보내주셨다…

오후 8시 50분쯤

이런 문제가 있는줄도 몰랐는데 크리스틴 누나가 일단 세이브 마이그레이션은 못하지만 게임이 튕기지는 않게 땜빵을 해놓은 상태였다.

자꾸 헤이트 플러스에 존재하지 않는 요소들을 세이브 파일들이 요청해서 생기는 문제인데… 정말 모르겠다…

오후 9시쯤

도저히 해결이 안되서 혹시 헤이트 플러스의 기반인 아날로그: 어 헤이트 스토리에 실마리가 있지 않을까 하여 게임을 다운로드 받았다.

그런데 뭔가 이상한, 전에 작업했을때는 없는 매우 수상하게 생긴 파일 하나가 있었다.

"sorry\_about\_this.rpa”

뭔 파일이야 이게!!!!!

매우 수상하여 압축을 풀고 디컴파일 하고 확인해보니 일본어 번역과 관련된 파일들이었다.

그리고 위에서 찾아대던 그 “존재하지 않는 요소"들을 여기서 찾았다.

아 뭐야 한글화 때문에 생긴 버그가 아니잖아!!!!!!!

오후 10시쯤

그 외에도 분명 베타 테스팅때 고쳤던 버그인데 부활한 버그가 있었는데 이건 패키징이 잘못 되어 그런 것이었다.

임시로 핫픽스를 배포하고 메일로도 버그에 대해 설명했다.

으아 힘들다.

