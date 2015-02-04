---
layout: post
title:  자바의 DNS 이름 풀기(name resolving) TTL 설정 방법
date:    2012/02/16 15:24
categories: java dns
---
$JAVA_HOME/jre/lib/security/java.security 파일에 TTL 5분을 설정합니다.

{% highlight txt %}
networkaddress.cache.ttl=300
{% endhighlight %}

NSCD 데몬을 사용할 경우에는 /etc/nscd.conf에 아래 설정도 추가합니다.

{% highlight txt %}
positive-time-to-live hosts 300
{% endhighlight %}

그리고 데몬을 재구동합니다.

{% highlight shell %}
service nscd restart
{% endhighlight %}
