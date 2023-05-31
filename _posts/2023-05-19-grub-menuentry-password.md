---
layout: post
title: "grub에서 일부 menuentry에만 비밀번호 걸기"
date: 2023-05-19 02:00:00 +0900
categories: blog
image: grub-menuentry-password.jpg
description: "사실은 grub 자체에 menuentry에 비밀번호 걸고, 일부 menuentry에만 풀기"
---

**저는 이 게시글을 따라함으로서 발생하는 모든 일에 대하 책임을 지지 않아요.**

글 이름은 `grub에서 일부 menuentry에만 비밀번호 걸기`지만, 실제로 다룰 내용은 `grub` 자체에 비밀번호를 걸어서 아무것도 못하게 만들어두고, 일부 `menuentry`는 비밀번호를 요구하지 않도록 만들거에요.
아무튼, 일부 `menuentry`에만 비밀번호를 거는 것과 거의 동일한 결과를 만들 수 있긴 해요.

뭐 하나 잘못 입력하거나 하면 `grub` 자체가 망가져버리는 불상사가 발생할 수 있으니 참고하세요.
일단 전 가상머신으로 테스트해봤어요.

***
## grub에 비밀번호 걸기

일단, 다음 내용을 `00_header` 파일을 열어서 맨 아레에 또는 `01_password` 파일을 만들어서 그 안에 적든 하면 되는거에요.
```sh
car << EOF
set superusers="{사용자계정이름}"
password {사용자계정이름} {비밀번호}
EOF
```
![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/0.png)

<br>
전 굳이 `01_password` 파일을 만들어서 따로 뺐어요.
가상머신에 실험용으로 깔아둔 아치리눅스에서 실험하면서 찍은 스샷인지라, 사용자 계정 이름이 `test`에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/1.png)

이제 `update-grub` 같은걸 하면,
```sh
$ sudo update grub
//또는
$ sudo grub-mkconfig -o /boot/grub/grub.cfg
```

<br>
이제 `grub`에서 메뉴를 고르거나 `c` 키나 `e` 키를 통해 무언가를 하려고 하면, 이런식으로 사용자 이름과

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/2.jpg)

<br>
비밀번호를 입력하라고 뜰거에요. 로그인하듯이 비밀번호를 입력하면 해당 `menuentry`에서 하려는 동작을 할 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/grub-menuentry-password.jpg)


***
## 일부 menuentry는 비밀번호 없이 작동하게 하기

적당한 위치에 `--unrestricted`를 적으면 되는거에요.

일단, 해당 `grub`를 사용하는 리눅스의 경우 `menuentry` 옆에 들어갈 문구가 변수 `CLASS`에 담기니, 거기다가 슬쩍 `--unrestricted`를 적어주면,

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/3.jpg)

<br>
`grub`에서 해당 리눅스를 선택하니 이런식으로 바로 선택되면서 켜지네요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/4.jpg)

<br>
`os-prober`도 아래에 밑줄친 부분을 슬쩍 보니, 변수 `CLASS`건들면 될 것 같아서, 위에 밑줄친 부분처럼 슬쩍 수정하니, 듀얼부팅으로 함께 깔려있는 윈도우를 `grub`에서 선택했더니 비밀번호 입력 없이 바로 켜졌어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/5.png)

<br>
이런식으로, `.iso 파일`을 넣어두고 `grub`에서 바로 라이브 부팅하는 경우도 비밀번호 입력이 필요하게 만들 수 있어요.

아래 사진에서 우분투처럼 뒤에 `--unrestricted`를 안붙이면 비밀번호 입력이 필요하고, 페도라처럼 `--unrestricted`를 붙이면 바로 켜지는거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-menuentry-password/6.png)

<br>
사실, 전 `grub`에서 바로 `.iso 파일`로 라이브 부팅을 가능하게 설정해놓고 싶어서 이런 뻘짓을 한거에요.
아무리 비밀번호를 잘 설정해두어도, 모르는 사람이 제 PC에서 `.iso 파일`로 라이브 부팅하는 메뉴를 골라버리면 PC 안에 있는 것들을 다 볼 수도 있고, 아무나 `root` 권한도 쓸 수 있기 때문이에요.

어차피 USB 연결해서 부팅 우선순위 바꾸면 되는거 아니냐는 생각이 들 수도 있지만, 그건 제가 바이오스 자체에 비밀번호를 걸어버려서 바이오스 진입을 못하게 만들어서 해결헸어요.

사실, 바이오스 자체에 걸어놓은 비밀번호를 부팅시마다 요구하는 방법도 있지만, 그러면 올바른 비밀번호가 입력될 때까지 화면이 계속 최대 밝기로 켜진 상태로 방치되는지라, 아무것도 안건들면 리눅스로 부팅되도록 만들어두기 위해서 사용하지 않았어요.