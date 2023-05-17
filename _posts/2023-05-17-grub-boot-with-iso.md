---
layout: post
title: "grub에서 바로 .iso 파일 라이브 부팅하기"
date: 2023-05-17 11:00:00 +0900
categories: blog
image: grub-boot-with-iso.jpg
description: "grub 부팅 메뉴에 .iso 파일을 넣어두고 라이브 부팅하기"
---

리눅스 `.iso 파일` 파일을 리눅스 부트로더인 `grub`의 부트 메뉴에 추가해놓고, 그 `.iso 파일`을 통해 바로 라이브 부팅을 하도록 만들거에요.

그러니까, 예를 들면 이런식으로 `우분투 .iso 파일`의 경로 등을 적어서 `grub` 부팅 메뉴에 넣어두고,

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-boot-with-iso/0.jpg)

<br>
그걸 선택하면 이렇게 해당 .iso 파일을 통해 라이브 부팅이 되도록 만들거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-boot-with-iso/1.png)

***

## 우분투 및 공통 설명
```sh
menuentry "{메뉴에 보일 내용}" {
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile noprompt noeject
    initrd (loop)/casper/initrd
}
```

<br>
예를 들어, .iso 파일이 `/home/username/iso` 폴더 안에 있고, 파일 이름이 `ubuntu-22.04.2-desktop-amd64.iso`이며, 해당 리눅스가 첫 번째 디스크의 3번째 파티션에 있다면,

그리고 부트 메뉴에는 "Ubuntu Desktop 22.02.2 LTS Live"라는 이름으로 넣고 싶다면
```sh
menuentry "Ubuntu Desktop 22.02.2 LTS Live" {
    # rmmod tpm
    set isofile="/home/username/ubuntu-22.04.2-desktop-amd64.iso"
    loopback loop (hd0,gpt3)$isofile
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile noprompt noeject
    initrd (loop)/casper/initrd
}
```

<br>
같은 방식으로 적으면 될거에요. `(hd0,gpt3)` 같은건 알아서 잘 찾아보세요?
`grub`에서 `c` 키 눌러서 콘솔 창으로 나가서 ls 같은걸 치면 연결된 보조기억장치 및 파티션 목록이 저런식으로 뜰텐데, 아무튼 잘 찍어보시면 될거에요.

***
## 페도라

`Fedora-Workstation-Live-x86_64-38-1.6.iso` 파일이 기준이에요. 다른 파일을 사용하실거라면 능력것 버전명이나 그런거 보고 수정해보세요.
`Fedora Spin`에서 받은 `KDE` 버전 같은 다른 데스크톱 환경인 경우에도 `WS` 대신 `KDE`로 적는 등 수정할게 필요할거에요.
```sh
menuentry "{메뉴에 보일 내용}" {
    insmod ext2
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/images/pxeboot/vmlinuz root=live:CDLABEL=Fedora-WS-Live-38-1-6 rd.live.image verbose iso-scan/filename=$isofile
    initrd (loop)/images/pxeboot/initrd.img
}
```

***
## 칼리 리눅스

`kali-linux-2023.1-live-amd64.iso` 파일이 기준이에요.
```sh
menuentry "{메뉴에 보일 내용}" {
    insmod ext2
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/live/vmlinuz boot=live findiso=$isofile
    initrd (loop)/live/initrd.img
}
```

***
## 만자로 리눅스
`manjaro-kde-22.0.5-minimal-230316-linux61.iso` 파일이 기준이에요. 아치 계열 리눅스들도 다 이런식인지는 모르겠어요.
```sh
menuentry "{메뉴에 보일 내용}" {
    set isofile="{.iso 파일 경로}"
    set dri="free"
    search --no-floppy -f --set=root $isofile
    probe -u $root --set=abc
    set pqr="/dev/disk/by-uuid/$abc"
    loopback loop ({파티션})$isofile
    linux  (loop)/boot/vmlinuz-x86_64  img_dev=$pqr img_loop=$isofile driver=$dri copytoram
    initrd  (loop)/boot/intel_ucode.img (loop)/boot/initramfs-x86_64.img
}
```
<br>
가만 생각해보니, `chroot`용으로 아치도 넣어두면 편할 것 같긴 한데, 그러면 사실상 개나소나 제 컴퓨터를 root 권한을 가지고 사용할 수 있는거네요? 안해야지.

***
## 리눅스 민트 데비안 에디션 (LMDE)

`우분투`가 기반인 `리눅스 민트`가 아닌, `데비안` 기반인 `리눅스 민트 데비안 에디션` 이야기에요. `lmde-5-cinnamon-64bit.iso` 파일이 기준이에요.
```sh
menuentry "{메뉴에 보일 내용}" {
    insmod ext2
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/live/vmlinuz boot=live findiso=$isofile
    initrd (loop)/live/initrd.lz
}
```
<br>
분명 `우분투`가 기반인 `리눅스 민트`도 성공했던 기억이 있는데, 다시 시도해보니 안되네요.

***
## 하모니카
`hamonikr-taebaek-6.0-amd64-Lite.iso` 파일이 기준이고, 싸지방 등에 보이는 그 하모니카가 맞아요. `데비안`을 기반으로 하는 `우분투`를 기반으로 하는 `리눅스 민트`를 기반으로 하는 `하모니카`에요.
```sh
menuentry "{메뉴에 보일 내용}" {
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile noprompt noeject
    initrd (loop)/casper/initrd
}
```
***
## 티멕스 OS
개발사 측에서 독자 개발이라는 거짓말을 했지만, 사실은 `데바인` 기반이라 그런지 적을 내용은 `LMDE`랑 별 차이가 없어요. `TmaxOS-21-Beta.iso` 파일이 기준
```sh
menuentry "{메뉴에 보일 내용}" {
    set isofile="{.iso 파일 경로}"
    loopback loop ({파티션})$isofile
    linux (loop)/live/vmlinuz boot=live findiso=$isofile
    initrd (loop)/live/initrd.img
}
```
***
## 기타 추가 정보

위에서 적으라고 하는 것들은 `/etc/grub.d/` 폴더 안에 있는 `40_custom` 파일을 `root` 권한으로 열고 거기다가 적으시면 되는거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-boot-with-iso/2.png)

<br>
전 그냥 텍스트 편집기 앞에 `sudo`를 붙여서 실행했어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-boot-with-iso/3.png)

<br>
아무튼 수정하신 뒤에, `sudo update-grub`나 `sudo grub-mkconfig -o /boot/grub/grub.cfg` 등을 하시면, 이런식으로 적었던 내용들이 부트 메뉴에 추가될거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/grub-boot-with-iso.jpg)

<br>
전전 사진 속 처럼 `--class ubuntu`나 `--class fedora` 같은걸 적으면, 테마 적용시 아래 사진처럼 앞에 저런 아이콘이 나올거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/grub-boot-with-iso/4.jpg)

<br>
그리고, `/etc/grub.d/` 폴더 안에 있는 파일들 앞에 써있는 수 순서대로 실행되는 듯 해서 custom 파일 앞에 적힌 수를 적당히 바꿨더니 `UEFI Firmware Settings`보다 위에 메뉴가 추가되네요.