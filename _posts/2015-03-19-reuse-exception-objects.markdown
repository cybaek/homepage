---
layout: post
title:  Exception 객체 재활용하기
date:    2015/03/19 16:00
categories: java
---
다음과 같은 코드를 많이 접하게 됩니다.

{% highlight java %}
if (result == null) {
	throw new ApiFailedException(ErrorCodes.SERVER_FILE_UPLOAD_ERROR);
}
{% endhighlight %}

이런 Exception 객체의 경우 immutable하고 생명주기도 짧습니다. Flyweight 패턴을 사용하기 딱이죠.
