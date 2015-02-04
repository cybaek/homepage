---
layout: post
title:  안드로이드 브라우저의 홈 페이지 주소 바꾸기
date:    2013/02/21 09:00
categories: java android
---
브라우저 홈페이지 주소를 API를 이용하여 바꿀 일이 있어 시도를 해봤는데요. 결론은 안 됩니다.

서로 다른 앱 간에 preference 파일을 읽고 쓸 일이 있을 때, 파일을 생성하는 쪽에서 Context.MODE_WORLD_READABLE로 생성하면 어떤 앱이든 읽고 쓸 수 있지만 디폴트인 Context.MODE_PRIVATE으로 생성하면 읽을 수 없습니다. 안드로이드는 기저가 리눅스이고, 결국 이런 모드에 따라 생성하는 파일의 권한은 리눅스 권한 관리를 따릅니다. 전자는 -rw-rw—-로 생성되고 후자는 -rw-rw-rw-입니다. 앱 마다 서로 다른 uid가 할당되니 전자는 당연히 읽을 수가 없는 것입니다.

하지만 Context.MODE_PRIVATE으로 생성한 파일이라도 아예 방법이 없는 것은 아닙니다. 파일을 생성하는 앱에서 AndroidMenifest 파일에서 다음과 같이 sharedUserId 속성을 정의해주고, 공유한 파일을 접근하고 싶어하는 앱에서도 똑같이 이 설정을 넣어주면 uid가 동일하게 되어 Context.MODE_PRIVATE 파일도 접근할 수 있습니다.

{% highlight xml %}
<manifest xmlns:android=”http://schemas.android.com/apk/res/android&#8221;
package=”com.example.writer”
android:sharedUserId=”com.android.browser”
android:versionCode=”1″
android:versionName=”1.0″ >
{% endhighlight %}

불행히도 com.android.browser의 AndroidMenifest 파일에는 sharedUserId 속성이 없습니다. 즉, 브라우저의 홈페이지 주소를 바꿀 수 없다는 것입니다.

{% highlight xml %}
<manifest xmlns:android=”http://schemas.android.com/apk/res/android&#8221; package=”com.android.browser”>
{% endhighlight %}