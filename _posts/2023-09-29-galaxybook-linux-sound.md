---
layout: post
title: "갤럭시북에서 리눅스 부팅시 소리 안나는거 해결 (삼성 노트북)"
date: 2023-09-29 15:00:00 +0900
categories: blog
image: galaxybook-linux-sound.png
description: "갤럭시북 Flex, Flex2 5G, 이온 / 아치, 만자로, 우분투"
---

아치 리눅스, 만자로 리눅스, 우분투에서 성공한 방법이에요.
[이 게시글](https://forum.manjaro.org/t/howto-set-up-the-audio-card-in-samsung-galaxy-book/37090)을 적당히 따라했더니 작동했어요.
- 성공해본 노트북 : 갤럭시북 Flex2 5G
- 성공 사례가 있는 노트북 : 갤럭시북 Flex, 갤럭시북 이온


일단 `sof-firmware`를 설치해야 해요. 만자로와 우분투에서는 아래 사진처럼 잘 뜨는 것을 보면 이미 깔려있는 것 같아요.
아치같은 경우는 `Dummy Output`으로 떠요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/galaxybook-linux-sound.png)

<br>

아무튼 아치 계열 리눅스에서는 다음 명령어를 통해 설치할 수 있어요.
```sh
$ sudo pacman -S sof-firmware
```
![image]({{site.url}}{{site.baseurl}}/assets/images/galaxybook-linux-sound/0.png)

<br>

`hda-verb`를 사용할건데, 그게 `alsa-tools`에 있을거에요. 따라서 다음 명령어를 통해 `alsa-tools`를 설치해야 해요.
```sh
$ sudo pacman -S alsa-tools //아치리눅스, 만자로리눅스

$ sudo apt-get -y install alsa-tools //우분투
```
![image]({{site.url}}{{site.baseurl}}/assets/images/galaxybook-linux-sound/1.png)

<br>

[여기를 누르면 나오는 내용](https://pastebin.com/raw/zsXp2vz6)을 `TO912.sh` 파일로 저장하고 실행하면 소리가 날거에요.
실행 권한은 `chmod` 명령어를 통해 능력것 부여하시면 될거에요.
```sh
$ ./TO912.sh
```
![image]({{site.url}}{{site.baseurl}}/assets/images/galaxybook-linux-sound/2.png)

<br>

다 따라한건 아닌데, 저 정도만 따라해도 소리는 나오더라구요. 이어폰에서도 나오고 스피커에서도 나와요.
재부팅시 저 배치파일 자동 실행 같은거 어케어케 잘 선택하면 될 듯.

그리고 아치위키에 `갤럭시북 Flex2 5G`는 내장 스피커가 켜지지 않는다는 내용이 있는데, 소리가 아주 잘 나오고 있어요.