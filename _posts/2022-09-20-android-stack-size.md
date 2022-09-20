---
layout: post
title: "안드로이드 스택 크기 변경"
date: 2022-09-20 01:00:00
categories: blog
image: android-stack-size.png
description: 안드로이드 스택 크기 바꾸기
---

Thread를 만들 때, 스택 크기도 설정할 수 있어요. 스택 크기를 늘린 쓰레드를 하나 만들고 거기서 굴리면 되는거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/android-stack-size.png)

대충 이런식인데,

```java
import java.lang.Thread;
import java.lang.ThreadGroup;
.
.
.
ThreadGroup group = new ThreadGroup("쓰레드 그룹 이름");
new Thread(group, new Runnable() {
    @Override
    public void run() {
        //실행할 내용
    }
}, "쓰레드 이름", stack_size).start();
```
<br>

플랫폼에 따라 `스택 크기`는 아무런 영향을 주지 않을 수도 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/android-stack-size/0.png)

<br>

안드로이드에서 기본 스택 크기는 8kB이고, 최대 256kB까지 올릴 수 있다고 들었으나, 실제로 해본 결과 더 올려도 잘 작동하더라구요.

​
[이 질문에 대한 답변](https://stackoverflow.com/questions/16843357/what-is-the-android-ui-thread-stack-size-limit-and-how-to-overcome-it)을 확인해보면 사실 기본 크기도 8kB가 아니라 계속 바뀌는 듯

<br>
아무튼, 대충 이게 스택 크기 바꿔가면서 오버플로우 뜰 때까지 재귀호출 돌리면서 얼마나 호출되나 볼려고 만든건데

![image]({{site.url}}{{site.baseurl}}/assets/images/android-stack-size/1.png)

<br>
스택 크기를 각각 기본, 256kB, 1MiB, 약 137MiB로 설정하고, 재귀 호출 돌리면서 얼마나 많이 돌아가나 본건데,

![image]({{site.url}}{{site.baseurl}}/assets/images/android-stack-size/2.png)

<br>
256kB 이상을 넘겨도 아주 잘 되네요?

![image]({{site.url}}{{site.baseurl}}/assets/images/android-stack-size/3.png)

<br>
추가적으로, `라이노 엔진`에서 문법만 자바스크립트 바꿔서 사용하는 경우는 별로 영항이 없나봐요. 그거 때문에 찾아봤던건데;;
