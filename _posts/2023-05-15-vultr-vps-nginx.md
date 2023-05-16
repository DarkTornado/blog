---
layout: post
title: "우분투 서버에 nginx 설치 및 방화벽 설정 (Vultr VPS 사용)"
date: 2023-05-15 19:00:00 +0900
categories: blog
image: vultr-vps-nginx.jpg
description: "벌쳐에서 구매한 우분투가 설치된 VPS에 nginx 설치해서 이것저것하기"
---

[저번에 쓴 글]({{site.url}}{{site.baseurl}}/vultr-vps-start)에서 이어질거에요.

***

## ssh 접속 및 nginx 설치

일단 다음 명령어를 통해 서버에 원격으로 접속했어요. `fingerprint` 어쩌고 저쩌고 뜨면서 뭐라고 하면 일단 `yes` 입력하고 엔터치면 접속이 될거에요.
```
$ ssh root@{서버아이피주소}
//이후에 비밀번호 입력
```
![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/0.png)

<br>
서버 아이피랑 비밀번호는 같은건 저기에 나와있을거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/1.png)

<br>

비밀번호가 특수문자 떡칠되어있는 절대로 안뚫릴 것 같이 생긴게 불편한 관계로, 저는 원격 접속 후에 `passwd {사용자이름}` 명령어를 통해 비밀번호를 바꿨어요.

아무튼 아래 명령어를 통해 `nginx`를 설치했어요. 혹시라도 `nginx`를 못찾았다고 뜬다면, `sudo apt-get update`를 입력하신 뒤에 다시 아래 명령어를 입력해보세요.
```
$ sudo apt-get install nginx
```
![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/2.png)

<br>

뭐 재실행할꺼냐고 물어보는 것 같은데, 그냥 방향키였나 탭이였나 눌러서 `OK`로 커서 옮기고 엔터쳐서 넘겼어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/3.png)

<br>
그리고 이제 웹 브라우저에 VPS의 아이피 주소를 입력해보면 이런식으로 그런거 없다고 나올거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/4.png)

***

## 방화벽 열기

<br>
다음 명령어를 통해 방화벽에서 80번 포트를 열어주면
```
$ ufw allow 80
```
![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/5.png)

<br>
이런식으로 접속이 될거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/thumb/vultr-vps-nginx.jpg)

***

## sftp로 서버에 접속해서 서버에 파일 올리기

`FileZilla`라는 프로그램을 사용할거에요. [여기를 눌러서](https://filezilla-project.org/download.php) 다운로드 사이트로 이동하신 뒤에 능력것 다운로드하시고 설치해주세요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/6.png)

<br>
호스트에는 `sftp://root@서버아이피`, 사용자명에는 `root`, 비밀번호에는 비밀번호를 적으시고 연결하시면 될거에요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/7.png)

<br>
아무튼 전 접속이 되었어요.

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/8.jpg)

<br>
웹 브라우저를 통해 접속하면 `/var/www/html/` 폴더 안에 있는 파일들이 보여질거에요. 

아무튼 전 다음 내용을 `index.html` 파일로 저장한 뒤에, 저기다가 올렸어요.
```html
<html>

<head>
    <meta charset="utf-8">
    <title>끄어엄</title>
</head>

<body>
    끄어엄, 끄어어엄.
</body>

</html>
```
![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/9.png)


저 안에 보이는 `index.nginx-debian.html` 파일이 위에서 봤던 `Welcome to nginx!` 어쩌고에요.

<br>
아까 올린 파일이 잘 뜨네요

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/10.png)

***

일단 제 사이트가 검색 엔진에 뜨지 않게 하고 싶은지라, 다음 내용을 `robots.txt` 파일로 저장해서 같이 올려두었어요.
```
User-agent: *
Disallow: /
```

![image]({{site.url}}{{site.baseurl}}/assets/images/vultr-vps-nginx/11.png)
