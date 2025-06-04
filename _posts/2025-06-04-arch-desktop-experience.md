---
layout: post
title: "아치 리눅스에 데스크톱 환경 설치"
date: 2025-06-04 09:00:00 +0900
categories: blog
image: arch-desktop-experience.png
description: "아치 리눅스에 데스크톱 환경 설치하기"
---

<span style="color:#FF1744">저는 이 게시글을 따라함으로서 발생하는 모든 일에 대하 책임을 지지 않아요.</span>

`아치 리눅스`는 굳이 없어도 되는 것들은 다 없는 상태라서, GUI도 없어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/0.png)

<br>
그래서, 이런식으로 검은 배경에 하얀 글자만 적힌 화면이 나올텐데,
마우스로 아이콘을 클릭하거나 하는 방식으로 사용할 수 있는 GUI 환경을 원한다면, `데스크톱 환경`이나 `창 관리자`를 설치해야 해요.

일단 쭉 읽어보시면서, 무엇을 쓰고 싶은지 결정하고 설치하세요.
설치한 `데스크톱 환경`을 지울 수는 있는데, 말끔하게 다 지워지지는 않을거에요.

***

# 데스크톱 환경 설치

## GHOME (그놈)

`그놈`은 `우분투`, `페도라` 등 유명한 리눅스 배포판들이 사용해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/1.png)


![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/2.png)

### 설치 명령어
```
# pacman -S gnome
# systemctl enable gdm.service
```
<br>

## KDE Plasma

`KDE`는 `KDE`에서 개발한 데스크톱 환경의 이름으로, 독일어기 때문에 `카데에`라고 읽는 것이 맞지만 전부 `케이디이`로 읽고, 한국에서는 종종 `크데`라고 부르기도 해요.
개발하는 곳의 이름도 `KDE`고, 거기서 개발하는 프로그램의 이름도 `KDE`.

지금은 `Plasma`로 이름이 바뀌었는데, 그냥 `KDE`라고만 말해도 알아서 다 알아들어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/3.png)

<br>
이건 `KDE Plasma`를 사용하는 `페도라`로 부팅한 모습. 개인적으로 아주 예쁘다고 생각해요. `페도라`는 기본적으로 `그놈`을 사용하지만, `KDE` 버전도 존재해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/4.png)

<br>
생긴 것에 비해 생각보다 많이 무거운 환경은 아니에요.

### 설치 명령어
```
# pacman -S plasma plasma-wayland-session
# pacman -S konsole    // 터미널 앱은 같이 설치되지 않으니, 별도로 설치
# pacman -S xorg-server
# systemctl enable sddm
```
<br>

## xfce

깔끔하고 단순하며 가벼운 환경. 그래서 디자인이 뭔가 조금 덜 화려한 듯한 느낌도 들지만,

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/5.png)

<br>
테마 적용 등을 통해 있어보이게 바꿀 수 있어요. `xfce`를 기본 데스크톱 환경으로 사용 하는 `칼리 리눅스`로 부팅한 모습

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/6.png)

### 설치 명령어
```
# pacman -S xfce4 xfce4-goodies
# pacman -S lightdm lightdm-gtk-greeter
# pacman -S xorg-server
# systemctl enable lightdm
```
<br>

### Cinnamon (시나몬)

`그놈3`를 기반으로 경량화 등을 시킨 데스크톱 환경이에요.
아마 시나몬만 설치하면 시커먼 배경이 튀어나올 수도 있는데, 그건 그냥 바탕화면 설정을 안해서 그래요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/arch-desktop-experience.png)

<br>
군대에서 `사이버 지식 정보방` 컴퓨터에 웬 윈도우 대신 요상한 환경이 깔려있는 경험을 했을 수도 있는데, 그건 아마 `하모니카`일거에요.
`하모니카`는 `시나몬`을 기본 데스크톱 환경으로 사용해요. 원래는 `마테`를 사용했는데 바뀌었어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/8.png)

<br>
개인적으로, 적당히 단순하면서도 화려한 것으로 보여요. `GNOME`이나 `plasma`보다는 단순하고, `xfce`나 이후에 서술할 `MATE`, `LXDE` 보다는 화려한 적당한 위치.

### 설치 명령어
```
# pacman -S cinnamon
# pacman -S gnome-terminal    // 터미널 앱은 같이 설치되지 않으니, 별도로 설치
# pacman -S lightdm lightdm-gtk-greeter
# pacman -S xorg-server
# systemctl enable lightdm
```
<br>

### MATE (마테)

`그놈3`이 나오면서 `그놈2`의 개발이 끝났는데, `그놈3`이 마음에 안드는 사람들이 모여서 `그놈2`를 이어서 만들었어요. 그게 `마테`에요.
`마테나무`에서 따온 이름이기 때문에, `마테`라고 읽는 것이 맞아요. `마테나무`의 잎으로 만든 차가 `마테차`.

너무 옛날에 만든 것처럼 생겼는데,

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/9.png)

<br>
`마테`도 테마 적용이나 니것저것 해놓으면 괜찮게 생겼어요. `리눅스 민트` 중 마테를 사용하는 버전을 부팅한 모습

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/10.png)

### 설치 명령어
```
# pacman -S mate mate-extra    // mate-extra는 굳이 안깔아도 됨
# pacman -S lightdm lightdm-gtk-greeter
# pacman -S xorg-server
# systemctl enable lightdm
```
<br>

### LXDE

`LXDE`는 아주 많이 가벼워요. 그래서인지, 없어도 되는 것들은 다 빼버린 옛날 GUI를 보는 듯한 느낌도 들어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/11.png)

<br>
이건 `LXDE`를 사용한 `데비안`의 모습인데, 그래도 너무 옛날 디자인인 듯한 느낌이 드네요. 하지만 그만큼 가볍지요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/12.png)

### 설치 명령어
```
# pacman -S lxde lxdm
# systemctl enable lxdm
```
<br>

### LXQt

`LXQt`도 아주 많이 가벼워요. 없어도 것들은 다 빼버린 옛날 GUI를 보는 듯한 느낌도 들어요.
`LDXE`를 만든 사람이 `LXQt`도 만들었어요. `LXDE`는 `GTK2`로 만들었는데, 이후에 `Qt`로 다시 만든 것이 `LXQt`. `GTK3`가 나오면서 `GTK2`는 개발 중단되었기 때문.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/13.png)

<br>
물론, 이거도 나름 예쁘게 만들 수 있어요. `우분투`에서 `그놈` 대신 `LXQt`를 선택해서 만들어진 `루분투`. 사실 `루분투`는 옛날에 `LXDE`를 썼어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/14.png)


### 설치 명령어
```
# pacman -S lxqt sddm
# systemctl enable sddm
```
<br>

### COSMIC

`러스트`라는 프로그래밍 언어로 만들어진 데스크톱 환경이에요. `우분투` 기반으로 만들어진 `Pop!_OS`에서 기본 데스크톱 환경으로 사용해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/15.png)

### 설치 명령어

최소 설치만 원한다면 `cosmic` 대신 `cosmic-session`를 설치하세요. 대신 `디스플레이 매니저`는 알아서 설치해야 해요.
```
# pacman -S cosmic
# systemctl enable cosmic-greeter
```

<br>

### Deepin

2년 전에는 잘 설치가 되었는데, 지금은 오류가 나네요. 일단 명령어만 적어둘게요.

### 설치 명령어
```
# pacman -S deepin deepin-kwin deepin-extra
# pacman -S xorg-server
# systemctl enable lightdm
```
<br>


***

# 창 관리자 설치

## Fluxbox

`Fluxbox`는 `BlackBox`를 기반으로 만들어진 `창 관리자`에요. 테스크톱 환경이 아니에요.
물론 GUI 환경이라 이것저것 할 수 있긴 해요. 굳이 있을 필요가 없는 것들은 다 빼버린 듯한 모습이에요.
그래서 이렇게 아무것도 없는 것처럼 보이는데,

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/16.png)

<br>
배경에다가 마우스 오른쪽 클릭을 하면 메뉴가 나올거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/17.png)

### 설치 명령어 (디스플레이 매니저와 함께 사용)

```
# pacman -S fluxbox
# pacman -S lightdm lightdm-gtk-greeter
# pacman -S xorg-server
# systemctl enable lightdm
```

<br>
[디스플레이 매니저 없이 사용하고싶다면, 여길 참고해보세요](https://blog.naver.com/dt3141592/223882703180)


***

`데스크톱 환경`이나 `창 관리자`는 2개 이상 설치해서 사용할 수 있어요.
이렇게 어느 환경으로 들어갈지 로그인 화면에서 선택할 수 있구요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-desktop-experience/7.png)

<br>
물론 저건 이 글을 작성하기 위해 다 깔아봐서 그런거고, 저는 저런 짓은 하지 않아요.
