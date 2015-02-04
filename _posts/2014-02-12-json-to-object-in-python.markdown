---
layout: post
title:  파이선에서 object_hook을 이용하여 JSON 읽기
date:    2014/02/12
categories: python json
---


{% highlight json %}
{
 "name": "cybaek",
 "detail" : { "last": "baek" },
 "emails": [ "cybaek@xxx.com", "cybaek@yyy.com" ]
 }
{% endhighlight %}
 
앞의 Json에서 name 값을 읽을 때 보통 다음과 같이 코딩합니다.


{% highlight python %}
import json
data = json.loads("...")
print data["name"]
{% endhighlight %}

http://docs.python.org/2.7/library/json.html 문서를 보면 object_hook을 넘길 수 있는데요. 이것을 활용하면 다음 예제처럼 보다 간결하게 데이터를 읽을 수 있습니다.


{% highlight python %}
import json
s = """
 {
 "name": "cybaek",
 "detail" : { "last": "baek" },
 "emails": [ "cybaek@xxx.com", "cybaek@yyy.com" ]
 }
 """
class JsonObject:
  def __init__(self, d):
    self.__dict__ = d
data = json.loads(s, object_hook=JsonObject)
 
print data.name
print data.detail
print data.detail.last
for email in data.emails:
  print email
print data.emails[0]
{% endhighlight %}

