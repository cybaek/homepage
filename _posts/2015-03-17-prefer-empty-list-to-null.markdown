---
layout: post
title:  빈 목록은 null이 아니라 빈 목록을 반환하도록
date:    2015/03/17 14:30
categories: java
---
DAO를 호출하는 코드를 보면 다음과 같은 형태를 많이 보게 됩니다.

{% highlight java %}
List<User> users = userDao.selectListByName(name);
if (users != null) {
	for (User user : users) {
        // ...
    }
}
{% endhighlight %}

목록이 없을 때, null을 반환하는지 빈 목록을 반환하는지 잘 모르니 그냥 앞에처럼 '방어'코드를 짜는 것입니다.

쉽게 볼 수 있는 안티패턴입니다. 우선 목록이 없을 때, null인지 아닌지 스펙을 확인하는 것이 먼저이고, 그 다음으로 null이라면 빈 목록을 리턴하도록 바꾸는 것이 좋습니다. 빈 목록을 반환할 경우 다음과 같이 간결합니다.

{% highlight java %}
List<User> users = userDao.selectByName(name);
for (User user : users) {
    // ...
}
{% endhighlight %}

참고로 빈 목록을 반환할 때 사용하기 좋은 편의 메소드가 있습니다. 이것을 이용하면 size 0인 컬렉션을 공유하여 메모리를 보다 효율적으로 사용할 수 있습니다.

{% highlight java %}
static <T> Set<T> Collections.emptySet(); // Returns an empty set (immutable).
static <K,V> Map<K,V> Collections.emptyMap(); // Returns an empty map (immutable).
static <T> List<T> Collections.emptyList()// Returns an empty list (immutable).
{% endhighlight %}

&lt;Effective Java, 2nd> 규칙 43에서 이와 관련한 자세한 내용이 있습니다.
