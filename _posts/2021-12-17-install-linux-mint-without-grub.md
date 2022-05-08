---
layout: post
title: "grub 빼고 리눅스 민트 설치하기"
date: 2021-12-17 23:00:00
categories: blog
image: install-linux-mint-without-grub.png
description: 리눅스 민트 설치할 때 부트로더는 제외시키기
---

리눅스 민트를 설치할 때 부트로더를 설치할 위치를 무조건 선택해야 해요.

![image](https://darktornado.github.io/blog/assets/images/install-linux-mint-without-grub/0.png)

<br>

리눅스 민트 설치 프로그램의 이름은 `ubiquity`에요. 보시다싶이, 터미널에 `ubiquity`를 입력해보면 옵션으로 `-b`를 넘기면 부트로더를 설치하지 않는다고 써있어요.

![image](https://darktornado.github.io/blog/assets/images/install-linux-mint-without-grub/1.png)

<br>

그런고로, `ubiquity -b`로 리눅스 설치를 시작하면

![image](https://darktornado.github.io/blog/assets/images/thumb/install-linux-mint-without-grub.png)

<br>

이런식으로 부트로더 설치를 하지 않을 수도 있어요.

![image](https://darktornado.github.io/blog/assets/images/install-linux-mint-without-grub/2.png)

<br>

리눅스 민트 중 데비안 기반인 `LMDE` 같은 경우는 설치 과정에서 부트로더를 설치하지 않도록 선택할 수 있어요.