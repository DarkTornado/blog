---
layout: post
title: "라이노 엔진 Script 객체 관련"
date: 2022-04-11 01:00:00
categories: blog
image: rhino-script-object.jpg
description: 라이노 자바스크립트 엔진에 있는 Script 객체는 무엇일까?
---

라이노 자바스크립트 엔진에서 `Script();`라는 함수를 사용하면 인자로 넘긴 소스를 최적화시킨 결과물을 반환하는데, 오류가 있는 소스를 인자로 넘기면 오류 메시지가 뜨기도 해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/rhino-script-object/0.png)

<br>

### Script 객체
- 라이노 엔진에 있는 `Script`는 객체는 `NativeScript`라는 자바 클래스로 구현되어 있어요.
- 다만, 라이노 엔진 문서에는 `NativeScript`에 대한 설명이 없기 때문에, 라이노 엔진의 소스를 참고하면서 작성된 글입니담.

![image]({{site.url}}{{site.baseurl}}/assets/images/rhino-script-object/1.png)

***

### 생성자

- 생성자를 호출하면 매개변수로 받은 소스 코드를 컴하일해서 실행하기 직전 단계까지 만들어요.
- 그래서 위 스크린샷처럼 `Script();`에 문법적으로 틀린 소스를 넘기면 오류가 발생한거에요.

- 인자를 여러개 넘겨도 Script 객체에게 넘어가긴 하지만, 가장 앞에 있는 인자를 제외하고는 전부 무시될거에요.

### Script.prototype.compile();

- 생성자와 동일한 역할을 해요.
- 내부 구조는 아주 조금 다르지만 사실상 동일하게 작동해요.

### Script.prototype.exec();

- 무조건 예외를 던지는 함수에요.
- 이 함수는 직접 호출해야 한다는 오류가 출력되는데, 소스를 뜯어보면 그냥 예외를 던지는 부분만 있어요.

### Script.prototype.toString();

- 실행 직전 상태인 컴파일된 결과물을 다시 소스로 되돌린 결과를 반환해요.

***

- 생성자 함수도 함수니까 `String(소스);`를 하면 해당 소스를 컴파일하고, 그 내용을 출력하면 문자열로 바꾸기 위해 `.toString();` 메서드를 호출하기에 다시 소스로 돌아온거에요.
- 즉, 소스를 최적화시키는 함수가 아니라, 소스를 컴파일해서 실행 직전으로 만들었다가 다시 디컴파일해서 소스로 되돌린 결과물이 출력된거에요.

- 아무튼 다음과 같은 형식으로 사용하는게 정석이에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/rhino-script-object/2.png)
