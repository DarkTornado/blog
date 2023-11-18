---
layout: post
title: ".iso 파일 넣기만 해면 되는 부팅 USB 만들기"
date: 2023-06-08 00:00:00 +0900
categories: blog
image: ventoy-usb.png
description: "ventoy를 사용해서 .iso 파일 넣기만 해면 되는 부팅 USB 만들기"
---

<span style="color:#FF1744">저는 이 게시글을 따라함으로서 발생하는 모든 일에 대하 책임을 지지 않아요.</span>

`ventoy`라는 프로그램을 통해 USB를 포멧하면, `.iso 파일`을 넣기만 하면 그 `.iso 파일`로 부팅이 가능한 USB를 만들 수 있어요.

우선 [여기를 눌러서](https://www.ventoy.net/en/download.html) `ventoy` 다운로드 사이트로 이동하신 뒤에,
본인 운영체제에 맞는 파일을 눌러보세요.

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/0.png)

<br>
그러면 깃허브 릴리즈 페이지로 갈텐데, 여기서 본인 운영제체에 맞는 버전을 다운로드하시면 될거에요.
일단 전 윈도우에서 사용할 예정이였으니, 윈도우 버전으로 받았어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/1.png)

<br>
압축을 풀면 나오는 파일들 중 `Ventoy2Disk.exe` 파일을 실행하시면 되는거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/2.png)

<br>
PC에 연결한 USB들 중 `.iso 파일`을 넣기만 해도 부팅 가능한 USB로 만들 USB 선택.
**당연히 USB 안에 있는 파일들은 전부 사라지는거에요.**

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/3.png)

<br>
**USB에 있는 파일들 다 지워진다고 알려주는 창이에요.** 두 번 물어볼거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/4.png)

<br>
아무튼 포멧 시작

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/5.jpg)

<br>
끝

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/6.png)

<br>
아햏햏

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/7.png)

<br>
뭔가 파티션을 나눠서 구석에다가 EFI 파티션을 만들어둔 듯한 느낌이에요. 저 안에 `grub`가 깔려있을 것 같은건 기분탓

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/8.png)

<br>
아무튼 이런식으로 `.iso 파일`들을 넣어두고

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/9.png)

<br>
PC의 부팅 우선순위 등을 바꾸거나 해서 USB로 부팅하면 이렇게 안에 있는 파일들 목록이 나와요.
여기서 `방향키`와 `엔터키`를 통해 어느 `.iso 파일`로 부팅할지 고르시면,

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/10.png)

<br>
이런식으로 부팅될거에요. 아래 사진은 `윈도우 10 .iso 파일`을 골랐을 때 모습이에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/ventoy-usb/11.jpg)


<br>
참고로, 모든 `.iso 파일`들이 `ventoy`를 통해 부팅 가능한건 아니에요.
