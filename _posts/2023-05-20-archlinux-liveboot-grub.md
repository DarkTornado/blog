---
layout: post
title: "grub에서 바로 .iso 파일로 아치 리눅스 라이브 부팅하기"
date: 2023-05-20 20:00:00 +0900
categories: blog
image: archlinux-liveboot-grub.png
description: "grub에 아치 리눅스 .iso 파일로 라이브 부팅하는 메뉴 추가하기"
---

`/etc/grub.d/40_custom` 파일을 열고, 다음 내용을 아래에 적으면 되는거에요.
```sh
menuentry '{grub에서 보일 문구}' --class arch {
    insmod ext2
    set isofile='{.iso 파일 경로}'
    loopback loop ({.iso 파일이 있는 파티션})$isofile
    linux (loop)/arch/boot/x86_64/vmlinuz-linux archisolabel={.iso 파일 마운트하면 보이는 이름} img_dev={.iso 파일이 있는 파티션} img_loop=$isofile earlymodules=loop
    initrd (loop)/arch/boot/intel-ucode.img (loop)/arch/boot/amd-ucode.img (loop)/arch/boot/x86_64/initramfs-linux.img
}
```
<br>

- `{grub에서 보일 문구}`에는 말 그대로 부팅하면 나오는 `grub` 메뉴에서 보일 내용을 적으면 되는거에요.
- `set isofile='{.iso 파일 경로}'`에도 .iso 파일의 위치를 적으면 되구요.
- `archisolabel={.iso 파일 마운트하면 보이는 이름}`에는 `.iso 파일`을 마운트하면 나오는 이름을 적으면 되는데, 예를 들어 아래 사진의 경우는, `ARCH_202303`으로 적으면 되는거에요.
![image]({{site.url}}{{site.baseurl}}/assets/images/archlinux-liveboot-grub/0.png)

- `loopback loop ({.iso 파일이 있는 파티션})$isofile`에서의 파티션은 `(hd0.gpt3)` 같은 형식으로 적으면 되고, `img_dev={.iso 파일이 있는 파티션}`에서의 파티션은 `/dev/sda3` 같은 형식으로적으면 되는거에요. 저같은 경우는 관심법과 `lsblk`로 확인해보니 각각 `(hd0.gpt4)`과 `/dev/nvme0n1p4`로 적으면 될 듯 해요.
![image]({{site.url}}{{site.baseurl}}/assets/images/archlinux-liveboot-grub/1.png)

<br>
일단 전 이런식으로 적었고,

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/archlinux-liveboot-grub.png)

<br>
이제 `update-grub` 같은걸 하면,
```sh
$ sudo update grub
//또는
$ sudo grub-mkconfig -o /boot/grub/grub.cfg
```

<br>
이런식으로 SSD 등에 넣어둔 아치 리눅스 .iso 파일로 라이브 부팅하는 메뉴가 `grub`에 추가될거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/archlinux-liveboot-grub/2.jpg)

<br>
잘 되네요.

![image]({{site.url}}{{site.baseurl}}/assets/images/archlinux-liveboot-grub/3.jpg)

<br>
다른 리눅스들도 추가하고 싶으시다면 [다음 게시글]({{site.url}}{{site.baseurl}}/grub-boot-with-iso/)을 참고해보세요.

이런식으로 아치리눅스로 라이브 부팅이 가능하게 해놓으면, 개나소나 `arch-chroot`를 통해 `root` 권한을 가진 상태로 본인의 PC를 사용할 수 있게 된다는 뜻이기도 하니, [이 게시글]({{site.url}}{{site.baseurl}}/grub-menuentry-password/)을 슬쩍 컨닝하면서 능력것 막아보세요.
