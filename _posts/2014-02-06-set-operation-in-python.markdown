---
layout: post
title:  파이선의 set 연산
date:    2014/02/06 09:00
categories: python set
---
파이선에는 set이라는 타입이 있습니다.
key만 있고 value는 없는 dict라고 생각하면 됩니다.

A, B라는 set이 있을 때 다음의 연산을 지원합니다.

합집합 A | B
교집합 A & B
차집합 A – B
대칭차집합 A ^ B
다음 코드는 두 목록에 다 속하는 대상을 뽑는 ‘일반적인’ 코드입니다.

{% highlight python %}
def get_both_popular_and_active_users():
  # Assume the following two functions each return a
  # list of user names
  most_popular_users = get_list_of_most_popular_users()
  most_active_users = get_list_of_most_active_users()
  popular_and_active_users = []
  for user in most_active_users:
    if user in most_popular_users:
      popular_and_active_users.append(user)

  return popular_and_active_users
{% endhighlight %}
  
이리 복잡하게 할 것 없이 그냥 & 연산자를 사용하면 됩니다.

{% highlight python %}
def get_both_popular_and_active_users():
  # Assume the following two functions each return a # list of user names
  return(set(get_list_of_most_active_users()) & set(get_list_of_most_popular_users()))
{% endhighlight %}
