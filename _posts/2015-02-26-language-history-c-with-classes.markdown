---
layout: post
title:  프로그래밍 언어의 역사 - C with Classes
date:    2015/02/26 10:00
categories: programming
---


# 비야네 스트라우스트럽(Bjarne Stroustrup)
  * 꿈의 언어를 Algol68에 Simula의 class를 더한 언어로 생각
  * 1975년 런던에서 C를 처음 접하고, 시스템 프로그래밍 언어, 기계 지향 언어, 저수준 언어로서 존경함
    * C를 접하고 C + Simula로 생각을 바꿈
  * 벨에 직장을 구하여, TCPL을 읽으며 C를 다시 배움
  * C 전문가는 아니었으나, 가장 현대적이고 현격한 시스템 프로그래밍 언어라고 인식
  * C 언어를 완전히 이해한 다음, 다음 사람들과 토의를 함: Stu Feldman, Steve Johnson, Brian Kernighan, Dennis Ritchie
    * Stu Feldman
        * Make 개발
        * ACM Software System Award 2003
    * Steve Johnson
        * yacc, lint, spell, Potable C Compiler 개발

## 참고: 역대 ACM Software System Award 수상자와 내용
  * 2012 - **LLVM**: Vikram S. Adve, Evan Cheng and Chris Lattner
  * 2011 - Eclipse: John Wiegand, Dave Thomson, Gregory Adams, Philippe Mulet, Julian Jones, John Duimovich, Kevin Haaland, Stephen Northover, and Erich Gamma
  * 2010 – GroupLens Collaborative Filtering Recommender Systems: Peter Bergstrom, Lee R Gordon, Jonathan L Herlocker, Neophytos Iacovou, Joseph A Konstan, Shyong (Tony) K. Lam, David Maltz, Sean McNee, Bradley N Miller, Paul J Resnick, John T Riedl, Mitesh Suchak
  * 2009 - VMware Workstation for Linux 1.0: Edouard Bugnion, Scott Devine, Mendel Rosenblum, Jeremy Sugerman, Edward Y. Wang
  * 2008 - Gamma Parallel Database System: David DeWitt, Robert Gerber, Murali Krishna, Donovan Schneider, Shahram Ghandeharizadeh, Goetz Graefe, Michael Heytens, Hui-I Hsiao, Jeffrey Naughton, Anoop Sharma
  * 2007 - Statemate: David Harel, Hagi Lachover, Amnon Naamad, Amir Pnueli, Michal Politi, Rivi Sherman, Mark Trakhtenbrot, Aron Trauring
  * 2006 - Eiffel: Bertrand Meyer
  * 2005 - The Boyer-Moore Theorem Prover: Robert S. Boyer, Matt Kaufmann, J Strother Moore
  * 2004 - Secure Network Programming: Raghuram Bindignavle, Simon S. Lam, Shaowen Su, Thomas Y. C. Woo
  * 2003 - **make**: Stuart Feldman
  * 2002 - **Java**: James Gosling
  * 2001 - SPIN model checker: Gerard Holzmann
  * 1999 - The Apache Group: Brian Behlendorf, Roy Fielding, Rob Hartill, David Robinson, Cliff Skolnick, Randy Terbush, Robert S. Thau, Andrew Wilson
  * 1998 - S: John Chambers
  * 1997 - Tcl/Tk: John Ousterhout
  * 1995 - **NCSA Mosaic**: Marc Andreessen, Eric Bina
  * 1995 - **World Wide Web**: Tim Berners-Lee, Robert Cailliau
  * 1994 - Remote Procedure Call: Andrew Birrell, Bruce Nelson
  * 1993 - **Sketchpad**: Ivan Sutherland
  * 1992 - Interlisp: Daniel Bobrow, Richard R. Burton, L. Peter Deutsch, Ronald Kaplan, Larry Masinter, Warren Teitelman
  * 1991 - **TCP/IP**: Vinton G. Cerf, Robert E. Kahn
  * 1990 - **NLS**: Douglas C. Engelbart, William English, Jeff Rulifson
  * 1989 - **PostScript**: Douglas K. Brotz, Charles M. Geschke, William H. Paxton, Edward A. Taft, John E. Warnock
  * 1988 - **INGRES**: Gerald Held, Michael Stonebraker, Eugene Wong
  * 1988 - System R: Donald Chamberlin, Jim Gray, Raymond Lorie, Gianfranco Putzolu, Patricia Selinger, Irving Traiger
  * 1987 - **Smalltalk**: Adele Goldberg, Daniel Henry Holmes Ingalls, Jr., Alan C. Kay
  * 1986 - **TeX**: Donald E. Knuth
  * 1985 - **VisiCalc**: Dan Bricklin, Bob Frankston
  * 1984 - Xerox Alto: Butler W. Lampson, Robert Taylor, Charles P. Thacker
  * 1983 - **UNIX**: Dennis Ritchie, Ken Thompson

## 영국에서 공부하던 시절

### 1979년 Simula를 이용하여 시뮬레이터를 개발

언어의 컨셉이 문제 해결에 도움을 주는 것에 감명 받음

  * class 컨셉 응용 프로그램의 컨셉을 프로그래밍 언어의 구조에 직접적으로 매핑하도록 도움을 줬음

그덕에 다른 어떤 언어보다 더 읽기 좋은 코드를 생산

  * 코루틴(co-routine)을 이용하여 응용 프로그램의 동시성도 쉽게 표현
  * class 계층(상속)을 이용하여 다양한 변형을 표현

### Simula의 타입 시스템에 감동

타입 오류는 둘 중의 하나.

 * 단순한 프로그래밍 실수
 * 디자인의 문제(conceptual flaw in the design)

후자가 굉장히 중요. Pascal의 경직된 타입 시스템과 Simula 유연함의 차이, 이것이 C++ 개발의 본질이었음 (The contrast 
  I perceived 
    between 
      the rigidity of Pascal and 
      the flexibiltiy of Simula 
was essential 
  for the development of C++)

Simula를 쓰면서 프로그램의 크기가 커질수록 유용함을 느껴 감동

### 언어는 좋았으나, implementation은 다른 이야기

  * 분리컴파일한 클래스의 링크 시간은 최악
    * 1/30의 프로그램을 미리 컴파일한 나머지와 링크하는 시간이 전체를 통으로 컴파일/링크하는 시간보다 오래 걸렸음
  * 실행시간 성능도 최악

이런 문제는 Simula의 근간에 있었고, 해결책이 없었음

  * 실행시간 타입 체킹, 변수 초기화 보장, 동시성 지원, 가비지 컬렉션
    * 한번 재봤더니 실행시간의 80%를 가비지 컬렉션으로 낭비

시뮬레이터는 리소스 관리를 직접 하고 있어 가비지가 생기지 않는데도

프로젝트가 망하게 생겨 급히 BCPL로 재작성

  * The experience of coding and debugging the simulator in BCPL
was HORRIBLE.
  * Simula에 비해 언어 기능은 부족했으나, 실행 속도는 빨랐음

**"알맞지 않는 도구로 문제를 해결하려고 덤비지 않으리라!!!"**

### 적당한 도구
  * Simula의 기능을 지원할 것: class, concurrency, class에 기반한 강한 타입 체킹
  * BCPL만큼 빠를 것: 분리 컴파일한 것들을 쉽게 결합, 한 언어의 근본적인 문제에 붙잡히지 않기 위해 간단한 링크 컨벤션(C, Algol68, Fortran, BCPL, 어셈블러 ...)
  * 포팅 가능한 구현: 호스트 시스템과 언어간에 굉장히 제한적인 통합

# 탄생

시작의 계기(April 1979)는

  * an attempt 
    to analyze the UNIX kernel 
    to determine how it could be distributed over a network of computers 
    connected by a local area network

두 개의 문제점이 대두

  * how to analyze the network traffic that woudld result from the kernel distribution
  * how to modularize the kernel

다음 두 가지를 표현할 방법이 필요

  * the module structure of a complex system
  * the communication pattern of the modules

**"알맞지 않는 도구로 문제를 해결하려고 덤비지 않으리라!!!"**라고 했었음!

그래서, **"툴부터 만들자!"** 그리고 앞의 두 가지는 스트라우스트럽의 주 전공이자 주 관심

1979년 10월에 Cpre라는 전처리기를 돌리고 있었고, 1980년 3월까지 전처리기를 다음어 갔음. 하나의 실 프로젝트에 적용해봤고, 몇 개의 실험적인 곳에도 적용(총 16개의 프로젝트에 적용) 이것이 "C with Classes"가 됨

특히 1979년 4월에서 10월에 '도구'가 아니라 '언어'로 사고의 전환을 하게 됨

당시에 C 확장 모듈이나 라이브러리 등이 있었으나, 그것들과 차이가 되는 점은
어떤 특정 응용 분야를 위한 기능을 추가한 것이 아니라 
범용적으로 쓸 수 있는 기능을 추가했다는 것

언어가 발전함에 따라, 특별한 응용 프로그램을 위한 기능을 제공하느냐, 일반적인 추상화 기법을 제공하느냐라는 질문은 계속해서 나왔음

이때마다 **추상화 매커니즘을 개선하는 방향으로 결정**해왔음

그래서 C++ '언어'에는 내장 복소수, 문자열, 매트릭스, 동시성에 대한 직접적인 지원, 퍼시스턴스, 분산 컴퓨팅, 패턴 매칭, 파일시스템 다루기 등이 없는 것임. 라이브러리 형태로 존재

C++는 프로그램의 구조를 개선하기 위해 시작한 것. 'computation'은 C가 해결했음.

C에 견줘 런타임 오버헤드 없이 프로그램 구조를 바꿀 수 없다는 것에 의구심을 가졌음

런타임, code compactness, data compactness를 C 수준으로 맞추는 것이 목표
housekeeping information 같은 것은 없음. 16비트 구조체 2개를 선언하면 32비트 레지스터에 쏙 들어감

테스트해보니 3% 정도 런타임 효율성이 떨어졌음. 바로 오버헤드를 제거

C with Classes 사용자들이 static type checking을 강화하기 원함
런타임에 체크하는 방법을 쓸 수 있으나, 그건 디버깅 환경에서나 용납가능
결과적으로 구현하지 못했음

# 기능

## Classes

C with Classes의 가장 중요한 관점은 class 컨셉!

{% highlight cpp %}
class stack {
    char s[SIZE];
    char* min;
    char* top;
    char* max;
    void new();
  public:
    void push(Char);
    char pop();
};

char stack.pop()
{
  if (top <= min) error("stack underflow");
  return *(--top);
}

void stack.push()
{
  if (top>max) error("stack overflow");
  *top++ = c;
}

class stack s1, s2;           /* two stack variables */
class stack * p1 = &s2;       /* p1 points to s2 */
class stack * p2 = new stack; /* p2 points to stack object allocated on free store */

s1.push('h');   /* use object directly */
p1->push('s');  /* use object through pointer */
{% endhighlight %}

### 디자인 결정사항들
  * Simula를 쫒음
    * 프로그래머가 타입을 명시하게 함
    * 'type'이 아니라 'class'라는 키워드 사용
        * 새로운 용어 만드는 것을 좋아하지 않음
        * Simula 스타일이 대부분의 경우 잘 맞았음
  * 사용자 정의 타입 객체의 표현은 클래스 선언의 일부분
    * true local variables of a user-defined type can be implemented without the use of free store or garbage collection
    * a function must be recompiled if the representation of an object is uses directly is changed
  * 컴파타일 시 접근 제어는 표현에 대한 접근을 제어하기 위해 사용
    * 클래스 선언에 있는 함수는 클래스 멤버를 사용 가능
    * public 멤버 함수는 다른 코드에서 사용 가능
  * 함수를 선언할 때, 리턴 값과 인자를 모두 명시
    * C와 다름
        * 보다 엄격한 타입 체크
  * 함수 정의를 어디서나 할 수 있음
    * lexical 메카니즘 문제가 아니라, 클래스를 인터페이스 스펙처럼 보이게 하려고
    * 소스 코드 구조와 관련된 관점
    * 멤버 함수를 분리 컴파일 할 수 있음
    * C의 링커 기술을 C++에서도 사용 가능
  * new()는 생성자
    * 객체를 처음 사용하기 전에 반드시 호출됨
  * 포인터와 비포인터 모두 사용 가능
  * 메모리 할당
    * C처럼 stack, static, heap 모두 생성 가능

## 런타임 효율성
Simula에서 class 타입은 지역, 전역 변수를 가질 수 없었음
모든 객체는 new 연산자를 통해 heap에 할당됨
이것이 비효율성의 원인
Simula로 코딩할 때, 이런 특징이 코딩 스타일을 나쁘게 만드는다는 생각을 했음

이 아유 하나만으로도 class 타입이 지역, 전역 변수가 될 수 있도록 했음
게다가 또한 빌트인과 사용자 정의 타입의 생성과 스코프에 다른 규칙을 두는 것은 우아하지 않음

C++ 디자인의 중요 원칙으로 자리 잡음: 사용자가 정의했던 빌트인이건 언어의 규칙에 있어 똑같아야 하고, 언어나 관련 도구의 지원 정도도 똑같아야 함

inline은 선언부의 몸체에 구현을 적어서 표현

{% highlight cpp %}
class stack {
  /* ... */
  char pop() 
  {
    if (top <= min) error("stack underflow");
    return *--top;
  }
};
{% endhighlight %}

## 링키지 모델(Linkage Model)

### 중요 결정사항들

  * 분리 컴파일은 기존의 C/Fortran UNIX/DOS 스타일 링커와 가능해야함
  * 링키지는 타입 세이프 해야함
  * 링키지는 다른 어떤 형태의 데이터베이스를 필요로 하면 안 됨
    * 구현을 향상시키기 위해 사용할 수는 있음
  * C, 포트란, 어셈블러 등 다른 언어로 작성한 프로그램 조각의 링키지가 쉽고 효율적이어야 함

### 이름 동등(name equivalence)을 채택

다음의 A와 B는 다른 타입

{% highlight cpp %}
struct A { int x, y; };
struct B { int x, y; };
{% endhighlight %}

다른 파일에 똑같은 이름으로 정의를 할 경우, 중복 정의 에러 발생

{% highlight cpp %}
struct C { int x, y; }; // in file 2
struct C { int x, y; }; // in file 3
{% endhighlight %}

이름 동등이 아니라 구조 동등을 채택했다면 중복 정의 에러가 발생하지 않음
그럴 경우, 현실에서 매우 힘든 일이 발생

이런 경우가 흔하지 않는데, 아마도 복사하면서 발생
또한 복사한 다음 양쪽이 동일하게 유지되는 경우는 흔치 않음
프로그램이 이상하게 동작하는 경우가 발생할 것임

구조가 동등할 경우, 실용적인 이유로 명시적 형변환을 허용

{% highlight cpp %}
extern f(struct A*);

void g(struct A* pa, struct B* pb)
{
  f(pa);  /* fine */
  f(pb);  /* error; A* expected */

  pa = pb;    /* error; A* expected */
  pa = (struct A*)pb;   /* ok; explicit conversion */

  pb->x = 1;
  if (pa->x != pb->x) error("bad implementation");
}
{% endhighlight %}

  *  자동 생성된 C 코드

{% highlight cpp %} 
class stack {
    char s[SIZE];
    char* min;
    char* top;
    char* max;
    void new();
  public:
    void push(Char);
    char pop();
};

void stack.push()
{
  if (top>max) error("stack overflow");
  *top++ = c;
}

void g(class stack* p)
{
  p->push('c');
}
{% endhighlight %}

{% highlight cpp %}
struct stack {
    char s[SIZE];
    char* min;
    char* top;
    char* max;
};

void stack_push(this, c)
struct stack* this;
char c
{
  if ((this->top)>(this->max)) error("stack overflow");
  *(this->top)++ = c;
}

void g(p) 
struct stack* p;
{
  stack__push(p, 'c');
}
{% endhighlight %}

  * this라는 포인터
    * 레퍼런스가 아니고 왜 포인터냐?
        * 초기 C with Classes에 레퍼런스가 없었음 ^^
    * self가 아니고 왜 this냐?
        * Smalltalk(self)가 아니라 Simula(THIS)에서 가져온 용어

# 정적 타입 체킹

C 코드와의 호환성 때문에, 

  * 선언하지 않은 함수의 호출을 허용했고
  * 그런 선언하지 않은 함수는 타입 체킹을 하지 않았음

타입 체킹에 큰 구멍

C with Classes로 C를 배운 사람들이 수동 타입 체킹 능력이 떨어지고, "이런 에러는 C with Classes를 쓰면 발생하지 않아!" 이런 불평을

autoprototyping: 첫 호출은 체크를 못하지만, 같은 호출이 두 번 이상 나오면 일관성 있는 타입인지 체크 (Walter Bright)

# 참고자료
  * http://en.wikipedia.org/wiki/Brian_Randell
  * 'Adding classes to the C language: An exercise in language evolution' http://onlinelibrary.wiley.com/doi/10.1002/spe.4380130205/abstract
  * http://www.techworld.com.au/article/252319/a-z_programming_languages_yacc/
  * http://en.wikipedia.org/wiki/Stu_Feldman
  * http://en.wikipedia.org/wiki/Software_System_Award
  * http://en.wikipedia.org/wiki/Stephen_C._Johnson
  * http://en.wikipedia.org/wiki/CAP_computer
  * http://homes.cs.washington.edu/~levy/capabook/
  * http://homes.cs.washington.edu/~levy/capabook/Chapter5.pdf
