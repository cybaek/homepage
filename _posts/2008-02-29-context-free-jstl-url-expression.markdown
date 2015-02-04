---
layout: post
title:  JSP에서 컨텍스트에 영향을 받지 않는 URL 지정하는 법
date:    2008/02/29 08:08
categories: java jstl
---

JSP에서 같은 컨텍스트에 있는 주소를 지정하는 방법입니다. 

EL을 이용합니다.

{% highlight java %}
${pageContext.request.contextPath}/a.jsp
{% endhighlight %}

깁니다. 당연히 못 외웁니다. ^^

JSTL을 이용합니다.

{% highlight html %}
<c:url value="/a.jsp" />
{% endhighlight %}

EL보다 훨씬 낫지요?

JSTL을 이용하면 URL 뒤에 붙는 매개변수도 우아하게(?) 처리할 수 있습니다.