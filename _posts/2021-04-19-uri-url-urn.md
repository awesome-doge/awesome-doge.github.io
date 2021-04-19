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

许多人知道URI是一种类似URL的东西，但是并不是真正知道URI和URL的关系，或者URI跟其他缩略词IRI和URN之间的关系。

大多数人对URL(uniform resource locators)比较熟悉，如http://…, ftp://…, \mailto:…​:. 简单来说URL表示一个资源的地址。

URI(uniform resource identifier) 是一个URL或URN。因此要想完全理解URI，我们需要首先理解什么是URN。

URN是uniform resource name 的缩写。在世界上有许多“唯一标识符”模式，例如，ISBNs(globally unique for books)，social security numbers(国家范围内唯一）,customer numbers(在一个公司的客户数据库中唯一) 以及 电话号码。 每一个“唯一标识符”模式都有自己的编码方式。URN是对各种不同“唯一标识符”模式的统一包装。URN的语法是 urn:<scheme-name>:<unique-identifier>. 一个URN码唯一标识了一个资源，如一本书、一个人或一台设备。URN码本身并不指定资源的地址。取而代之的，它假设有一个注册器提供资源URN到它的地址的匹配关系。URN规范并没有规定注册器的格式，它可以是数据库、可以是服务器应用、可以是一张图表或其他方便的任何东西。一些RUNs的假设示例有：urn:employee:08765245, urn:customer:uk:3458:hul8 and urn:foo:0000-0000-9E59-0000-5E-2。URN的<scheme-name>(示例中的employee、customer、foo)部分暗含了解析和解释<unique-identifier>的方法。一个武断的URN是没有意义的，除非：(1) 你知道<scheme-name>暗含的语义， 并且(2) 你可以访问<scheme-name>的注册器。一个注册器不一定是公开的或全球可访问的。如 urn:employee:08765245 可能仅在某个特定的公司内有意义。

现在，URNs已经不像URLs那样流行了，因此URI被广泛的误用为URL的同义词。

IRI是internationalized resource identifier的缩写。IRI是URI的国际化版本。特别的，一个URI包含US-ASCII字符集中的字母和数字，除此之外，IRI还包含欧洲字符、希腊字符、中文等。


參考文獻：

IRI, URI, URL, URN
* IRI, URI, URL, URN and their differences, https://fusion.cs.uni-jena.de/fusion/blog/2016/11/18/iri-uri-url-urn-and-their-differences/
* https://blog.csdn.net/ttyy1112/article/details/105216380
*  Internationalized Resource Identifiers (IRIs), https://tools.ietf.org/html/rfc3987

RDF
* RDF 1.1 Concepts and Abstract Syntax, https://www.w3.org/TR/rdf11-concepts/
* W3CHINA.ORG开放翻译计划（OTP）, http://zh.transwiki.org/cn/rdfprimer.htm

Json-LD
* https://www.slideshare.net/gkellogg1/favorites
* https://www.slideshare.net/gkellogg1/presentations
* https://json-ld.org/learn.html
* https://www.w3.org/TR/json-ld11/


HTTPRange-14
* https://en.wikipedia.org/wiki/HTTPRange-14

LinkedData
* https://www.w3.org/wiki/LinkedData

NFT Use case
* https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-002.md

#### NFT Metadata Layer Model
| Layer |  |
|-----|------|
| **8. Operationalization** | At ticketing, Vicki and Stephen each present a QR code representing their ticket to a scanner in the theatre lobby. Lights illuminate a path to their seats and the tickets are recorded as used. |
| **7. Assertions** | TicketAdvisor claims performances through the month of December 15 will have a cameo by Lin-Manual Miranda. [??? is this part of this scenario or is there a better assertion] | 
| **6. Extensions &    Restrictions to Rights** | Seats changed to B16 and B18. Seat changes after December 14 at 8PM are no longer allowed. | 
| **5. Instantiation** | Two tickets to see Phantom of the Opera at 8 PM on December 15, 2020, seats D24 and D26, respectively. (Two separate tokens) |  
| **4. Embodied Rights** | Theatre Ticket: Right to attend and be seated at a particular performance, at a particular venue, at a particular time. Seats are changeable if alternative seats are available. |
| **3. Token Logic** | Resellable Bearer token | 
| **2. Interchain** | Atomic transactions guarantee all transfers happen simultaneously: payment to Ellenor, transfer of ticket to Stephen, and change of both seats | 
| **1. State Machine** | Stephen pays Ellenor via bitcoin. Ticketing is on Ticket Chain, Payments are on MoneyChain (which has fiat onramps / offramps) |
