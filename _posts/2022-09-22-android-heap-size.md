---
layout: post
title: "안드로이드 힙 크기 변경"
date: 2022-09-22 10:00:00
categories: blog
image: android-heap-size.png
description: 안드로이드 힙 크기 바꾸기
---

`AndroidManifest.xml` 파일에 있는 `<application>` 안에다가
```xml
android:largeHeap="true"
```
을 추가해주면 된다.