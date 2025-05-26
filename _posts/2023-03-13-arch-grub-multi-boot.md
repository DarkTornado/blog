---
layout: post
title: "아치 리눅스랑 같이 깔려있는 OS 인식시키기"
date: 2023-03-13 01:00:00
categories: blog
image: arch-grub-multi-boot.png
description: 아치 리눅스랑 멀티부팅으로 같이 깔려있는 운영제체를 grub가 못찾을 때 인식시키기"
---

### 같이 깔려있는 운영체제 찾게 만들기

분명 윈도우 + 아치리눅스 조합으로 듀얼부팅을 해두었는데, 아무리 `grub-mkconfig -o /boot/grub/grub.cfg`를 해도 저 메뉴에 나오지를 않는단 말이죠?

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/0.png)

<br>

그럴 때는 우선 `os-prober`를 설치하시고 (물론 전 아치리눅스 최초 설치 시점에 같이 깔았어요)
```
$ sudo pacman -S os-prober
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/1.png)

<br>

`usr/bin/grub-mkconfig` 파일을 열어주세요.
```
$ sudo vim /usr/bin/grub-mkconfig
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/2.png)


<br>
내려보면

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/3.png)


<br>

`GRUB_DISABLE_OS_PROBER="true"`라고 적힌게 보일텐데

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/4.png)

<br>

저걸 "false"로 바꿔주세요.
```
GRUB_DISABLE_OS_PROBER="false"
```


<br>

그리고나서 저장하신 뒤에 `grub-mkconfig -o /boot/grub/grub.cfg`를 다시 하시면 윈도우를 잘 찾아올거에요.
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/5.png)

<br>

짠. 윈도우가 잘 나오긴 했어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/6.png)

***

### 윈도우는 찾지만 리눅스는 못찾는 경우

근데, 윈도우 + 페도라 + 아치 리눅스 조합으로 설치해봤는데, 그때는 윈도우는 아주 잘 찾아오면서 페도라는 못찾더라구요?

그건 그냥 페도라가 설치되어 있는 파티션을 마운트시키면 알아서 찾아더라구요.

아래 사진에서 파란색 네모는 페도라를 설치해둔 파티션을 마운트하기 전에 `grub-mkconfig -o /boot/grub/grub.cfg` 한건데, 페도라가 안떠요. 
하지만 마운트한 이후에 다시 하면 빨간색으로 밑줄을 쳐놓은 부분을 보시면 알 수 있듯이 페도라도 잘 찾아와요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/7.png)

<br>

아치 리눅스, 윈도우, 페도라 3개 모두 잘 뜨는 것을 확인할 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-grub-multi-boot/8.png)
