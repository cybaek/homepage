---
layout: post
title:  Java8의 람다
date:    2015/04/28 21:45
categories: java
---

Java8의 가장 큰 변화를 꼽으라고 한다면 람다라는데 이견이 없을 것입니다.

코드가 간결해지고 좋다니 한번 써봐야지라고만 생각하다가 다음 링크를 읽고 완전히 반했습니다. 도입 과정을 이해하고 나니 느낌이 달랐습니다.

http://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html

쉬운 영어지만, 설명을 풀어보겠습니다.

## 상황

다음과 같은 Person 클래스가 있다고 가정합니다.

{% highlight java %}
public class Person {

    public enum Sex {
        MALE, FEMALE
    }

    String name;
    LocalDate birthday;
    Sex gender;
    String emailAddress;

    public int getAge() {
        // ...
    }

    public void printPerson() {
        // ...
    }
}
{% endhighlight %}

이 인스턴스의 목록을 `roster`라는 변수에 담고 있습니다.

## 특정 조건으로 필터링

특정 연령 이상을 뽑아서 해당 `Person` 인스턴스의 `printPerson()` 메소드를 호출한다면 다음과 같이 작성할 것입니다.

{% highlight java %}
public static void printPersonsOlderThan(List<Person> roster, int age) {
    for (Person p : roster) {
        if (p.getAge() >= age) {
            p.printPerson();
        }
    }
}
{% endhighlight %}

## 추가 필터링 조건

만일 특정 연령 범위로 필터링을 한다면 다음의 메소드를 또 만들어야 합니다.

{% highlight java %}
public static void printPersonsWithinAgeRange(
    List<Person> roster, int low, int high) {
    for (Person p : roster) {
        if (low <= p.getAge() && p.getAge() < high) {
            p.printPerson();
        }
    }
}
{% endhighlight %}

거의 비슷하고 필터링하는 조건 부분만 다르죠. 하지만 메소드를 또 하나 만들었습니다.

## 필터링 조건을 추상화

검사하는 부분을 인터페이스로 만들어서 다음과 같이 개선할 수 있습니다.

{% highlight java %}
interface CheckPerson {
    boolean test(Person p);
}

public static void printPersons(
    List<Person> roster, CheckPerson tester) {
    for (Person p : roster) {
        if (tester.test(p)) {
            p.printPerson();
        }
    }
}

class CheckPersonEligibleForSelectiveService implements CheckPerson {
    public boolean test(Person p) {
        return p.gender == Person.Sex.MALE &&
            p.getAge() >= 18 &&
            p.getAge() <= 25;
    }
}

printPersons(
    roster, new CheckPersonEligibleForSelectiveService());
{% endhighlight %}

이제 필터링 조건이 다르다고 그 때마다 메소드를 만들지 않아도 됩니다. 그저 `CheckPerson` 인터페이스를 구현한 클래스만 만들어서 인자로 넘기면 됩니다.

## 익명 클래스 도입

앞에 경우 `printPersons()`는 일반화를 했지만, 인자로 넘기는 클래스를 매번 별도 파일에서 정의하고 호출하는 일은 번거롭습니다. 
특히 그렇게 만든 클래스를 보통 한 번만 사용하기에 더더욱 귀찮죠. 이럴 때 흔히 익명 클래스를 사용합니다.

{% highlight java %}
printPersons(
    roster,
    new CheckPerson() {
        public boolean test(Person p) {
            return p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        }
    }
);
{% endhighlight %}

이제 호출하는 순간에 클래스를 정의해서 바로 넘깁니다.

## 람다를 이용해서 더 간결하게

앞에 코드를 람다를 이용해서 간결하게 작성할 수 있습니다.

{% highlight java %}
printPersons(
    roster,
    (Person p) -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
{% endhighlight %}

`CheckPerson`의 인터페이스를 보면 메소드는 하나이고, 그 메소드는 `boolean` 반환하고 인자는 하나입니다.
앞 코드 처럼 적으면 알아서 가장 적합한 인터페이스에 매핑해줍니다.
지금의 경우 `Person`이라는 타입 명시도 할 필요가 없습니다. 그러면 더 간결해집니다.

{% highlight java %}
printPersons(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
{% endhighlight %}

## 자주 사용하는 함수적 인터페이스

앞에서 언급한 그런 유형의 인터페이스는 매우 많이 사용합니다. Java8의 `java.util.function`에 가보면 이런 인터페이스가 가득합니다.
굳이 `CheckPerson`같은 인터페이스를 정의할 필요도 없습니다.
이제 코드를 다음처럼 확 줄일 수 있습니다.

{% highlight java %}
public static void printPersonsWithPredicate(
    List<Person> roster, Predicate<Person> tester) {
    for (Person p : roster) {
        if (tester.test(p)) {
            p.printPerson();
        }
    }
}

printPersonsWithPredicate(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
{% endhighlight %}

`Person` 클래스를 제외하고 이게 전부입니다.

## 필터링 후 하는 행위도 일반화

현재 메소드를 보면 조건에 만족할 경우 `p.printPerson()`을 호출하는데요. 그 동작이 다른 경우가 있다면 다시 비슷한 메소드를 하나 더 만들어야 합니다.
하지만 람다를 이용하면 앞서 조건을 코드로 넘긴 것처럼 해야할 행동도 코드로 넘길 수 있습니다.

{% highlight java %}
public static void processPersons(
    List<Person> roster,
    Predicate<Person> tester,
    Consumer<Person> block) {
        for (Person p : roster) {
            if (tester.test(p)) {
                block.accept(p);
            }
        }
}
{% endhighlight %}

Predicate은 boolean을 반환했는데 Consumer는 이름처럼 뭔가를 하고 반환하는 것은 없습니다. printPerson()과 같은 일에 딱 맞는 인터페이스입니다.

이제 호출하는 쪽에서 원하는 작업을 넘기면 됩니다.

{% highlight java %}
processPersons(
     roster,
     p -> p.getGender() == Person.Sex.MALE
         && p.getAge() >= 18
         && p.getAge() <= 25,
     p -> p.printPerson()
);
{% endhighlight %}

`Person`을 받아서 `Person`을 그대로 사용하지 않고 `Person`을 뭔가로 변환 매핑한 다음에 그 결과물을 출력할 수도 있습니다.
흔한 일입니다. 이런 경우에 알맞는 함수적 인터페이스는 `Function`입니다. 이것을 적용하면 다음과 같은 코드가 나옵니다.

{% highlight java %}
public static void processPersonsWithFunction(
    List<Person> roster,
    Predicate<Person> tester,
    Function<Person, String> mapper,
    Consumer<String> block) {
    for (Person p : roster) {
        if (tester.test(p)) {
            String data = mapper.apply(p);
            block.accept(data);
        }
    }
}

processPersonsWithFunction(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25,
    p -> p.getEmailAddress(),
    email -> System.out.println(email)
);
{% endhighlight %}

`Person`을 `email`로 바꿔서 `email`을 출력합니다.


## 조금 더 일반화하면

`Person`뿐만 아니라 어떤 타입도 사용할 수 있도록 바꾸면 다음과 같습니다.

{% highlight java %}
public static <X, Y> void processElements(
    Iterable<X> source,
    Predicate<X> tester,
    Function <X, Y> mapper,
    Consumer<Y> block) {
    for (X p : source) {
        if (tester.test(p)) {
            Y data = mapper.apply(p);
            block.accept(data);
        }
    }
}

processElements(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25,
    p -> p.getEmailAddress(),
    email -> System.out.println(email)
);
{% endhighlight %}

## stream을 이용하면

Java8에서 `Collection` 객체에 `stream()`을 추가했습니다. 이것을 이용하면 앞에서 정의한 `processElements()`마저 필요없습니다.

{% highlight java %}
roster
    .stream()
    .filter(
        p -> p.getGender() == Person.Sex.MALE
            && p.getAge() >= 18
            && p.getAge() <= 25)
    .map(p -> p.getEmailAddress())
    .forEach(email -> System.out.println(email));
{% endhighlight %}

이게 전부입니다. `CheckPerson`이나 `processElement()` 등 그 어떤 것도 필요 없습니다. 

---

람다를 안 쓸 이유가 없지요?