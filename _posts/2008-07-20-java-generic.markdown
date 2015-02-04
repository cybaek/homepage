---
layout: post
title:  자바 제네릭
date:    2008/07/20 02:35
categories: java generic
---
먼저, 아래 내용은 <Effective Java, 2nd> Item28의 일부를 정리한 것임을 밝힙니다. 

--- 아래 ---

어떠한 타입도 담을 수 있는 Stack 클래스가 있습니다.

{% highlight java %}
public class Stack<E> {
  public Stack();
  public void push(E e);
  public E pop();
  public boolean isEmpty();
}
{% endhighlight %}

pushAll메소드를 구현하여 덧붙이면 다음과 같이 작성할 수 있습니다.

{% highlight java %}
public void pushAll(Iterable<E> src) {
  for (E e : src)
    push(e);
}
{% endhighlight %}

이렇게 작성한 메소드를 다음처럼 사용할 수도 있습니다.

{% highlight java %}
Stack<Number> numberStack = new Stack<Number>();
Iterable<Integer> integers = ...;
numberStack.pushAll(integers);
{% endhighlight %}

사실 이 코드는 컴파일조차 할 수 없습니다.

Integer가 Number를 상속했기에 당연히 되리라 생각할 수 있지만, 컴파일 타임에 Iterable&lt;Integer>와 Iterable&lt;Number>는 완전히 다른 타입입니다. 제네릭에서 가장 착각하기 쉬운 부분입니다.

이런 경우에는 'bounded wildcard type'을 이용하면 '상식대로' 돌아가도록 개선할 수 있습니다.

{% highlight java %}
public void pushAll(Iterable<? extends E> src) {
  for (E e : src) 
    push(e);
}
{% endhighlight %}

'Iterable<? extends E>'는 'E의 하위타입에 대한 Iterable' 이라고 읽습니다. 그렇다고 E를 못넘기는 것은 아닙니다. E와 E의 하위타입 모두 가능합니다.

참고로, 여기서 변수 src는 정보를 생산(e)하고 있지, 다른 변수 값을 이용하지 않습니다. 이 경우 src를 생산자(producer)라고 부를 수 있습니다. 이런 변수를 'producer'라고 부르는 것은 &lt;Effective Java>의 지은이 'Joshua Bloch'가 임의로 붙인 것 같습니다. 참고라고 적었지만 일단 외워두는 것이 좋습니다. (이유는 다음 글에)

다음 글에서는 반대 경우를 설명 드리겠습니다. 
