---
layout: post
title:  클래스 패스에 둔 파일의 절대 경로를 알고 싶을 때
date:    2007/12/10 18:51
categories: java
---
클래스 패스에 있는 파일을 읽는 방법(ClassLoader, Class, ResourceBundle)은 많습니다. 반면에 그렇게 읽은 파일의 절대 경로를 구하는 방법은 찾기 쉽지 않았습니다.

아래 스프링에 있는 ClassPathResource를 이용한 코드 조각이 있습니다.

{% highlight java %}
import java.io.File;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;

Resource r = 
  new ClassPathResource("com/cybaek/test/core/hello.doc");
File f = r.getFile();
String path = f.getAbsolutePath();
{% endhighlight %}

