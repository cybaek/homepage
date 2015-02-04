---
layout: post
title:  메소드 이름은 명확하게
date:    2008/02/25 10:00
categories: programming
---


{% highlight java %}
public void setTimeout(int timeout);
{% endhighlight %}

위 메소드 인자 timeout의 단위는 sec 일까요? ms 일까요?

레퍼런스를 보기 전까지는 아무도 모릅니다. 하지만 아래와 같이 바꾸면 쉽게 알 수 있습니다.

{% highlight java %}
public void setTimeoutSeconds(int timeout);
{% endhighlight %}

단위가 ms인 곳에 2, 3을 지정해서 결과가 나왔다 안나왔다 하여 헤메는 모습, 반대로 sec인 곳에 2000, 3000을 지정해서 타임아웃 값이 의미가 없었던 경우를 봤습니다.

모두 메소드 이름이 명확했다면 그런 실수는 하지 않았을 것입니다.
