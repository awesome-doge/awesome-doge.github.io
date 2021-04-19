---
layout: post
title: URI, URL, URN
date: '2021-04-19 12:00:54 +0800'
---

![](https://i.imgur.com/YcdVaKb.png)
* URI = Uniform Resource Identifier 统一资源标志符
* URL = Uniform Resource Locator 统一资源定位符
* URN = Uniform Resource Name 统一资源名称

```
IRI is a superset of URI (IRI ⊃ URI)
URI is a superset of URL (URI ⊃ URL)
URI is a superset of URN (URI ⊃ URN)
URL and URN are disjoint (URL ∩ URN = ∅)
```
 
大白话，就是URI是抽象的定义，不管用什么方法表示，只要能定位一个资源，就叫URI，本来设想的的使用两种方法定位：
1. URL，用地址定位；
2. URN 用名称定位。举个例子：去村子找个具体的人（URI），如果用地址：某村多少号房子第几间房的主人 就是URL， 如果用身份证号+名字 去找就是URN了。结果就是 目前WEB上就URL流行开了，平常见得URI 基本都是URL。
