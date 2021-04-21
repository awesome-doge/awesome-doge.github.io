---
layout: post
title: URI, URL, URN
date: '2021-04-19 12:00:54 +0800'
---

![](https://i.imgur.com/YcdVaKb.png)
* URI = Uniform Resource Identifier 統一資源標誌符
* URL = Uniform Resource Locator 統一資源定位符
* URN = Uniform Resource Name 統一資源名稱

```
IRI is a superset of URI (IRI ⊃ URI)
URI is a superset of URL (URI ⊃ URL)
URI is a superset of URN (URI ⊃ URN)
URL and URN are disjoint (URL ∩ URN = ∅)
```
 
大白話，就是URI是抽象的定義，不管用什麼方法錶示，隻要能定位一個資源，就叫URI，本來設想的的使用兩種方法定位：
1. URL，用地址定位；
2. URN 用名稱定位。舉個例子：去村子找個具體的人（URI），如果用地址：某村多少號房子第幾間房的主人 就是URL， 如果用身份證號+名字 去找就是URN了。結果就是 目前WEB上就URL流行開了，平常見得URI 基本都是URL。

許多人知道URI是一種類似URL的東西，但是並不是真正知道URI和URL的關係，或者URI跟其他縮略詞IRI和URN之間的關係。

大多數人對URL(uniform resource locators)比較熟悉，如http://…, ftp://…, \mailto:…​:. 簡單來說URL錶示一個資源的地址。

URI(uniform resource identifier) 是一個URL或URN。因此要想完全理解URI，我們需要首先理解什麼是URN。

URN是uniform resource name 的縮寫。在世界上有許多“唯一標識符”模式，例如，ISBNs(globally unique for books)，social security numbers(國家範圍內唯一）,customer numbers(在一個公司的客戶數據庫中唯一) 以及 電話號碼。 每一個“唯一標識符”模式都有自己的編碼方式。URN是對各種不同“唯一標識符”模式的統一包裝。URN的文法是 urn:<scheme-name>:<unique-identifier>. 一個URN碼唯一標識了一個資源，如一本書、一個人或一臺設備。URN碼本身並不指定資源的地址。取而代之的，它假設有一個註冊器提供資源URN到它的地址的匹配關係。URN規範並冇有規定註冊器的格式，它可以是數據庫、可以是服務器應用、可以是一張圖錶或其他方便的任何東西。一些RUNs的假設示例有：urn:employee:08765245, urn:customer:uk:3458:hul8 and urn:foo:0000-0000-9E59-0000-5E-2。URN的<scheme-name>(示例中的employee、customer、foo)部分暗含了解析和解釋<unique-identifier>的方法。一個武斷的URN是冇有意義的，除非：(1) 你知道<scheme-name>暗含的語義， 並且(2) 你可以訪問<scheme-name>的註冊器。一個註冊器不一定是公開的或全球可訪問的。如 urn:employee:08765245 可能僅在某個特定的公司內有意義。

現在，URNs已經不像URLs那樣流行了，因此URI被廣泛的誤用為URL的同義詞。

IRI是internationalized resource identifier的縮寫。IRI是URI的國際化版本。特別的，一個URI包含US-ASCII字符集中的字母和數字，除此之外，IRI還包含歐洲字符、希臘字符、中文等。


參考文獻：

IRI, URI, URL, URN
* IRI, URI, URL, URN and their differences, https://fusion.cs.uni-jena.de/fusion/blog/2016/11/18/iri-uri-url-urn-and-their-differences/
* https://blog.csdn.net/ttyy1112/article/details/105216380
*  Internationalized Resource Identifiers (IRIs), https://tools.ietf.org/html/rfc3987

A Universally Unique IDentifier (UUID) URN Namespace
* https://tools.ietf.org/html/rfc4122

RDF
* RDF 1.1 Concepts and Abstract Syntax, https://www.w3.org/TR/rdf11-concepts/
* W3CHINA.ORG開放翻譯計畫（OTP）, http://zh.transwiki.org/cn/rdfprimer.htm

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
