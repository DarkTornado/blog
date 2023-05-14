---
layout: post
title: "Vultr 회원가입 및 VPS 구매"
date: 2023-05-13 15:00:00 +0900
categories: blog
image: vultr-vps-start.png
description: "벌쳐에서 VPS 구매하기"
---

백업 서버를 구축하기 위해, `Vultr(벌쳐)`에서 VPS를 하나 샀어요.

이미 벌쳐를 사용중인 제 지인에게 초대 링크를 받아서 가입했어요. 초대 링크로 들어가면 저런식으로 메인 화면으로 가질텐데 원래 그게 정상이에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/0.png)

<br>
링크를 준 사람과 그 링크를 받아서 가입한 사람한테 크레딧을 주는데, 가입한 사람에게는 $100 정도 주는걸로 기억하는데, $250네요?
어차피 저거 유효기간 30일인걸로 알고있긴 한데,

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/1.png)

<br>
아무튼 이메일로 온거 들어가서 계정 활성화도 하고,

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/2.png)

<br>
카드 등록도 했어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/3.png)

<br>
`I just want to link my credit card -$0.00 deposit`를 체크해야 굳이 나갈 필요가 없는 돈이 안나가요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/4.png)

<br>
`Product` 탭에 들어가서

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/5.png)

<br>
화면 오른쪽에 있는 `+` 버튼을 누르면, 서버를 추가할 수 있어요.
`Deploy New Server`를 누르면 되는거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/6.png)

<br>
이것저것 뭐가 많이 있는데, 전 `Cloud Compute`에 있는 `AMD High Performance` 중 가장 싼 $6짜리 요금제를 골랐어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/vultr-vps-start.png)

<br>
가장 가격이 낮은 요금제는 한국 리전에서는 사용할 수 없고, 운영제체로 우분투를 사용할꺼면 램이 최소 1GB는 필요해서, 최소한 $5짜리는 써야하는데, 그럴꺼면 1달러 더 추가해서 더 좋은 CPU를 쓰고 말지요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/7.png)

<br>
전 백업은 딱히 없어도 되고, 어차피 저기서 해주는 디도스 방어는 무의미하다는 주변에 있는 사악한 아죠씨의 조언도 있고 하니 그냥 다 체크 해제.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/8.png)

<br>
아무튼 만들었어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/9.png)

<br>
히히 서버당

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/10.png)

<br>
일단 ping 요청에는 잘 응답하고 있어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-start/11.png)
