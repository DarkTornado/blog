---
layout: post
title: "아치 리눅스 설치 (멀티 부팅)"
date: 2023-03-17 01:00:00
categories: blog
image: arch-multi-boot.png
description: "멀티 부팅으로 아치 리눅스 설치하기 + 시나몬"
---

사실 아치 리눅스를 다시 설치하는 미래의 나를 위해서 작성해두는 글일지도 몰라요.
[English Post](https://darktornado.github.io/archlinux-multiboot/)

***

## 기존 파티션 용량 줄이기

아치 리눅스를 설치할 생각을 하고 있을 정도인 사람이라면 이 정도는 당연히 할 줄 알거라고 믿어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/0.png)

***

## .iso 파일 다운로드 및 부팅 USB 만들기

그냥 [아치 리눅스 홈페이지](https://archlinux.org/download/)에 들어가서 토렌트로 받으면 되는거에요.
불법 공유 때문에 토렌트 이미지가 나락으로 가있긴 하지만, 여기서는 공식 배포가 토렌트인걸

***

## 라이브 부팅

가장 위에걸 고르면 된다는건 당연히 알겠지

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/1.png)

<br>
아무튼 부팅이 끝났어요. GUI 따위는 없어요. 인스톨러 따위도 없어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/2.png)

<br>
`date` 명령어 같은거 확인해서 시간이 잘 맞나 확인해보라는 말을 들었던 적이 있어요

***

## 인터넷 연결

유선 인터넷을 사용하시거나 가상머신에 설치중이시라면 인터넷 연결은 알아서 되어있을거에요.
인터넷 연결은 대충 구글에 `ping` 요청 넣어보면 되는거에요.

분명 미래의 나는 와이파이 정도만 가능 사용할 수 있는 노트북을 사용하고 있을거에요.
그러니 `iwctl`을 통해 와이파이에 연결을 해야해요.

```
# iwctl
```

<br>
아햏햏

```
# device list     //컴퓨터에 있는 네트워트 인터페이스 찾기
# station {인터페이스} scan     //주변 와이파이 검색
```

<br>
저거 입력 후 잠시 대기. 와이파이 검색하라고 시킨거고 사실 2초 정도만 기다려도 될거에요.

```
# station {인터페이스} get-networks     //주변 와이파이 목록 출력
# station {인터페이스} connect "와이파이 이름"     //해당 와이파이에 연결
```

<br>
비밀번호가 걸려있는 와이파이라면 이후에 비밀번호를 입력하면 됩니당
다 끝났으면 `iwctl` 밖으로 탈출

```
# exit
```

***

## 파티션 생성 및 마운트

`lsblk` 명령어로 확인해보니 <s>사실 여기서는 가상 디스크지만,</s> SSD는 `nvme0n1`인듯 해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/3.png)


<br>
```
# cfdisk {디스크}
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/4.png)

<br>
아까 윈도우에서 줄였던 공간 선택 후 `New` 선택 후 엔터. 파티션 선택하는건 상/하 방향키, 아래 New, Quit 같은 메뉴는 좌/우 방향키로 이동할 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/5.png)

<br>
용량은 이미 알아서 최대로 입력되어 있을거니까 엔터

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/6.png)

<br>
`Write`를 선택헤서 수정사항 반영

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/7.png)

<br>
잘못 건들면 원래 있던거 날려먹을 수 있으니, 다시 한 번 더 확인해보고 제대로 고른게 맞다면 `yes` 입력 후 엔터

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/8.png)

<br>
그리고 `Quit` 골라서 나오면 됩니당

`lsblk -f` 명령어 등을 통해 어떤게 어느 파티션인지 잘 알아오시고나서 마운트
```
# mount /dev/{아치 리눅스 설치할 파티션} /mnt
# mkdir -p /mnt/boot/efi
# mount /dev/{EFI 파티션} /mnt/boot
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/9.png)

***

## 아치 리눅스 설치

```
# pacstrap /mnt base base-devel linux linux-firmware vim
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/10.png)

<br>
`fstab`도 생성해줘요.

```
# genfstab -U /mnt >> /mnt/etc/fstab
```

<br>
아무튼 아치 리눅스 설치만 끝났어요.

***

## chroot 실행

아마 터미널 왼쪽에 적힌 계정 이름이나 경로같은게 머시기가 바뀔거에요.
```
# arch-chroot /mnt
```

***

## root 계정 비밀번호 설정 및 사용자 추가

검색하면 나오는 정보인 `root 계정`의 비밀번호는 기본적으로 `root`로 설정되어있다는 내용은 그짓말이니 믿지 마시고, 저처럼 미리 비밀번호 설정해두세요.
안그러면 또 라이브 부팅해서 `chroot`로 들어와야 해요.
```
# passwd root     //이후에 비밀번호 입력
# useradd {유저이름}
# passwd {유저이름}     //이후에 비밀번호 입력
```

<br>
물론, `sudo`가 가능한 계정을 만들어두고, `root 계정` 자체를 안쓰는 방법도 있어요.

***

## 부트로더 설치

```
# pacman -S grub efibootmgr dosfstools openssh os-prober mtools
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={부팅 메뉴에 보일 이름}
# grub-mkconfig -o /boot/grub/grub.cfg
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/11.png)

***

## 시나몬 설치

전 시나몬을 사용할거에요. 굳이 시나몬을 설치하실 필요는 없으니, 원하시는 데스크톱 환경으로 설치하시면 되는거에요.

```
# pacman -S cinnamon     //시나몬 설치
# pacman -S gnome-terminal     //터미널은 안깔리니 터미널 따로 설치
# pacman -S xorg-server lightdm lightdm-gtk-greeter     //아무튼 필요한거 설치
# mkdir /home/{계정이름}     //폴더 미리 안만들어두면 GUI에서 로그인하는 순간 오류뜸
# chmod 777 /home/{계정이름}     //만들기만 하면 권한 부족해서 또 오류뜸
systemctl enable lightdm     //재부팅시 GUI 자동 실행. 종종 자동으로 켜지게 하면 오류 안뜨고 수동으로 키면 오류나는 환경들이 있어요.
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/12.png)

<br>
아무튼 위에 저 시나몬이랑 이것저것 다 설치하면 `800 ~ 900 MiB` 정도 먹을거에요.

***

## NetworkManager 설치

이거 안해두면 재부팅했을 때 인터넷이 안될거에요.

```
# pacman -S networkmanager
# systemctl enable NetworkManager     //대/소문자 구분 필요
```

***

## 재부팅

```
# exit     //chroot 종료
# reboot     //재부팅
```

<br>
와! 재부팅을 해보니 `grub`가 나와요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/13.png)

<br>
저거 배경 시커먼건 배경화면이 없어서 그래요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/14.png)

<br>
아무튼 아치 리눅스 및 시나몬 설치가 끝났어요!

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/15.png)

***

## 이것저것 필요한거 설치 및 설정

미래의 내가 `sudo` 가능한 계정을 만들어주겠지. 귀찮으니 `root 계정`으로 접속

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/16.png)

<br>

로케일 설정을 할거에요.
`/etc/locale.gen` 파일을 열어서 `en_US.UTF-8`랑 `ko_KR.UTF-8` 앞에 있는 주석(`#`) 삭제

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/17.png)

<br>
수정을 했다면 저장 후 다음 명령어 실행

```
# locale-gen
```

<br>
그리고 한글 관련된 이것저것 설치

```
# pacman -S noto-fonts-cjk     //한글 폰트
# pacman -S ibus ibus-hangul     //한글 입력기
```

<br>
부팅 시 `ibus` 자동 실행은 미래의 내가 해주겠지. 지금은 그냥 부팅 시마다 수동으로 키고 있어요.

***

## 같이 깔려있는 운영체제들 grub에 추가

`/usr/bin/grub-mkconfig` 파일을 열어서 저 부분을 false로 수정
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/18.png)

<br>
이렇게

```
GRUB_DISABLE_OS_PROBER="false"
```

<br>
그리고 `grub-mkconfig -o /boot/grub/grub.cfg`를 해서 수정사항 반영.
같이 깔려있는 윈도우는 잘 찾고 다른 리눅스는 못찾는다면, 리눅스가 설치되어 있는 파티션을 마운트하면 될거에요.
마운트하면 잘 찾는데, 마운트 안하면 못찾더라구요.

```
grub-mkconfig -o /boot/grub/grub.cfg
```
![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/19.png)

***

### 기타 잡 정보

`Ctrl + Alr + F1`나 `Ctrl + Alr + F2` 같은 단축키 사용시 CLI 환경으로 나갈 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/arch-multi-boot/20.png)
