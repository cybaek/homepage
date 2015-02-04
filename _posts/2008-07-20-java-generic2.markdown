---
layout: post
title:  자바 제네릭2
date:    2008/07/20 03:30
categories: java generic
---

pushAll에 이어 popAll을 추가 구현해 보겠습니다. 단순하게 제네릭을 이용하면 아마도 다음 코드와 비슷할 것입니다.

{% highlight java %}
public void popAll(Collection<E> dst) {
  while(!isEmpty()) 
    dst.add(pop());
}
{% endhighlight %}

그리고 popAll을 다음처럼 호출할 것입니다.

{% highlight java %}
Stack<Number> numberStack = new Stack<Number>();
Collection<Object> objects = ...;
numberStack.popAll(objects);
{% endhighlight %}

이 코드 역시 컴파일 할 수 없습니다. Collection&lt;Object>와 Collection&lt;Number>는 다릅니다.

앞에 코드는 Object 형 묶음인 objects변수에  Number형을 싹 꺼내서 담으려고 합니다. 이 경우는 앞 글에서 언급한 <? extends E>로 해결할 수 없습니다. 'Object extends Number'와 같은 의미구문은 자바세상에서 절대 존재할 수 없습니다. 이 경우는 역으로 &lt;E extends ?> 가 맞습니다. 그렇다고 그렇게 코드를 작성하지는 못하고, super라는 키워드를 이용합니다. <? super E>

dst변수는 데이터를 이용하는 소비자(consumer)입니다. 제 관찰 기준으로, 매개변수의 메소드에 인자를 넘겨 호출하면 소비자입니다. (혹시 이 기준이 틀리다면 댓글 ^^)

이제 제네릭을 이용할 때, 인자에 단순히 E라고 적을 것이 아니라 상황에 따라 extends, 혹은 super를 적어야 한다는 것을 아셨습니다. 조슈아 아저씨가 쉽게 외우도록 한국형 공식을 만들었습니다.

PECS

약어입니다. producer-extends, consumer-super. 

JavaOne2008에서 조슈아 아저씨는 작년에 이 부분 설명이 좀 어려웠다고 고백하며 미안하다 했습니다. 아무래도 어느 정도의 암기가 필요했다고 생각한 것 같습니다. 저도 한 번 설명듣고 PECS를 외우고 나니, 다른 보기를 들 때 이해하는데 한결 나았습니다. 참고로 &lt;Effective Java, 2nd> 책에도 크게 약어를 적어 놓았습니다.

PECS stands for producer-extends, consumer-super.

주의할 점이 있습니다.

한 변수가 P와 C의 역할을 다 하는 경우가 있습니다. 그 때는 그냥 E만 적습니다. (제네릭 타입)

두 번째로 메소드를 호출하는 쪽에서는, 구현 코드에서 extends를 썼는지 super를 썼는지 의식하지 않도록 메소드를 디자인해야합니다. 앞 두 글의 클라이언트 코드는 구현 쪽을 신경쓰지 않았습니다. 메소드 구현부에서 클라이언트의 의도대로 수행되도록 적절히 extends나 super 키워드를 적었습니다. 
