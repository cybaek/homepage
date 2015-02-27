---
layout: post
title:  프로그래밍 언어의 역사 - Objective-C
date:    2015/02/27 09:30
categories: programming
---

# 간략한 역사
  * C + Smalltalk
  * 1980년대 톰 러브와 브래드 콕스가 개발
  * 후에 Objective-C와 강력한 클래스 라이브러리를 결합한 상품을 파는 회사를 설립
  * 1988년 NeXT는 이 회사에서 Objective-C 라이센스를 받음
  * 2006년 애플은 Objective-C 2.0을 발표
    * 현대적인 가비지 컬렉션, 문법 기능 향상, 런타임 성능 개선, 64비트 지원 등


# [] 문법

## 함수를 호출했느냐, 메시지를 전달했느냐
doSomething()을 **호출**

{% highlight objectivec%}
obj.doSomething();
{% endhighlight %}

obj의 doSomething()에 a, b, c **인자를 전달**

{% highlight objectivec%}
obj.doSomething(a, b, c)
{% endhighlight %}

obj에서 doSomething **메시지를 전달**

{% highlight objectivec%}
[obj doSomething];
{% endhighlight %}

더 **구체적인 메시지 전달**
{% highlight objectivec%}
ShiftyMethods *shifty = [ShiftyMethods new];
int i = 1;
[shifty performSelector:@selector(incrementAnInteger:) 
             withObject:(id)&i];
{% endhighlight %}

## Smalltalk를 잠깐 엿보면
사전 객체에 값을 넣는 예제

{% highlight smalltalk%}
y := Dictionary new
y at: 'One' put: 1
y at: 'Two' put: 2
y at: 1 put: 'One'
y at: 2 put: 'Two'
{% endhighlight %}

# 톰 러브(Tom Love) 인터뷰

## Engineering Objective-C

### 왜 새로운 언어를 만들지 않고, 기존의 언어를 확장하였나?
  * 큰 조직에서 호환성에 대한 요구가 매우 중요했기 때문
    * C 프로그램은 Objective-C 로 컴파일 가능하다. (수정해야할 것이 하나도 없다.)
  * 크고 중요한 제약사항
    * mix & match를 쉽게 해주는 제약

### 왜 C를 선택했나?
  * 아마, 우리가 연구환경으로 C로 작성된 유닉스 시스템을 사용하고 있었고, C로는 하기 어려운 것을 시도하고 있었기 때문일 것이다. (주: 스트라우스트럽은 이런 상황이 언어를 변화할 수 있는 기회라고 말했음)
  * 1981년 가을, Byte 잡지에 Smalltalk 기사가 났었다.
    * Brad "스몰토크의 대부분 기능들을 어떻게 C에 추가할 수 있을지 알겠어"
  * 우리는(러브와 콕스)는, 텔레커뮤니케이션 시스템을 만드는 소프트웨어 개발자를 돕는, 분산 프로그래밍 환경을 만드는 ITT내 리서치 그룹에 속에 있었음.
  * 요즘에 CAD 툴이라 불리는 것을 빌드하기 위한 적절한 툴을 찾는 중이었음

### 최근의 관점에서, Objective-C 가 Smalltalk보다 나은 면이 있는가?
  * 최근 Objective-C 라이브러리는 1983년과 84년 가을에 나온 첫 버전과 매우 다름
  * 언어는 각 언어에 적합한 영역이 있음
  * Smalltalk는 OOP를 배우기에 매우 좋은 언어. 학계에서 OOP를 Smalltalk 으로 배우지 않는 것이 이상함
  * 내가 OS를 만들어야 한다면, Smalltalk을 선택하지 않을 것이다.
    * 반면에, 연구모델 혹은 프로토타입 같은 어떤 것을 만들어야 한다면, Smalltalk은 아름다운 솔루션이다.

### Objective-C 와 C++ 모두 C에서 시작했지만, 다른 방향으로 발전했다. 지금 보기에 어떤 접근이 더 좋은가?
  * 한 가지 경우는, 매우 작고 간단한 (감히 말하기에 우아한) 프로그래밍 언어로 매우 또렷하고 잘 정의된 접근이었고
  * 다른 경우는 아름답지못하고(ugly), 복잡하고, 어려운 언어로 어떤 면에선 매우 까다로운 기능을 갖게하는 접근이었다.

### C++은 매우 복잡한 면이 있는가?
  * Oh, absolutely.

### C++이 Objective-C 보다 많이 쓰이는 이유가 뭐라고 생각하는가?
  * AT&T 이름 때문에

### 단지, 그 이유때문인가?
  * 그렇게 생각한다.

### 오늘날 Objective-C 에 대해선 어떻게 생각하는가?
* It still exists. How about that?

### Objective-C 2.0에는 흥미로운 기능을 추가된다. - 애플이 계속 살려놓음.
* 어제 밤에, 아이폰용 개발하는 누군가랑 이야기했음
* 아이폰 용 개발킷 다운로드 받았는데, 그건 완전히 Objective-C라고 했음. 그렇게 계속 살아있음

## Growing a Language

### 당시에, Smalltalk를 선택한건 최선인 것 같다. 지금에도 좋은 선택인가?
* Smalltalk 는 우아한 언어
* Objective-c 는 하이브리드 언어에 대한 아이디어로 시작
  * C에서 어떠한 것도 제거하지 않았음
  * C 파생언어가 아닌, C에 기반한 하이브리드 언어를 만들었음
* Objective-c 에서 대괄호 "[]"는 메세지 전달 표현
* 처음 아이디어는, 라이브러리나 클래스 세트를 만든 이 후엔, 대괄호 안에서 대부분의 작업을 하는 것
* 절차적 언어와 객체지향 언어의 하이브리드

### C에서 시작해서 Smalltalk를 추가하게 된 동기가 있나?
* 전화 교환기 시스템을 만드는 국제적이고 커다란 팀을 위한 프로그래밍 환경을 만들때 사용하기 위한 "옳은(right)"언어를 알아내려 노력
* 81년 가을 Byte 지에 Smalltalk가 소개. 우리는 해당 내용을 여러 번 정독.
  * Brad가 하루는 내 사무실로 찾아와, 컴퓨터를 1주일만 집에 가져가겠다고
  * "일주일이면, C 확장기능으로 Smalltalk에 가까운 것을 만들어 올수 있을 것 같다.""

### 일주일 작업은 아닌것 같아보이는데, 컴파일러 자체는 복잡하지 않은가.
  * 복잡하지 않다.
  * 기반이 깔끔한 언어는 복잡하지 않다.
  * C++ 같은 것 상상하지 말아라.

## Project Management and Legacy Software

### (기존 코드 재작성)
  * 초기에 큰 C 프로그램을 Objective-C 로 재작성하는 경우에 대한 많은 분석
    * 결과는 1/5로 줄었음

### 좋은 압축률이다.
  * 4년 전에 프로젝트는 1100만 라인의 COBOL + C++ 코드를 50만 라인의 자바로 바꾸는 프로젝트였음

# 브래드 콕스(Brad Cox) 인터뷰

## Objective-C and Other Languages

### 왜 새로운 언어를 만들지 않고, 기존 언어를 확장했나?
  * C에 만족하였지만, 한계가
    * OOP를 하기위해 기반언어를 다시 발명하는 것은 시간낭비

### 왜 C를 선택했는가?
  * 당시에, 우리가 가진 것이 그것이라서
    * Ada, Pascal, COBOL, FORTRAN, Chill. (이런 것들 중, C가 아니면, 어떤 언어로 시작하면 적당했을까?)
  * 우리의 목표는, OOP를 실험실에서 실환경(factory floor)로 이동시키는 것이었다. C만이 유일하게 믿을만한 옵션

### C++을 처음 봤을 때 무슨 생각을 했나?
  * Objective-C가 유명해지기 전에 스트라우스트럽과 벨렙에서 함께 이야기를 나눴음
    * 스트라우스트럽은 스태틱 바인딩에 초점을 두고 C를 업그레이드
    * 나는 다이나믹 바인딩을 추가하는데 초점

### 두 언어가 사람들에게 사용되는 정도가 다른것을 어떻게 설명할 수 있을까?
  * Objecitve-C는, 컴파일러와 관련 라이브러리외의 수입이 없는 작은 회사의 초기 제품
  * AT&T는 수익 보단 다른 이유 때문에 C++를 만들었고, C++를 퍼트릴 여유가 있었음

### 애플이 발표한, Objective-C 2.0 프로젝트에 포함이 되었나?
  * 내가 그들의 제품을 좋아하는 것 말고는 애플과 관계가 없음

### garbage collectors에 대한 의견은?
  * 좋다. 하지만,
  * 큰 성능 희생없이, 혹은 작은 노력으로 C에 넣을 수 있는 기능으로 생각하는 장사꾼들과 싸워야만 했음

### Objective-C 에서 다중 상속을 금지한 이유는?
  * 역사적인 이유가 있는데, Objective-C가 상속을 지원하지 않는 Smalltalk를 계승했기 때문
  * 오늘 다시 결정한다면, 단일 상속도 없앨 것임
  * OOP에서 중요한 것은 상속이 아니라 캡슐화  

### 왜 Objective-C가 namespace를 지원하지 않는가?
  * 당시 나의 목표는 Smalltalk를 복사하는 것이었고, Smalltalk에 namespace가 없었기 때문이다.
  * 오늘날, 당신이 Objective-C를 애플의 제품으로 아는 것과 같이, 나도 그러함
  * 최근 내 작업은 XML과 자바이다.

### protocols 의 개념이 Objective-C의 유일한 것인가?
  * I wish I could take credit for that.
  * 프로토콜 아이디어는 Objective-C 백본 위에 추가한 것 중 하나
  * 당시, Smalltalk 에 없던 기능이었으나, Steve Naroff 가 smalltalk에 추가
    * Steve Naroff는 애플에서 Objective-C 담당(주: NeXT부터 계속 근무)

### 자바가 당신의 디자인에 영향을 받은 것으로 보인다. 자바도 단일상속을 지원한다. 자바에서도 단일 상속을 제거하는 것이 좋겠나?
  * 아마도
  * 다른 기능들 처럼, 단일 상속은 오용의 가능성이 있으며, 캡슐화 만큼 중요하지는 않음

# 참고자료
  * <Masterminds of Programming> http://shop.oreilly.com/product/9780596515171.do
  * http://en.wikipedia.org/wiki/Smalltalk

