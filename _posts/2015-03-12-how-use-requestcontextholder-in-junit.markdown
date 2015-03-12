---
layout: post
title:  Spring RequestContextHolder를 유닛테스트에서 Mocking하는 방법
date:    2015/03/12 23:36
categories: java
---
MVC의 Controller가 아닌 Service 계층의 메소드를 테스트할 때, RequestContextHolder를 다뤄야할 때가 있습니다.

이 때 유용한 작은 코드입니다.

{% gist 4eeb1bb37b88302c68c1%}
