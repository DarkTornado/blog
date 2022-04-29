---
layout: post
title: "디스크 파티션 분할하기"
date: 2021-12-01 21:00:00
categories: blog
image: disk-partition.jpg
description: 윈도우에서 디스크 파티션 분할하기
---

왼쪽 아래에 있는 윈도우 로고 우클릭한 다음에 `디스크 관리` 클릭

![image](https://darktornado.github.io/blog/assets/images/disk-partition/0.jpg)

<br>

그러면 이런식으로 디스크들이 뜰텐데,

![image](https://darktornado.github.io/blog/assets/images/disk-partition/1.jpg)

<br>

용량을 줄일 파티션에다가 대고 우클린한 다음에 `볼륨 축소` 클릭. 해당 기능은 아마 NTFS 파일 시스템을 사용하는 파티션에만 할 수 있을거에요.

![image](https://darktornado.github.io/blog/assets/images/thumb/disk-partition.jpg)

<br>

잠시 기다리면

![image](https://darktornado.github.io/blog/assets/images/disk-partition/2.jpg)

<br>

나오는 화면에서 얼마나 출일지 입력

![image](https://darktornado.github.io/blog/assets/images/disk-partition/3.jpg)

<br>

단위는 MB라고 써있지만 실제로는 MiB니까 참고해주세요. 일단 전 8GiB로 했어요. `1GB = 1000MB`이고 `1GiB = 1024MiB`인데, 윈도우에서는 1024로 나눠놓고 사이에 i 생략해서 보여줘요.

![image](https://darktornado.github.io/blog/assets/images/disk-partition/4.jpg)

<br>

끝!

![image](https://darktornado.github.io/blog/assets/images/disk-partition/5.jpg)

<br>

이동할 수 없는 파일 어쩌고저쩌고 하면서 용량이 충분해도 조금밖에 못줄이는 경우는, 중간에 가상메모리 파일이나 시스템 백업 시점 같은 이동할 수 없는 파일이 끼어있는 것이니, 관련 기능을 잠시 꺼두고 나누면 됩니당.
