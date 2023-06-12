---
layout: post
title: "linode 더 낮은 요금제로 바꾸기"
date: 2023-06-12 00:23:00 +0900
categories: blog
image: linode-change-plan.png
description: "linode 더 낮은 요금제로 바꾸기 + 디스크 용량 줄이기"
---

리노드에서 [2023년 4월 1일부터 Dedicated CPU 플랜과, nanode를 제외한 Shared CPU 플랜들의 가격이 인상](https://www.linode.com/blog/linode/akamai_cloud_computing_price_update/)되었어요.
그런고로, 기존에 사용하던 요금제보다 더 낮은걸로 바꿔볼거에요.

새로 VPS를 만들고 내용물을 거기로 옮겨야 하나 생각하고 있었는데, 그냥 요금제를 바꾸는 기능이 있더라구요.

||CPU|RAM|디스크|가격|
|:--:|:--:|:--:|:--:|:--:|
|기존|2|4GB|80GB|$ 36|
|변경|1|2GB|50GB|$ 12|

이니까, 일단 디스크 용량을 `30GB` 정도 줄어야 해요. `df -h` 명령어를 통해 여유공간을 확인할 수 있어요.
전 `80GB` 중 `10GB` 정도를 사용하고 있으니, 그냥 줄여도 될 것 같아요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/0.png)

<br>
디스크 용량을 줄일꺼면 우선 서버를 꺼야 해요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/1.png)

<br>
쇽

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/2.png)

<br>
`Storage` 탭에서 용량을 조절하려는 디스크의 `Resize` 문구 클릭

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/3.png)

<br>
`81408`이라는 수치는 `80 × 1024 - 512`를 한 결과에요. 스왑 파티션이 `512MB`를 먹고 있네요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/4.png)

<br>
`50GB`로 줄일 예정인지라 `50 × 1025 - 512`인 `50688MB`로 적었어요.

여기도 1024로 나눠놓고 십진 접두어를 사용하는 만?행을 저지르고 있네요.
원래는 `1GB = 1000MB`, `1GiB = 1024MiB`가 맞아요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/5.png)

<br>
오른쪽 아래에 디스크 줄이기가 시작되었다고 뜨고,

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/6.png)

<br>
원래 용량이 적혀있던 곳에서 진행 정도를 볼 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/7.png)

<br>
끝

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/8.jpg)

<br>
이제 오른쪽 상단에 있는 다른 메뉴들이 담겨있을 것 같은 버튼을 누르고 `Resize` 버튼을 누르면

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/linode-change-plan.png)

<br>
요금제를 변경할 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/9.png)

<br>
어느 요금제로 바꿀지 선택하고

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/10.png)

<br>
VPS의 `label`을 저기다가 적고 `Resize Linode` 버튼을 누르면

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/11.png)

<br>
바꾸는게 시작되었다는 알림이 오른쪽 아래에 출력될꺼에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/12.jpg)

<br>
`RESIZING`이라고 써있네요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/13.jpg)

<br>
진행 정도와 남은 시간은 알림이 뜨는 창에서 볼 수 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/14.jpg)

<br>
끝

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/15.png)

<br>
이제 서버를 키시면 됩니당

![image]({{site.url}}{{site.baseurl}}/assets/images/linode-change-plan/16.png)
