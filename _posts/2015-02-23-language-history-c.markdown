---
layout: post
title:  프로그래밍 언어의 역사 - C
date:    2015/02/23 09:00
categories: programming
---

이 글은 2013년 6월에 comtin과 함께 스터디를 위해 정리했던 내용입니다.

# 간단한 역사
  * 1969년에서 1973년에 AT&T 벨 연구소에서 초기 버전 개발
  * 1977년에서 1979년에 다시 한 번 큰 변화
    * B 언어에서 유래했기에 이름을 C라고 붙임
    * B는 BCPL에서 타입을 제거한 간략한 버전
  * 1978: The C Programming Language, K&R, White Book 출판
  * 1980년대 중간 표준화, ANSI X3J11 committee

# B의 문제
  * BCPL, B는 'word' 기반. 'cell'은 하드웨어의 'word'와 동일함
    * PDP-11과 B, BCPL이 잘 맞지 않는 부분이 생김
    * 문자처리 방법의 문제
        * 각 문자를 각 셀로 펼쳤다가 다시 패킹하는 형태로 작업
        * 개별 문자를 접근하고 변경하는 방법이 byte 기반 언어에서 적절한 방법이 아님
  * 오리지널 PDP-11은 부동소수점 연산을 제공하지 않고, 제작사에서는 추후 제공하기로 약속하였지만,
    * 멀틱스 BCPL과 GCOS 컴파일러에선 특별한 연산자를 정의하는 것으로 제공하였던 기능
    * 한 word의 크기가 충분히 큰 기계에서만 제공하던 기능
    	* PDP-11은 1 word가 16bit, 부동소수점 연산을 제공하기엔 크기가 작음
  * 포인터 처리에 오버헤드가 있음
    * 포인터를 word 배열의 인덱스로 정의함
    * 런타임에 컨버전이 필요하게 됨
    	* 기계가 정의하는 byte 단위 주소로 런타임시 컨버팅이 필요
  * 위와 같은 이유로, 문자에 대한 지원, 바이트 어드레싱, 부동 소수점 하드웨어을 위해 타입 체계가 필요해짐
  * 타입 안전성과 인터페이스 검사 등은 그리 중요하게 보이지 않았음
  * 위와 같은 언어 자체의 문제와, 느린 속도의 threaded-code 를 생성하는 B 컴파일러도 문제점

![데니스 리치, 켄 톰슨, PDP-11](http://cm.bell-labs.com/cm/cs/who/dmr/kd14.jpg)

##Hello, world

## BCPL
{% highlight c %}
GET "LIBHDR"

LET START() BE
$(
    WRITES("Hello, world!*N")
$)
{% endhighlight %}

## B

{% highlight c %}
main() {
    printf("Hello, world!*n");
}
{% endhighlight %}

## C

{% highlight c %}
#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Hello, world!\n");
    return 0;
}
{% endhighlight %}


# 기원
  * BCPL은 Martin Richard가 60년대 중반 MIT 방문 시절에 만듦
    * 70년대 초까지 몇 가지 흥미로운 프로젝트에서 사용됨
  * BCPL, B, C는 (모두 포트란과 Algol60으로 대표되는) 절차형 언어
    * 시스템 프로그래밍에 중점을 둔 언어
    * 작고, 간결하게 표현되며
    * 간단한 컴파일로 작업이 쉬운,
    * 전통적인 OS에서 제공하는 구체적인 데이타 타입과 오퍼레이션에 기반한 "하드웨어에 가까운" 추상을 제공.
    * I/O와 기타 다른, OS와 인터액션에 라이브러리를 사용함
    * 코루틴이나, 클로져 같은 흥미로운 제어를 라이브러리를 통해 할 수 있음
    * 여러 기계 사이에 포팅이 가능한 정도로 충분한 추상성을 제공하고 있었음
  * BCPL, B, C는 상세하게는 문법적으로 많은 부분에서 다르지만, 대체로 비슷하다고 할 수 있음
    * 프로그램은 전역 선언과 함수 선언으로 구성됨
    * BCPL에서 프로시져는 중첩될 수 있지만, 내부 프로시져에서 스태틱이 아닌 객체는 사용할수 없었음
    * B, C는 프로시져 중첩을 허용하지 않았음
    * 초기 버전 B를 제외하고, 모두 분할 컴파일이 가능
  * BCPL의 syntactic & lexical 매커니즘은 B & C 보다 더 우아하고 규칙적임 (elegant & regular)
    * BCPL의 프로시져와 데이터 선언은 더 똑같은 구성이었음
    * BCPL에서 제공하는 loop 구조가 더 완결성이 있는 세트였음
    * BCPL에서는 라인 끝의 statement마지막의 세미콜론(;)을 생략할 수 있었음
    * B & C 에서는 이런 편의를 제거
    * 이런 몇 가지 차이점에도, 대부분의 BCPL은 B와 C로 바로 변환 가능
  * BCPL과 B의 문법 차이는, 메모리 제한 때문이기도 함
    * BCPL은 컴파일시에 프로그램 전체를 메모리에 올렸다가, 결과를 출력
    * 메모리 제약으로 B는 1 패스를 선택, 읽어서 바로 결과로 출력
  * B에서는 BCPL의 불편한 부분을 의도적으로 피하는 디자인을 했음
    * 각각 별도로 컴파일된 프로그램 사이 통신을 위해, BCPL의 'global vector' 메커니즘을 사용하였음
    	* 프로그래머가 각 프로그램이 외부에서 보여야하는 데이터와 프로시저의 이름을 vector의 offset을 지정하여 연결하게 하는 형태
  * 초기 B언어에서는 프로그램을 각각 빌드할 수 없게 함
    * 이후 B & C에는 링커가 변수와 함수 이름을 찾아(resolving) 링킹 하는 것으로 처리
  * BCPL과 B의 문법 차이는, 취향의 차이도 있음
    * 할당자(=)의 차이
        * BCPL :=
        * B, C =
    * 주석의 차이
        * BCPL //
        * B, C /* */
    * 포트란의 영향을 받은 선언문
        * 변수 이름 앞에, auto, static 등의 지시자가 있음
        * C는 그것에 더하여, 타입 이름까지 있음
  * 위와 같은 문법적인 차이점이 존재하지만, BCPL의 근간인 타입 스트럭쳐와 표현식 평가 규칙 등은 B에 그대로 남아있음
    * 타입없는 변수(또는, 싱글 타입, word 또는 cell)
    * 고정 길이 비트패턴
    * 메모리는 셀(fixed-length bit pattern)의 배열
    * 셀 내 데이타의 의미는 적용되는 오퍼레이션에 의존적
      * \+ 오퍼레이터의 경우, 셀 내의 데이터는, 기계(하드웨어)의 정수 더하기 연산의 operand 의미
  * BCPL, B는 메모리 배열 개념이 동일함
    * 메모리는 셀의 연속적인 배열
    * 배열의 인덱스로 (메모리의) 셀 내의 값이 해석됨
    * 배열 선언
        * BCPL: let V = vec 10
        * B: auto V[10];
    * 배열내 특정 셀에 접근
        * BCPL: V!i
        * B: V[i]
        * B: *(V+1)
    * 당시에는 배열에 대한 이런 접근이 일반적인 것이 아니었음
    * C도 B를 따름
  * BCPL, B, C 모두 문자형 데이타에 대한 지원이 강력하지 않음
    * BCPL 문자열의 첫 패킹된 바이트는 문자열의 길이를 나타냄
    * 반면, B는 '*e'라고 부르는 특수문자로 문자열의 끝을 확인함
      * 스트링 길이 제한을 피하기 위한 이유
      * 스트링 길이를 유지하는 것이 경험상 더 불편하였기 때문
    * 문자열의 각 문자를 을 각 셀에 한 개씩 풀어서 작업하고 다시 패킹하는 형태

# 선C시대
  * TMG 버전 B가 동작한 이후, 톰슨은 B를 B로 재작성함
    * 개발 중에, 톰슨은 계속 메모리 제약 문제로 고민
    * B를 재작성하면서 메모리 사용을 줄이는 기능이 들어감
        * 예) x=+y
        * =+ 표현은 Algol68에서 가져옴. (Mclloy's TMG 버전에 통합된 기능)
        * =+ 는 += 의 오기이나, 1976년 B언어의 처음 lexer에서 고쳐지기 전까지는 계속 사용
  * 톰슨이 ++, -- 같은 연산자를 발명, prefix, postfix 형태를 모두 지원 (초기 버전 B에는 없는 기능)
    * 사람들은 PDP-11 의 auto-increment, auto-decrement 메모리 기능을 사용하기 위해 만든것으로 생각하지만, 이는 틀린 것.
        * B를 만들당시 PDP-11 이 없었음.
        * PDP-7 에도 일부 auto-increment 메모리 셀이 있었긴 했음
          * 이 기능이 톰슨에게 ++, -- 연산자를 만들게하게 했을 수 있지만, prefix, postfix 에 대해 일반화한 것은 톰슨 고유의 것
        * 실제로, 오퍼레이터를 구현할 때, auto-increment 메모리 기능을 직접 사용할 수 없었음
        * ++x 가 x=x+1 보다 작은 형태로 변환되는 것을 관찰한 것이, 혁신의 근거였을 것
  * PDP-7의 B 컴파일러는 머신 코드를 생성하지 않고, 'threaded code'를 생성함
    * threaded code 는, 기본이 되는 기능을 수행하는 코드 조각들에 대한 주소 값의 시퀀스로 컴파일러 결과가 나오고, 이를 해석하여 실행하는 형태
    * simple stack machine으로 동작
  * PDP-7에서, B자체를 제외하고는 B로 쓰여진 것이 매우 작았음
    * 하드웨어가 너무 작고 느렸기 때문
    * OS와 유틸들을 B로 다시 쓰는 것은 너무 비싼 일
    * 그 당시 톰슨은 코드 페이징을 사용하여, 8K의 메모리 제한을 넘을 수 있는 'Virtual B'컴파일러를 내놓음
        * 그러나, 실제 유틸을 사용하긴 너무 느림
    * 그렇지만, B로 쓴 몇 가지 유틸이 있었는데,
        * dc (variable-precision calculator)
    * 당시, 리치가 진행한 야심찬 기획은 GE-635기계에서 돌아가는 코드(threaded code가 아니라)를 직접 만드는 B 언어 크로스 컴파일러
  * Fortran, PL/I, Algol68 같은 메이저 언어를 만드는 것을 생각해 보았으나, 그런 것은 당시 리소스로는 절망적인 크기
    * 하여, 단순하고 작은 툴들을 만들어냄
    * 위의 언어가 작업에 영향을 주었지만, 우리 것을 하는 것이 더 재미남 - 리치
  * 1970년에 PDP-11 을 얻을 수 있었음
    * DEC에서 처음 도착한 건 프로세서, 3개월 뒤 디스크 도착
    * 오퍼레이터를 위한 코드 조각만 사용하는 threaded code를 사용하는 B 프로그램을 작성, 간단한 어셈블러를 B로 작성
    * PDP-11에 OS를 올리기 전에, dc 를 먼저 포팅하여 테스팅
    * 디스크를 기다리는 동안, 톰슨이 유닉스 커널과 기본 명령어를 PDP-11 어셈블러로 재작성
  * 당시에 yacc 첫 번째 버전이 나옴

# C 태동기
  * NB(newB)는 매우 짧은 시간 동안 존재, 언어 설명도 없음
  * int, char 타입, int, char 의 배열, int, char 포인터를 지원
    * [10] 배열 선언
    * [] 는 포인터 선언
    * 타입이 생기면서, 배열의 첨자는 배열 기본 타입의 배수를 어드레싱 하는 것으로 정의

{% highlight c %}
int i, j;
char c, d;
int iarray[10];
int ipointer[];
char carray[10];
char cpointer[];
{% endhighlight %}

  * B에서의 이동을 쉽게 하기 위해,
    * struct 추가
    * struct가 추상적인 표현이지만, 메모리 표현이기도 함
    * 타입 구성은 Algol68에서 빌려온 것,
      * 기본 타입에 기반한 타입 스트럭쳐 (struct), 배열, 포인터, 함수
      * union, 캐스팅 등의 개념은 이후 C 버전에 영향을 끼침
    * 타입 시스템 만든 이후에, NB로 부르기엔 충분치 않아서 새로운 이름을 정함. "C"

# C 유아기
  * 언어가 계속 변경됨
    * &amp;&amp;, \|\| 등 추가
    * 1972-3 시기에 언어가 계속 변경됨
  * 1971년에서 1972년에 B는 NewB로 진화해서 결국 C가 됨: 가장 생산적인 해였다고 회고
  * 1972년에서 1973년 초에 전처리기를 포함하게
    * 초기버전은 단순한 #include, #define 만 지원
    * 이후, 확장되어 인자가 있는 매크로와 conditional compiler 기능 등을 도입

# 이식성
  * 1973년 초, 현대적인 C의 핵심적인 부분이 완료됨.
    * struct 자료형을 추가하고, 여름동안 PDP-11 유닉스 커널을 C로 재작성하며 이런 노력은 완전히 결실을 맺음
        * PL/I, ALGOL에 이어 비 어셈블리어로 운영체제를 개발
    * 톰슨은 sturct가 생기기 전 초기 C 작성에 일부 도움을 줌. 이후 포기
        * 2015년 현재 구글에서 근무
        * 2009년 "Go"로 다시 등장!
    * 해당 기간동안, 컴파일러는 주변 다른 기계를 목표로 함
      * IBM 360/370으로 이식이 필요
        * 마이크 레스크(Mike Lesk)가 포팅 가능한 I/O 패키지를 개발
        * 추후에 C의 표준 I/O 루틴이 됨
        * 마이크 레스크는 후에 "에릭 슈밋"(현 구글 회장)과 Lex를 만듦(IT 회사 CEO를 하려면 실리콘밸리에서는 이 정도는 기본)
  * 1978에 K&R 'The C Programming Language'를 출판
    * K가 책의 대부분 설명 부분을 작성하고,
    * R이 Unix와 연결되는 부분과, 부록 부분의 언어 레퍼런스 부분을 작성함
  * 1973 - 1980 기간, 언어는 더 자라남
    * unsigned, long, union, enum 추가
    * struct는 거의 first-class object가 됨
    * C로 만든 유닉스 커널에서 자신을 얻어, 시스템 유틸을 C로 작성
    * 다른 플랫폼으로도 이동
  * 1977 즈음에, C는 이식성과 타입 안전성에 집중
    * 리치와 스티븐 C. 존슨이 유닉스의 이식성을 높이기 위해 C언어를 추가로 변경
    * 존슨의 Portable C Compiler는 C언어의 여러 구현 버전의 기초가 됨
        * 2007년 다시 개발을 시작하여, C99 스펙을 지원하는 버전 1.0을 "2011년" 4월 1일에 릴리즈
    * 당시의 C는, 타입이 없는 언어를 부모로 둔 티가 많이 나던 언어
  * K&R 책에서, C의 타입 룰을 표시했지만, 그 전의 수 많은 프로그램 때문에, 컴파일러는 조금 더 관대하게 동작했음
    * 사람들에게 공식적인 C의 룰을 따르도록 하기 위해, lint가 등장

# C언어의 진화

## C99

### 디자인
  * C89와 하위호환성을 유지하지만, 일부는 더 강한 제약을 가지게 되었음
    * 실제로, 더 이상, 타입이 없는 경우 int 로 암묵적으로 가정하지 않음

### 새로운 기능

인라인 함수의 도입
  * C++과 동일한 문법

변수의 선언은 더이상 파일 범위나 복합 명령어의 시작에서만 할 필요가 없음

long long int, 선택적인 확장 정수형, 명시적 불린 자료형, 그리고 복소수를 나타내기 위한 complex 자료형 등 새로운 자료형 도입

  * optional extented integer
    * mininum-width integer types 최소크기지정 정수형 (지정한 크기거나 그 보다 커야함)
    * fastest minimum-width integer types 빠른연산 최소크기지정 정수형
        * 연산이 빠르게 되는 것을 기대하는 정수형.
        * 모든 경우의 연산에 대해 가장 빠른 것을 보장하는 것은 아님. 컴파일러 구현에서는 명확하지 않은 경우, 크기와 부호가 맞는 다른 정수형을 사용할 수 있음.
  * _Bool keyword
    * stdbool.h 에서 제공. 다음 매크로를 제공함
        * bool _Bool 과 같음
        * false (_Bool)0 과 같음.
        * true  (_Bool)1 과 같음.
    *  C99에서 bool 타입은 정수형
  * _Complex keyword

{% highlight c %}
int_least8_t   uint_least8_t
int_least16_t  uint_least16_t
int_least32_t  uint_least32_t
int_least64_t  uint_least64_t

int_fast8_t  uint_fast8_t
int_fast16_t uint_fast16_t
int_fast32_t uint_fast32_t
int_fast64_t uint_fast64_t
{% endhighlight  %}

가변 길이 배열(VLA: variable-length array)

{% highlight c %}
float read_and_process(int n)
{
  float vals[n];
  for (int i = 0; i < n; i++)
    vals[i] = read_val();
  return process(vals, n);
}
{% endhighlight  %}

BCPL이나 C++와 같은 //로 시작하는 주석들

snprintf와 같은 새로운 라이브러리 함수

stdbool.h, inttypes.h, complex.h, tgmath.h 와 같은 새로운 헤더 파일들

자료형에 무관하게 동작하는(type-generic) 수학 함수들 (tgmath.h에 포함)
  * math.h, complex.h에서 제공되는 수학함수들의 type generic 매크로를 tgmath.h에서 제공
  * 제한적인 형태의 함수 오버로딩 기능. 컴파일타임에 매크로 치환.

{% highlight c %}
extern float cos(float x);
extern double cos(double x);
extern long double cos(long double x);
...
p = cos(0.78539f); 
// 를 호출하는 경우 float cos(float x)가 호출됨. 0.78539f 로 타입을 확인
{% endhighlight  %}

  * C++에는 제대로된 함수 오버로딩 기능이 있으므로, 불필요함.

IEEE 부동소수점 자료에 대한 개선된 지원

지정된 이니셜라이저(designated initializers)

{% highlight c %}
int a[6] = { 0, 0, 15, 0, 29, 0 };
int a[6] = { [4] = 29, [2] = 15 };  
// C99 designated initializer 사용. 위와 같은효과.

struct point { int x, y; };
struct point p = { xvalue, yvalue };
struct point p = { .y = yvalue, .x = xvalue };  
// C99 designated initializer 사용. 위와 같은 효과. 
{% endhighlight  %}


복합 리터럴(compound literals)
  * 초기화를 캐스팅하는 것처럼 보임

{% highlight c %}
struct foo {int a; char b[2];} structure; 
// 이런 구조체 정의가 있는 경우,

structure = ((struct foo) {x + y, 'a', 0}); 
// compound literals 을 이용하여 구성
// 위 문장은 다음과 동일함.
{
  struct foo temp = {x + y, 'a', 0};
  structure = temp;
}
{% endhighlight  %}

  * 복합리터럴은 어디에나 사용가능함

{% highlight c %}
int x;
x = (int) { 1 } + (int) { 3 }
// 위 문장은 다음과 동일
int x;
int unnamed1 = {1};
int unnamed2 = {3};
x = unnamed1 + unnamed2;
// unnamed object 가 생김
{% endhighlight  %}

  * 함수 인자를 처리할 때 효율적임.

{% highlight c %}
struct POINT { int x, int y };
void drawline(struct POINT start, struct POINT end);
drawline((struct POINT) { 1, 2 }, (struct POINT) { 3, 4 }) 
// 복합리터럴을 인자로 사용한 함수 호출 
// 복합리터럴이 없는 경우 코드를 상상해보면, 왜 좋은지 알게됨
{% endhighlight  %}

가변 인수 매크로(Variadic macro)의 도입

{% highlight c %}
MYLOG(FormatLiteral, ...) \
  fprintf (stderr, "%s(%d): " FormatLiteral "\n", __FILE__, __LINE__, __VA_ARGS__) 
{% endhighlight  %}

보다 적극적인 코드 최적화를 위한 restrict 한정자
  * 포인터에 사용

{% highlight c %}
void updatePtrs(size_t *ptrA, 
                size_t *ptrB, 
                size_t *val)
{
  *ptrA += *val;
  *ptrB += *val;
}
// 인자의 *ptrA, *ptrB, *val 이 모두 같은 메모리 영역을 가리키지 않는다면, 다음과 같이 선언.
void updatePtrs(size_t *restrict ptrA, 
                size_t *restrict ptrB, 
                size_t *restrict val);
{% endhighlight  %}

  * 포인터가 서로 다른 곳을 가리키는 것을 "프로그래머"가 보장
    * 컴파일러는 최적화를 수행하기가 용이해짐

## C11

  * C11 GCC 4.6, Clang 3.1 이후 지원

Alignment specification (메모리 정렬 지정) &lt;stdalign.h>

  * _Alignas specifier.
  * alignof operator
  * aligned_alloc function

{% highlight c %}
int alignas(double) b;  // double 에 맞게 b 를 align
alignas(double) unsigned char buf[sizeof(double)];
// unsigned char 타입 buf를 sizeof(double) 크기만큼 할당하되, 
// double을 담을(hold a double) 수 있게 align.

alignas(max_align_t) 를 사용하면, platform 에서 제공하는 모든 타입을 담을 수 있음.

aligned_alloc(size_t bound, size_t nbytes)
// nbytes 를 bound 에 맞춰 할당
{% endhighlight  %}

_Noreturn function specifier
  * 함수가 리턴하지 않음을 명시함. // caller 로 돌아오지 않음.
  * 컴파일러 최적화에 도움이 됨 // caller 로의 리턴주소를 스택에 저장하지 않아도 됨.

{% highlight c %}
_Noreturn void f() {
  abort();
  }
{% endhighlight  %}

_Generic keyword. Type-generic 표현식 제공

{% highlight c %}
#define cbrt(X) \
  _Generic((X), long double: cbrtl, default: cbrt, float: cbrtf)(X)
// X 의 타입에따라서, cbrtl(X), cbrt(X), cbrtf(X) 로 적절히 치환.
// 참고로, cbrt 함수는 세제곱근 구하는 함수
{% endhighlight  %}

멀티쓰레드 지원

  * _Atomic 타입. <stdatomic.h>, uninterruptible object access

유니코드 지원 향상

  * UTF-16, UTF-32 인코딩 데이타를 위한, char16_t, char32_t 타입 및 커버전 함수들(<uchar.h>)
  * unicode 리터럴을 위한 u, U prefix

gets() 함수 제거.(이전 버전표준에서 deprecated 처리)

  * 대신, gets_s() 함수 제공

{% highlight c %}
char *gets( char *str );
char *gets_s(char *str, rsize_t n);
{% endhighlight  %}


Bounds-checking interface

  * 바운드 검사를 하는 안전한 버전의 문자열 처리함수 제공
    * 기존 함수에 _s suffix 를 붙여서 제공
    * 기존 문자열함수에서 길이를 입력받는 함수가 있었으나, buffer overrun 을 막기위한 용도. 
      * 문자열바운드(null) 처리는 적절하게 들어있지 않았음.

{% highlight c %}
//C11, safe version of strcat
errno_t strcat_s(char * restrict s1, 
                 rsize_t s1max, 
                 const char * restrict s2);
{% endhighlight  %}

fopen 모드 추가

  * x 모드 추가. O_CREAT \| O_EXCL 과 동일한 의미 (lock 파일등에서 주로 사용됨)

fopen_s 제공

{% highlight c %}
errno_t fopen_s(FILE * restrict * restrict streamptr, 
                const char * restrict filename, 
                const char * restrict mode);

{% endhighlight  %}

Anonymous structs and unions

  * 유니온과 구조체가 중첩되는 경우 유용함

{% highlight c %}
struct T {
  int m;
  union {     // anonymous
    char* index;
    int key;
  };
};

struct T t;
t.key = 1300;  // anonymous union의 데이타를 직접 접근
{% endhighlight  %}

quick_exit 제공

  * 최소한의 deinitialization 으로 프로그램 종료
  * exit가 실패할 경우 사용.

복소수 생성을 위한 매크로 제공

{% highlight c %}
#include <complex.h>
double      complex CMPLX( double x, double y ); 
float       complex CMPLXF( float x, float y );
long double complex CMPLXL( long double x, long double y ); 

#define CMPLX(x,y) ((double)(x)+_Imaginary_I*(double)(y))
#define CMPLXF(x,y) ((float)(x)+_Imaginary_I*(float)(y))
#define CMPLXL(x,y) ((long double)(x)+_Imaginary_I*(long double)(y))
{% endhighlight  %}

static assertion 제공

  * static assertion은 컴파일 시점에 조건을 확인하는 것
    * 조건에 맞지 않으면, 컴파일 실패
    * 타입 크기 호환성 검사등에 유용함

{% highlight c %}
_Static_assert(sizeof(size_t) >= 8, 
    "size_t must be at least 64-bits");
_Static_assert(sizeof(void *) == sizeof(void(*)()), 
    "object pointer must be the same size as function pointer");
{% endhighlight  %}

# 다른 언어로의 진화

  * C++: C를 왜 쓰냐?
  * Go: 이 시대에 새로운 시스템 프로그래밍 언어로서

# 참고자료
  * HelloWorld 
    * http://en.wikipedia.org/wiki/List_of_Hello_world_program_examples
    * http://c2.com/cgi/wiki?SmalltalkHelloWorld
  * http://en.wikipedia.org/wiki/C99
  * http://en.wikipedia.org/wiki/C11_(C_standard_revision)
  * http://cm.bell-labs.com/cm/cs/who/dmr/
  * http://cm.bell-labs.com/cm/cs/who/dmr/chist.html

