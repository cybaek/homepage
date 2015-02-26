---
layout: post
title:  프로그래밍 언어의 역사 - C++
date:    2015/02/26 21:00
categories: programming
---

# 언어의 사상

## 철학
  * 프로그래밍 언어란 두 가지 상관된 목적을 만족해야함
    * 프로그래머가 시스템의 동작의 실행을 지정할 수 있는 수단을 제공 --> 기계 친화적인 언어 -->  C
    * 어떻게 해야 동작하는지를 고민하는 프로그래머가 쓸 수 있는 개념의 집합을 제공 --> 문제 친화적인 언어 --> C++
  * Many C++ design decisions have their roots in my dislike for forcing people to do things in some particular way
  * My preference is to slowly - often painfully slowly - persuade people to try new techiques and adapt the ones that suit their needs and tastes.

## Aim
  * C++ makes programming more enjoyable for serious programmers
  * C++ is a general purpose programming language that
    * is a better C
    * supports data abstraction
    * suppprts object-oriented programming

### 서문 <The C++ Programming Language, 4th Edition>
> "C++ feels like a new language. That is, I can express my ideas more clearly, more simply, and more directly in C++11 than I could in C++98. Furthermore, the resulting programs are *better checked by the compiler and run faster."

## General Rules
  * C++'s evolution must be driven by real problems.
    * 실제 프로젝트에서 C++이 무엇이 부족한지 보여주는 것이 언어 변화를 위한 좋은 동기 부여 방식
  * Don't get involved in a sterile quest for perfection.
    * 언어 다듬는데 수년 보내다가 언어 설계자는 실질적인 피드백을 얻지 못함
        * 그렇게 해서 나온 것은 현실과 동떨어짐
        * 스펙은 한 번 나오면 바꾸기 어려움
    * 언어가 성숙함에 따라 언어 자체의 변화보다는 도구나 라이브러리에 의존한 대안을 찾는 경향이 있음
  * C++ must be useful 'now'.
    * 언어 사용자들의 환경(오래된 운영체제, 저사양 하드웨어, 기술 역량, 교육 등)은 최첨단이 아님
    * 이런 사용자들을 고려해야함
    * 시간과 C++ 성공 결과를 가지고 변화 추구
  * Every feature must have a reasonably obvious implementation.
    * 명백한 분석과 코드 생성 전략이 있어야 하고, 실제로 사용하기에도 알맞아야 함
    * 구현의 복잡성과 사용의 복잡성에서 늘 구현의 복잡성을 택함
        * 컴파일러 개발자보다 C++ 사용자가 더 많음
  * Always provide a transition path.
    * 더 좋은 대안을 제시하고
    * 예전의 안 좋은 것을 쓰지 말 것을 권고(컴파일러 경고)
    * 이후 예전 방법
    * 수 년이 흐른 뒤, 문제의 기능 제거
        * C 호환 때문에 제거하지 못하는 기능이 있지만, 컴파일러 경고로 대신
  * C++ is a language, not a complete system.
    * C++은 통합 시스템이 아니라, 컴파일러, 링커, 런타임 라이브러리, IO 라이브러리, 편집기, 파일시스템, 디비 등등 각각 유지 관리
      * 포팅이 쉽고
      * 서로 다른 언어로 작성한 코드간 협업이 쉬움
      * 도구를 공유할 수 있고
  * Provide comprehensive support for each supported style.
  * Don't try to force people.

## Design Support Rules
  * Support sound design notions. 논리적으로 옳은 디자인 사상을 
    * C가 어셈블리를 대체한 것처럼, 시스템 프로그래밍에서 추상화 레벨을 높이는 것이 목표
        * 언어의 새로운 기능을 추가할 때, 설계 표현을 향상시킬 수 있는 것인지 고려
            * 클래스로 표현한 개념을 효율적으로
    * 지원하는 언어 스타일에 따라 제안 받은 언어 기능을 추가하기도 하고 탈락시키기도 하고
        * 모든 스타일을 지원하는 언어도 없지만, 한 가지 스타일만 지원하면 적응력 떨어져 결국 실패
  * Provide facilities for program organization.
    * 계산 속도 문제는 이미 C가 해결
    * 표현력 향상에 관심
  * Say what you mean.
    * 저수준 언어의 문제점: 개발자들이 대화할 때 표현하는 것과 실제로 코딩할 때 표현이 다른 점
    * 언어를 보다 선언적으로 만들면 이 간극을 좀힐 수 있음
        * 선언적(declarative) 프로그래밍: 제어 흐름없이 계산 방식을 기술하는 방법
           * HTML의 &lt;emp> 태그, SQL
  * All features must be affordable.
    * 기능 추가는 굉장히 비용이 낮은 다른 방법이 없을 때
    * 우아함과 효율성 둘 다 얻으면 좋겠지만, 선택해야한다면 효율성
  * It is more important to allow a useful feature than to prevent every misuse.
    * 잘못된 사용을 막은 예
        * 모든 인자 타입 체킹
        * 클래스 기본 접근제어는 private
    * 마음먹고 시스템을 깨는 개발자는 막을 수 없음
    * 오래된 C 슬로건 "trust the programmer"
    * 타입 체킹이나 접근제어도 의도된 공격을 막으려고 한 것이 아님
      * to allow class privider 
          * to state clearly what is expected from users
          * to protect against accidents
  * Support composition of software from separately developed part.

## Language-Technical Rules
How things are expressed in C++

  * No implicit violations of the static type system.
    * 모든 객체는 특정 타임으로 생성
    * 객체를 선언한 타입이 아닌 다른 타입으로 사용하면 타입위반
    * 이런 타입 위반이 발생하지 않는 언어를 'strongly typed'
    * 이런 타입 위반을 컴파일 시점에 알 수 있는 언어는 'strongly statically typed'
    * C의 유니온, 캐스트, 배열 때문에 모든 타입위반을 컴파일 시에 알 수 없음: 컴파일러 워닝
    * 이런 문제의 대안으로 클래스 상속, 표준 배열 템플릿, 타입안전 링키지, 동적 체크 캐스트를 제공
    * RTTI와 예외처리 기능이 런타임 시에 컴파일러나 링커가 잡지 못한 에러를 핸들링하도록 도와줌
  * Provide as good support for user-defined types as for built-in types.
    * UDT라고 제약 받는 것이 없음
  * Localilty is good.
    * class는 코드를 지역화하고, 잘 정의한 인터페이스를 거쳐 접근할 수 있는 채널을 제공
  * Avoid order dependencies.
  * If in doubt, pick the variant of a feature that is easiest to teach.
  * Syntax matters(often perverse ways).
  * Preprocessor usage should be eliminated.
    * 구분용 상수를 정의하는데는 const, enum
    * 함수 호출 오버헤드를 피하려면 inline
    * 함수와 타입의 일반화 형태를 만들고 싶다면 template
    * 이름 충돌을 막고 싶다면 namespace



# 역사

## 1979~1981년
  * Simula의 OOP가 유용하다고 생각했으나, 실제로 사용하기에 너무 느렸음
  * "C with Classes"를 개발
    * C는 그때도 지금도 속도나 저수준 기능의 희생없이 포팅하기 좋은 언어로 인식
    * 지원하는 기능
      * 1980
        * classes
        * basic inheritance
        * public/private access control
        * constructors and destructors
        * call and return functions(나중에 없어짐)
        * 'friend' class
        * type checking and conversion of function arguments
      * 1981
        * inlining
        * default function arguments
        * overloading of the assignment operator
    * 초기에 C with Classes의 컴파일러를 "Cfront"라고 불렀음
      * Cpre라는 C 컴파일러 이름에서 따온 것
      * C with Classes 코드를 오리지날 C코드로 바꾸는 전처리기
      * "Cfront" 코드의 상당 부분을 C with Classes로 작성
      * self-hosting compiler: a compiler that can compile itself
        * C with Classes 소스 코드를 C with Classes로 컴파일
      * 새로운 추가 기능(exceptions)을 통합하기 어려워 1993년에 사라짐

## 1983년
  * C with Classes에서 C++로 이름을 바꿈
    * ++ 연산자: 스트라우스터럽에 영감을 줌
  * 추가한 기능
    * virtual functions
    * function overloading
    * references with the & symbol
    * the const keyword
    * single-line comments

## 1985년
  * <The C++ Programming Language> 출판
  * 아직 표준화가 되지는 않았음

## 1989년
  * 추가한 기능
    * protected and static members
    * inheritance from several classes

## 1990년
  * <The Annotated C++ Reference Manual> 출판
  * Borland's Turbo C++ 판매

## 1998년
  * 최초의 C++ 표준: ISO/IEC 14882:1998(776쪽)
    <The Annotated C++ Reference Manual>에서 큰 영향을 받음
    * 흔히 C++98이라고 부름
    * STL 포함

## 2003년
  * C++98의 문제점들을 보완
  * 흔히 C++03이라고 부름

## 2005년
  * TR1 (Library “Technical Report 1”) published
    * 14 likely new components for the standard library
  * 이제 준하는 새로운 표준을 C++0x라고 부름
    * 하지만 2011년 중반이 되도록 표준을 릴리즈 못함
    * 몇몇 컴파일러는 C++0x 기능을 지원하기 시작

## 2011년
  * 새로운 표준이 드디어 나옴(1353쪽)
    * C++0x가 아니라 C++11이라고 부름
    * Boost 라이브러리가 많은 영향을 끼침
  * 추가한 기능
    * regular expression support 
    * a comprehensive randomization library
    * a new C++ time library, 
    * atomics support, 
    * a standard threading library 
    * a new for loop syntax providing functionality similar to foreach loops in certain other languages
    * the auto keyword
    * new container classes
    * better support for unions and array-initialization lists
    * variadic templates


# C++TR1

  * 2007년 ISO/IEC TR 19768:2007
  * 정식명칭: ISO/IEC TR 19768, C++ Library Extensions
    * http://www.iso.org/iso/iso_catalogue/catalogue_ics/catalogue_detail_ics.htm?ics1=35&ics2=60&ics3=&csnumber=43289
  * 추가 사항
    * 정규표현
    * 스마트 포인터
    * 해쉬 테이블
    * 난수 발생기
  * 문서의 목적: "to build more widespread existing practice for an expanded C++ standard library."
  * TR1은 표준이 아니라, 드래프트 문서
    * 하지만, 대부분이 C++11 표준에 포함
    * C++11 이전에 벤더들은 이 문서에 맞춰 확장
    * 거의 대부분의 기능이 Boost에 있음
  * 참고
    * http://www.boost.org/

# C++11

  * ISO가 2011년 8월 12일에 승인한 C++ 프로그래밍 언어의 최신판
    * C++0x라고도 알려짐: 2010년 이전에 정리 마치려다 11년까지 갔음, 한 때 10진수가 아니라 16진수라고 비꼬기도
  * 추가 사항
    * 표준 라이브러리의 업그레이드
    * 스레드
    * 튜플 자료형
    * 해쉬 테이블
    * 정규 표현식
    * 범용 스마트 포인터
    * 확장가능한 난수 생성기
    * wrapper 레퍼런스
    * 함수객체에 대한 다형성이 있는 wrapper
    * 메타 프로그래밍을 위한 type traits
    * 함수객체의 리턴형에 대한 방법
  * 새로운 라이브러리의 대부분은 C++ 표준 위원회의 TR1이라고 불리는 기술 보고서에서 정의되고 있으며 이는 2005년에 발표
    * TR1의 대부분은 std::tr1 네임스페이스에서 현재 이용가능
    * C++11에 맞게 그 네임스페이스를 std로 이동 예정
    * 또한 C++03에서 구현 가능했던 기능들을 C++11에 맞게 향상되겠지만 오리지날 TR1 규정의 부분은 아님
  * 이후를 위한 TR2
    * http://en.wikipedia.org/wiki/C%2B%2B_Technical_Report_1#Technical_Report_2
  * 참고
    * http://www.stroustrup.com/C++11FAQ.html
    * http://www-sop.inria.fr/geometrica/events/WG21_meeting_june_2008/public_talks.html
    * http://www.artima.com/shop/overview_of_the_new_cpp


# 스트라우스트럽 인터뷰

## Design Decisions

### 새로운 언어를 만들지 않고, 기존 언어를 확장한 이유는?

  * Simula처럼 프로그램을 구성(OOP)할 수 있고, C처럼 효율적인 로우레벨 코드를 쓸 수 있는 언어가 필요
  * 단지 몇 가지 문제를 푸는데 도움을 원하였으므로, 새로운 언어를 디자인하고 싶지 않았음
  * C를 기반으로 하지 않았더라도, 다른 언어를 기반으로 사용하였을 것

### 기반 언어가 C 인 이유

  * 주변에 데니스 리치(Dennis Ritchie), 브라이언 커닝언(Brian Kernighan)과 유닉스의 대단한 사람들이 가까이에 있었음(스트라우스트럽은 벨에서 근무)

  * C는 강타입언어지만, 약한 타입검사를 함
  * 약한 타입검사가 걱정스러웠음
  * 당시(1979)에 C는 많이 사용되는 언어가 아니었다.
  * C++이 C에 기반한 것은, C의 (강타입 부분) 계산모델에 대한 신뢰 및 동료에 대한 신뢰의 표현

  * C를 선택한 것은 당시 시스템 프로그램을 위한 고수준 언어에 대한 지식에 근거한 것(사용자와 구현자 두 가지 입장에서 모두)
  * 당시 대부분의 작업이 하드웨어와 가깝게 있었고, 어셈블러에 가까운 성능을 요구
  * C의 기본 모델위에 더 좋은 타임 체크 시스템이 있는 모델을 선택
  * 그리고, 프로그램을 위한 프레임워크로 Simula의 클래스를 원했었기 때문에, C의 메모리 & 계산 모델 위에 Simula 의 클래스를 얹었음
  * 그 결과, 엄청나게 표현력이 강하고 유연한 것이 나왔고, 거대한 런타임 시스템의 도움 없이 어셈블러의 속도에 도전

### 왜 멀티패러다임을 지원하게 하였는가?

  * 프로그래밍 스타일을 조합하는 것이 종종 최고의 코드로 이끌기 때문
  * 최고의 의미를 직접적으로 표현하면, 디자인, 빠른 실행, 유지보수성 등

#####참고

![<Essential C++>](http://ecx.images-amazon.com/images/I/51SWSEF2GFL._SX225_.jpg)
 
  * <Essential C++> 
    * http://www.amazon.com/Essential-C-Stanley-B-Lippman/dp/0201485184/
  * C++ In-Depth 시리즈 중의 한 권
    1. 시리즈 편집장: 스트라우스트럽
  * 차례
    1. C++ 프로그래밍의 기초
    2. 절차적 프로그래밍
    3. 제네릭 프로그래밍
    4. 객체 기반 프로그래밍
    5. 객체 지향 프로그래밍
    6. 템플릿 프로그래밍
    7. 예외 상황 처리

### 자바는, OOP 에 온전히 집중한다. C++이 generic programming 에서 장점을 취할 때, 자바가 OOP에 집중한 것이 자바를 더 복잡하게 만드는 면이 있는 것으로 보이는가?

자바언어 디자이너가 OO를 강조한 것이 터무니 없게 되었다.
순수함과 단순함을 주장하며 자바가 등장하였을 때, 자바가 성공하게 되면, 그 크기와 복잡성이 매우 커질것으로 예상하였고, 실제로 그렇게 되었다.
예를들면, 자바 컨테이너에서 데이타를 꺼낼때, 컨테이너가 어떤 타입의 데이타를 담고 있는지 표현할 수 없기 때문에, Object로 부터 casting 으로 변환하는 것을 표현해한다. 장황하고, 효율적이지 못하다.
이제, 자바는 generics가 있지만, 느리다. 언어의 복잡성을 증가시키는 다른 예로는 enumeration, reflection, inner class 등이 있다.


복잡성은 어딘가에서 나타나게 마련이다. 복잡성이 언어 디자인에 없다면, 수많은 라이브러리나 애플리케이션에서 나타난다.
모든 알고리즘이 클래스 내에 있어야한다는 자바의 강박 때문에, 데이타가 없이 스태틱 함수로만 이뤄진 클래스 같은 이상한 것이 생겼다.
수학에서, x.f(), x.f(y), (x,y).f() 대신에, f(x), f(x,y)를 쓰는 것은 이유가 있다.


C++은 데이타 추상화와 generic 프로그래밍 기법의 조합으로 객체 지향의 표현 문제를 논리적으로 잘 풀어낸다.
고전적인 예로 vector<T> 에서 T는 복사할 수 있는 타입이면 무엇이든 가능하다. 빌트인, 포인터, 사용자 정의 (스트링, 복소수 등) 타입들.
이 모두가 실행시점의 오버헤드 없이, 데이타 레이아웃의 제약 없이, 표준라이브러리 구성에 특별한 규칙을 두지 않고서 가능하다.
single-dispatch-hierachy OO 모델에 어울리지 않는 다른 예로는, 두 클래스에 모두 접근해야하는 operation을 들 수 있다.
예를 들면, operator*(Matrix, Vector). 각 클래스의 "method" 로는 자연스럽게 해결할 수 없다.

### 자바와 C++의 포인터 접근의 차이점은?


자바도 포인터가 있다. 자바의 포인터는 암시적이고, 레퍼런스라고 부른다.
포인터를 암시적으로 만드는 것은 장/단점이 있고, 진짜 스택 오브젝트를 만드는 것도 단점만큼의 장점이 있다.
모든 타입에 대해 "스택 로컬 변수"와 "진짜 멤버 변수"를 지원하는 것은
통일된 의미론을 지원하고,
값 의미 개념을 잘 지원하고,
compact한 메모리 레이아웃과 최소화된 접근 비용을 제공하며,
일반적인 자원관리를 위한 C++ 지원의 기초가 된다.

레이아웃 트레이드 오프를 생각해보면,
C++에서 vector&lt;complex>(10) 는 25 words.
java에서는 56 words.

레퍼런스를 어디서나 쓸 수 있게 하고 암시적으로 하는 것은, 프로그래밍 모델과 garbage collector 구현을 단순하게 하지만 메모리 오버헤드는 급증하고, 메모리 접근 비용과 메모리 할당 비용은 비례해서 증가한다.

자바는 포인터 연산등을 통해 포인터를 잘 못 사용하는 일은 없다.
잘 작성된 C++프로그램은 포인터로 인해 생기는 문제를 겪지 않을 수 있다. 포인터 연산 대신, iostream, containers, and algorithms 등 고 수준의 추상화를 이용할 수 있다.
자료구조의 직접적이고 효율적인 접근을 위해서 포인터는 중요하다.

포인터의 어두운 면은, buffer overruns, 삭제된 메모리 포인팅, 초기화 되지 않은 메모리 포인팅 등이 있다.

Scoped resource management 는 강력한 도구.


### "값 의미구조"(value semactics)와 "일반적인 자원 관리"(general resource management)는 무슨 뜻인가?

value semactics는 복사할 수 있는 것.
자바에선, 기본타입에서는 가능하지만, 사용자 정의 타입(클래스)에서는 불가능하다.
general resource management 는 object 가 리소스(e.g. file handle, lock)를 소유하는 흔한(popular) 테크닉이다.

RAII
객체 생성시에 자원을 얻고, 객체 삭제시에 자원해재를 하는 것.
모든 자원을 이렇게 관리할 수 없지만, 많은 자원들이 가능하고, 이 것은, 자원 관리를 암시적이고 효율적이게 한다.

### "하드웨어에 가깝게(close to hardware)"는 C++ 디자인의 가이드된 원리 처럼 보인다. C++가 다른 언어에 비해 더 bottom-up 디자인이라 불릴 만 한가?

top-down & bottom-up 디자인 구분은 잘 못 된 구분이라고 생각한다.
"하드웨어에 가깝게"의 의미는, 계산모델(메모리상의 객체의 순서, 고정크기 객체에 대해 정의된 연산 등)이 수학적 추상화가 아니라, 컴퓨터 하드웨어에 가깝다는 의미이다.
자바 & C++은 "하드웨어에 가깝게"가 맞다. 차이점은 machine 이 실제 기계인지 가상기계인지 부분이다.
진짜 문제는, 문제와 해결책에 대한 사람의 인식 을 제한적인 기계의 세계로 가져가는가 하는 것이다.
사람에겐 어려운 기계적인 해법으로 접근할 수도 있고, 여러 추상의 단계등을 통해 비용을 들여서, 사람이 이해하기 쉬운 형태로 해결할 수도 있다.
C++은 두 가지 형태의 접근이 모두 가능하다.

## Using the Language

### 디버깅은 어떻게 하나? C++개발자에게 제안할 것은?

디버깅을 매우 싫어하며, 디버깅을 가능한 피하려고 한다.
소프트웨어를 디자인해야한다면, 컴파일되고, 잘못동작하기가 어렵도록 인터페이스와 불변식(invariants)들을 만들것이다.
그리고, 테스트를 만들겠다.
시스템적으로 인터페이스를 테스트 할 수 있어야 한다. 테스트는 최대한 자동화 해야하며, 자주 수행하여야 한다.
리그레션 테스트를 유지하고, 자주 실행하여야 한다. 시스템의 모든 진입점과 모든 출력을 테스트해야한다.
시스템을 품질 높은 컴퍼넌트로 구성해야한다. monolithic 프로그램은 이해하기에도, 테스트하기에도 어렵다.

### 안전성에 대한 생각은?

타입 안전성을 활용하는 형태로 C++을 사용하라. pointer, array 등을 직접사용하지 말 것 (80년대 c 스타일)

### 시스템 소프트웨어나 임베디드 애플리케이션 등에, C++을 사용하기 주저하는 사람에게 C++을 추천하겠는가?

C++은 해당 영역에서 계속 사용이 안정적이고 상당히 증가하고 있다.
록히드마틴의 Joint Strike Fighter 프로그램같은 미션크리티컬 소프트웨어에서도 사용한다.
That's an all c++ plane. (주: JSF는 F-35 전폭기 개발 과제)
C++은 임베디드 영역에서 1984년 부터 사용되었고, 빠르게 증가했다.심비안, 모토롤라, 아이팟, GPS시스템이 그 예다.
C가 더 효율적이라고 생각하는 사람은 내 논문 한 번 읽어봐 "Learning Standard C++ as a New Language".
ISO C++ 표준위원회가 만든 C++의 성능에 대해 기술 문서가 있으니, 그것도 보도록. ("Technical Report on C++ Performance). 성능에 대한 많은 이슈와 미신들을 설명한다.

### 리눅스나 BDS 등의 커널은 여전히 C를 사용한다. 왜 C++로 가지 않을까? OO 와 관계된 어떤 것 때문일까?

거의 보수주의와 타성때문일것.
C 커뮤니티 일부는 수십년간의 경험에 기대어, 거의 의도적으로 무시하고 있는 것 처럼 보인다.
다른 OS, 시스템 프로그램, 하드 리얼타임 시스템, safety-critical 코드들이 C++을 수십년간 사용하고 있다.
예를 들면, 심비안, IBM OS/400, K42, BeOS, 윈도우 일부, 그리고 수많은 오픈소스 프로젝트 (eg, KDE)

그리고, 질문자가 C++과 OO 를 동일시 하는 것 같아보이는데, C++는 OOP만을 의미하지 않는다.
내가 쓴 "Why C++ is not junt an Object-Oriented Programming Languages"이 온라인에 있다.
C++은 여러 프로그래밍 스타일(혹은 패러다임, 긴 단어를 좋아한다면)과 그 스타일을 섞어 사용할 수 있다.
고성능과 "하드웨어에 가깝게"에 가장 적절한 다른 패러다임은 generic progrmming 이다.
ISO C++ standard library 자체가, 그 프래임웍과 알고리즘 부분에서, 상당량이 OO 보다 GP 이다.
추상성과 성능을 모두 필요로 할 때, generic program이 사용된다.
C++ 보다 C로 더 잘 쓸수 있는 프로그램을 본 적이 없다. 그런 프로그램이 존재할 수 없다고 생각한다.
최악의 경우, C와 비슷하게 C++를 쓸 수 있다.

### 프로그래머는 C 에서 C++로 코드를 변경해야 하는 이유는? C++을 제네릭 프로그램언어로 사용했을 때 장점은?

코드는 C 로 먼저 쓰여지고, 프로그래머는 C 부터 시작한다고 생각하나 본데…
대부분의 C++ 프로그램과 프로그래머는 그렇지 않다. ….

C에서 지원하는 것보다 C++이 지워하는 프로그래밍 스타일 중 더 좋은 것을 발견하면, C 에서 C++로 변경하겠지.
C++의 타입검사가 더 엄격하고, 타입안전성이 높은 표현의 지원이 있다.

제네릭 프로그래밍 언어로 C++을 사용한다면, 표준 컨테이너와 알고리즘을 사용할 수 있다.
Boost 등의 라이브러리를 사용하게 되면, 제네릭 프로그래밍을 상속받은 함수형 프로그래밍 테크닉을 사용할 수 있다.

질문이 약간 잘못 된 듯 하다. C++이 OO 언어 또는 GP 언어로 표현되는 것을 원치 않는다.
C++은 여러 프로그래밍 스타일을 지원하며, 여러 스타일을 조합하는 것을 지원하고, 시스템 프로그래밍의 경향성이 있다.

## OOP and Concurrency

### 프로그램의 평균 크기와 복잡성이 매년 늘어나고 있다. OOP가 이런 상황을 더 키우거나 더 복잡하게하지 않았나? 재사용 가능한 object 에 대한 요구가 프로그램을 더 복잡하게 만들고, 작업량을 늘리는 것 같은 느낌이 있다.

재사용해야하는 툴을 디자인하고, 나중에 수정을 해야하는 경우, 처음 만든 것에 의해 맞춰야할 부분이 정해지게 된다. 이 것이 솔루션의 제약(restriction)이 된다.
정적으로 타입검사를 하는 OO 상속을 이용한 프로그램 작성시 문제는, 좋은 기본 클래스 디자인 부분이다. 많은 예측과 경험이 필요한 부분이지만, 디자이너가 어떻게 다 알 수 있겠는가.
일반적으로, 디자인을 강제할 수 있는 상황에선 사람들은 후진 우회로를 찾아 대응할 것이고,
디자인을 강제하지 않는 곳에선, 본질적으론 같은 기능에 대해 호환되지 않는 인터페이스들이 나타나게 된다.

이런 상황에 대해, 일반적인 해법은 없지만, GP 는 OO가 실패한 부분에 많은 케이스에 대한 답이다.
간단한 예가 컨테이너이다. (컨테이너 원소와 컨테이너 각각에 대해 상속에 대한 개념을 표현할 수 없지만, 효율적인 해결책을 제시했다.)

### 이런 문제가 C++에 한정적인가? 아니면 다른 프로그램언어에도 있는가?

클래스 상속에 정적 타입 검사를 하는 언어(C++, Java, C#)는 모두 동일한 문제가 있다. Smalltalk, Python 같은 동적 타입체크 언어에는 그런 문제가 없다.
C++은 해당문제를 GP로 풀고 있다. 핵심 특징은 템플릿이다. 타입체크를 늦게 하는 모델로, 실행시간에 동적 타입 체크를 하는 언어가 제공하는 기능과 동일한 것을 컴파일 시점에 제공한다.
최근 C++을 따라하여, Java와 C#이 최근 추가한 "generics"가 템플릿을 개선한 것이라 종종 주장한다. (내 생각엔 맞지 않지만… )

"리팩토링"이 해당 문제를 해결하려는 시도로서 일반적(popular)이다.
초기 인터페이스 디자인을 넘어서야할 때, 단순하게 코드를 재 구성하는 brute force 테크닉.

### 이런 문제가 OO에서 일반적이라면,OO가 단점보다 장점이 많다는 것을 어떻게 확신할 수 있나? 좋은 OO 디자인을 하기가 어렵다는 것이 다른 모든 문제의 근원인 것 같다.

어떤 면에 문제가 있다는 사실이, 그 언어로 작성한 많은 아름답고, 효율적이고 유지하기 좋은 시스템이 있다는 사실을 바꾸진 못한다.
OO design 은 시스템을 디자인하는 기본적인 방법 중에 하나이고, 인터페이스를 정적으로 검사하는 것이 OO design에 이점을 제공한다.

소프트웨어 개발에 있어서, "모든 악의 근원" 같은건 없다.
디자인은 어렵다.

### OO 패러다임과 동시성(concurrency)사이에 연결(link)이 있나? 동시성(concurrency) 지원하기 위해, OO 디자인 자체 또는 디자인데 대한 구현을 바꿔야하는가?

오랜 연결이 있다. oop 를 최초로 지원한 simula67 역시 동시작업을 표현하기 위한 메커니즘을 제공하였다.
첫 번째 C++ 라이브러리가, 현재 우리가 threads 라고 부르는 것을 지원하기 위한 라이브러리였다.
1988년에 벨랩에서 우리는 6 프로세서가 있는 컴퓨터에서 C++을 사용했고, 그렇게 사용하는게 우리만은 아니었다.
90년대에는 분산 & 병렬 프로그래밍을 지원하기 위한 수십개의 실험적인 C++ 변종(dialects)과 라이브러리가 존재하였다.
현재 멀티코어에 대한 관심이, 내겐 처음 보는 일이 아니다.
사실 내, 박사학위 주제가 분산 컴퓨팅이고, 계속 그 분야를 놓지 않았다.

### C++은 동시성에 대한 준비가 있나? 라이브러리는 만들수 있겠지만, 언어와 표준 라이브러리에서 동시성에 대해 깊은 검토가 필요한 것 아닌가?

Almost. C++0x will be.
동시성을 위한 준비를 위해, 언어는
컴파일러 작성자가 최근 하드웨어의 장점을 활용할 수 있도록, 명확하게 기술된 메모리 모델이 있어야 한다.
thread-local-storage 와 atomic data type 같은 몇 가지 작은 언어 확장이 필요하다
라이브러리형태로 동시성 지원을 추가할 수 있다.
자연스럽게 첫번째 표준 라이브러리는, 시스템 타입(linux or widonws 등)에 관계없이 사용할 수 있는 threads 라이브러가 될 것이다.
그런 라이브러가 이미 있었지만, 표준 라이브러리는 아니었다.
데이타 경쟁을 피하기 위한, 락 형태와 같이 사용하는 Thread는, 직접적으로 동시성을 사용하는 가장 나쁜 방법이다.

동시성에 있어서 한 가지 주요 이유는, 동시에 진행되어야하는 작업을 어떻게 포장(package up)할 것인가 하는 것이다.
C++에선 "function object"가 그 답이 될 것이다.
C++98 은 named operations 를 잘 지원했다.
C++0x 는 람다 함수를 제공하므로, 더 간단하게 지원한다.
C++0x 이후에, 위원회는 라이브러리에 대한 기술 리포트에 대한 계획이 있다.
쓰레드 풀과 워크 스틸링 형태의 것들이 제공될 것이다.
그것은, 사용자가 직접 thread 를 생성하고, 락을 잡고 하는 것들 대신에 태스크 단위의 동시 작업을 하는 기본 메커니즘이 될 것이다.

### 현대의 많은 시스템은 컴포넌트화 되어 네트웍에 흩어져 있다. 웹 애플리션과 매쉬업등이 그런 트랜드를 강조하여 보여준다. 언어가 네트웍의 그런 면을 반영해야할까?

동시성은 여러가지 형태가 있다.
한 기계안에서 throughput 또는 반은 시간을 향상시키기 위한 것.
지리적으러 분산된 환경을 다루는 것,
좀 더 저수준의 것 (pipelining, cacheing .. )

C++0x 은 하드웨어 아키텍트와 컴파일러 작성자 사이에 "contract"를 제공하여, 프로그래머가 저수준의 상세한 사항을 몰라도 되도록, 기반 기능들 세트 및 보장을 제공할 예정이다. 코드와 프로세서를 매핑하기 위한 기본 thread 라이브러리를 제공하게 될 것이다.
이 것을 기반으로 다른 모델들 라이브러리 형태로 지원할 수 있다. (higher level concurrency model 등)
C++0x 에 표준 마샬링 방법이 들어가기를 바랐으나, 들어가지 않았다.
첫 번째 C++ 라이브러리에 가벼운 형태의 동시성 지원이 들어간 이후로, 동시성 지원을 위한 수백의 라이브리와 프레임웍이 나왔으나, 커뮤니티에서 표준으로 동의하지 않고 있다.

## Future

### C++ 2.0 이 나올까?

C++ 2.0 이 의미하는 것에 따라 다르겠지
C++의 좋은 것을 취하고, 나쁜 것을 버린 바닥부터 만드는 새로운 언어를 의미하는 거라면, 모르겠다.
C++0x 라고 이름 붙은 C++ 다음 표준에 집중하고 있다.
많은 면에서 C++0x 는 C++ 2.0 이 될 수 있다.
새로운 특징과 새로운 표준 라이브러리를 제공한다.
static_assert, constexpr, concept, auto, nullptr,

### 새로운 언어를 만들지 않은 이유는?

몇 가지 주요 질문이 떠오른다.

새로운 언어가 풀어야할 문제는 무엇?
누구를 위해 문제를 풀어야 할까?
획기적으로 새로운 무엇을 제공할 수 있나?
새로운 언어가 세상에 잘 퍼질 수 있을까?
Would designing a new language simply be a pleasant distraction from the hard work of helping people build better real-world tools and systems?

내가 만족할 만한 답을 하지 못했다.
C++ 이 완벽한언어라고 생각하는 것은 아니다.
새로운 언어는, 기존 언어보다 약간 좋거나 약간 우아한 것 이상이 되어야 한다.

# C++을 제대로 알고 싶다면...
스트라우스트럽의 머릿속으로
  
  * 언어의 발전을 이해하고, 
    * <The Design and Evolution of C++> http://www.stroustrup.com/dne.html
  * 현재 언어 스펙을 이해하고, 
    * <The C++ Programming Language, 4th> http://www.stroustrup.com/4th.html
  * 창시자가 제시하는 스타일과 기술을 익히기 
    * Bjarne Stroustrup's C++ Style and Technique FAQ: http://www.stroustrup.com/bs_faq2.html

# 참고자료
  * <The Design and Evolution of C++> http://www.stroustrup.com/dne.html
  * <The C++ Programming Language, 3th> http://www.stroustrup.com/3rd.html
  * http://ko.wikipedia.org/wiki/C%2B%2B11
  * http://cppnow.org/
  * http://www.boost.org/
  * http://www.cplusplus.com/info/history/
  * http://www.cplusplus.com/info/description/
  * http://www.techworld.com.au/article/252319/a-z_programming_languages_yacc/
  * <Masterminds of Programming> http://shop.oreilly.com/product/9780596515171.do
  * http://en.wikipedia.org/wiki/Declarative_programming
  * http://ko.wikipedia.org/wiki/%EC%84%A0%EC%96%B8%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D

