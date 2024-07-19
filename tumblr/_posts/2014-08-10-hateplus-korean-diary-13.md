---
layout: post
title: Hate Plus 한국어화 작업일지 - 13
date: '2014-08-10T01:14:00+09:00'
tags:
- hate plus
- hate plus 한국어화 작업일지
tumblr_url: https://blog.iamghost.kr/post/94255911563/hateplus-korean-diary-13
redirect_from:
- /post/94255911563/hateplus-korean-diary-13
---
2014년 8월 10일

번역을 이미 했지만 제대로 출력이 안 되는 텍스트가 무지 많다.

고치다보니까 이들의 패턴을 알게 되었다.

1. 호칭이 다른 텍스트들

영문판에선 Mr, Ms, Miss 등으로 호칭을 다양화 했는데 한국어판에선 “선생님"으로 통일했다.

(이거 왜 이렇게 한건지 모르겠는데 신의 한수였는듯…)

이거 다 다른 문장으로 나올 줄 알고 원문을 이런식으로 받았었는데:

Hey… one last thing, Miss Investigator?
Hey… one last thing, Ms Investigator?
Hey… one last thing, Mr Investigator?
Hey… one last thing, Investigator?

게임상에서는 이런식으로 처리하고 있었다.

Hey… one last thing, [title]Investigator?

원래는 Ren'Py가 [title]부분을 출력하기 전에 바꿔주는데, 대사 번역이 적용되는 시점은 이거보다 훨씬 전이다.

그래서 치환되기 전의 문장을 그대로 찾은뒤 바꿔야 하는 것.

2. 조건부 조립식 텍스트들

인물 프로필 텍스트들은 조립식이다. 진행에 따라 계속 설명이 바뀌는데 이건 또 별개의 텍스트를 독립된 문장으로 본다.

예를 들자면:

Councillor Kim was the grandfather of Kim So-yi… Old \*Mute was pretty antagonistic towards him… he was the Councillor of Engineering.
Former Councillor Kim was the grandfather of Kim So-yi… Old \*Mute was pretty antagonistic towards him… he was the Councillor of Engineering.

이 둘은 다른 문장이다…

이들 조합이 상당히 많아서 번역이 안 했는데 됐다고 착각하기도 하고 그런다.

