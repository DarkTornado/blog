---
layout: post
title: "윈도우를 설치한 VHD가 갑자기 최대 용량이 되었을 때"
date: 2023-10-12 20:00:00 +0900
categories: blog
image: window-vhd-max.png
description: "용량을 다 채운 것도 아닌데 갑자기 최대 용량까지 증가해버린 경우 원래 용량으로 되돌리기"
---

VHD에 설치한 윈도우에서 분명 `시스템 종료`를 눌렀는데 지맘대로 업데이트를 시작하는게 너무 화가 나서 강제종료를 해버렸더니, 용량이 최대치로 늘어나버렸어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/window-vhd-max.png)

<br>
최대 용량을 `64GiB`로 했는데, 그거 다 채운 것도 아닌데 저러고 있어요.


그냥 VHD 안에 있는 윈도우로 부팅했다가 다시 밖에 있는(?) 윈도우로 부팅하면 용량이 정상적으로 돌아와요.

![image]({{site.url}}{{site.baseurl}}/assets/images/window-vhd-max/0.png)
