---
layout: post
title:  프로그래밍 언어의 역사 - B
date:    2015/02/23 09:00
categories: programming
---

이 글은 2013년 6월에 comtin과 함께 스터디를 위해 정리했던 내용입니다.

# 역사

  * 1960년대 벨에서 멀틱스 프로젝트를 수행
    * MIT, GE, Bell Lab 조인트 벤처에서 시작됨
  * 1969년에 벨랩은 멀틱스가 너무 늦었고, 비싸다고 생각
    * 켄 톰슨이 이끄는 그룹이 멀틱스의 대안을 진행하기 시작
    * 켄 톰슨은 사용하기 편한 컴퓨팅 환경을 만들기 원했음
    * 멀틱스의 혁신적인 부분을 통합하길 원함
        * 제어의 중심으로서 프로세스의 명시적 개념
        * 트리 형태의 파일 시스템
        * 사용자 레벨 프로그램인 커맨드 인터프리터
        * 텍스트 파일을 단순하게 표현
        * 장치에 대한 일반적인 접근
  * 멀틱스에 대한 기능구현은 미루고, 다른 언어를 만들기 시작함
    * 멀틱스 구현언어는 PL/I 이었는데, 톰슨과 리치의 취향이 아니었음
    * BCPL을 포함한 다른 언어도 사용하였으나, 어셈블러 레벨 위의 언어로 프로그램을 쓸 때 생기는, 쓰기 쉽고 명확하게 이해되는 장점을 잃은 것을 아쉬워하고 있었음
    * 그 당시에는 이식성은 관심을 크게 두지 못하였음
  * 1968년에 톰슨이 작업한 DEC PDP-7은 8K 18-bit 워드 메모리가 있었고, 쓸만한 소프트웨어는 없었음
    * 오리지널 UNIX 시스템은 PDP-7 어셈블러로 작업
    * 작업 초기에는 GE-635 머신의 GEMAP 어셈블러용 매크로 세트를 사용하여 작업
    * 포스트프로세싱으로 PDP-7 에서 읽을 수 있는 종이 테이프를 출력하는 형태
    * 위와 같이 종이테입을 생성 방법으로 유닉스 커널, 에디터, 어셈블러, 쉘, 간단한 유틸리티(cp, cat, rm 등)를 모두 작업함
    * 위의 작업이 된 이후에, PDP-7 자체에서 계속 개발가능하게 됨.
    * 톰슨이 작업한 PDP-7 어셈블러는 단순함에 있어서, DEC의 것보다 훨씬 좋음
        * 프로그램 표현식을 해석하고 바로 실행파일을 만들어 냄
        * 라이브러리, 로더, 링커가 없었음: 어셈블러가 전체 프로그램을 처리하여 바로 "고정된 이름"의 실행파일을 만들어냄.
            * 그 고정된 이름이 a.out, 어셈블러의 결과(the output of the assembler)를 의미함
            * 이 후 링커가 생기고, 다른 이름을 지정할 수 있는 방법이 생겼지만, 기본 이름으로 계속 사용 중
  * 1969년, PDP-7위에서 동작하는 첫번째 유닉스가 나온지 얼마되지 않은 때, Doug Mcllroy가 유닉스에서 동작하는 첫번째 고수준 언어 TMG를 만듦
      * TMG는 컴파일러를 작성하기 위한 언어
      * 멀틱스에서 PL/I 컴파일러를 만들때 사용하였음
  * 톰슨은 유닉스를 위해 새로운 시스템 프로그래밍 언어가 필요하다고 생각함
      * 포트란을 만들려고 시작했다가,
      * B라는 언어를 만듦
          * B는 타입없는 C
          * 좀 더 정확하게는, 8K 메모리에 맞게 줄어든 BCPL(Basic Combined Programming Language)
          * B라는 이름이 BCPL에서 줄어든 것을 나타내는 것인듯.
          * Bon 이라는 언어에서 왔다는 이론도 있음
          * Bon은 톰슨이 멀틱스에서 만들었던 언어, B와 언어상의 관계는 없음.

![켄 톰슨과 데니스 리치](http://upload.wikimedia.org/wikipedia/commons/3/36/Ken_n_dennis.jpg)  

# 샘플 B 코드

{% highlight c %}
  /* The following function will print 
  a non-negative number, n, to the base b, where 2<=b<=10,  
  This routine uses the fact that in the ASCII character set, 
  the digits 0 to 9 have sequential code values.  */

  printn(n,b) {
    extrn putchar;
    auto a;
 
    if(a=n/b) /* assignment, not test for equality */
      printn(a, b); /* recursive */
    putchar(n%b + '0');
  }
{% endhighlight %}

# 참고자료
  * HelloWorld
    * http://en.wikipedia.org/wiki/List_of_Hello_world_program_examples
    * http://c2.com/cgi/wiki?SmalltalkHelloWorld
  * http://cm.bell-labs.com/cm/cs/who/dmr/chist.html

