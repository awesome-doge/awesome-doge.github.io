---
layout: post
title: NFT Design
date: '2021-04-20 16:12:59 +0800'
---

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421175124.png)

- [數據描述的方法](#數據描述的方法)
- [DID 重要文獻](#did-重要文獻)
- [DID 工具包 spruceid](#did-工具包-spruceid)
- [DID 架構定位](#did-架構定位)
  - [會議論文](#會議論文)
  - [黑客松作品](#黑客松作品)
  - [btcr](#btcr)
  - [Use Case](#use-case)
- [代幣分類架構圖](#代幣分類架構圖)
- [Claims](#claims)
- [系統設計與實現](#系統設計與實現)


---

## 數據描述的方法

* RDF (xml base)
  > 參考文獻
  > * [維基百科](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%BA%90%E6%8F%8F%E8%BF%B0%E6%A1%86%E6%9E%B6)
  > * [w3c 中文](http://zh.transwiki.org/cn/rdfprimer.htm)

* IRI (Json base)
  * URI
    * URL
    * URN
      * UUID
      * DID
        * IID

---

## DID 重要文獻
* [w3c.github.io/did-core](https://w3c.github.io/did-core/)
* [w3.org/TR/vc-data-model](https://www.w3.org/TR/vc-data-model/)
* [w3.org/TR/2021/NOTE-did-spec-registries-20210409/#blockchainaccountid](https://www.w3.org/TR/2021/NOTE-did-spec-registries-20210409/#blockchainaccountid)
* [w3c-ccg.github.io/did-primer](https://w3c-ccg.github.io/did-primer/)
* [w3.org/TR/2021/NOTE-did-use-cases-20210317/](https://www.w3.org/TR/2021/NOTE-did-use-cases-20210317/)
    > ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421112756.png)
    ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421112830.png)
    ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421112857.png)
    ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421112916.png)
    ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421112936.png)
* [DID 去中心化數字身份](https://www.chainnews.com/zh-hant/articles/855126602963.htm)
* [did.baidu](https://did.baidu.com/did-concepts/)
  > ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165145.png)j![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165103.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165445.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165641.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165721.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421165827.png)
* [告別網路個資外洩-去中心化分散式身份識別 W3C Decentralized Identifiers (DIDs)技術探討](https://www.syscom.com.tw/ePaper_New_Content.aspx?id=784&EPID=271&TableName=sgEPArticle)

**其他**
- [w3c-ccg.github.io/amira/](https://w3c-ccg.github.io/amira/)
- [en.bitcoin.it/wiki/BIP_0136](https://en.bitcoin.it/wiki/BIP_0136)
- [w3schools.com/tags/tag_link.asp](https://www.w3schools.com/tags/tag_link.asp)
- [w3schools.com/html/html_links.asp](https://www.w3schools.com/html/html_links.asp)
- [hackmd.io/5c0ksa5sRBW9EwtRbJeiag](https://hackmd.io/5c0ksa5sRBW9EwtRbJeiag)
- [wiki/HTTPRange-14](https://en.wikipedia.org/wiki/HTTPRange-14)
- [wiki/Resource_Description_Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework)
- [wiki/Turtle_(syntax)](https://en.wikipedia.org/wiki/Turtle_(syntax))

ERC725/735 identities
* [ERC725Alliance/ERC725/blob/master/docs/use-cases.md](https://github.com/ERC725Alliance/ERC725/blob/master/docs/use-cases.md)
* [ethereum/eips/issues/735](https://github.com/ethereum/eips/issues/735)
* [https://eth.wiki/ideas/erc-735](https://eth.wiki/ideas/erc-735)

## DID 工具包 spruceid
- [spruceid](https://github.com/spruceid/)
- [docs/](https://spruceid.dev/docs/)
- [docs/didkit/concepts](https://spruceid.dev/docs/didkit/concepts)   
- [spruceid/didkit](https://github.com/spruceid/didkit)
- [spruceid.github.io/did-doge/index.html](https://spruceid.github.io/did-doge/index.html)
- [spruceid/did-doge](https://github.com/spruceid/did-doge)
![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421103032.png)

## DID 架構定位

> * [ssimeetup.org/dids-demystified-hands-intro-dids-btcr-did-method-kim-hamilton-duffy-webinar-5/](https://ssimeetup.org/dids-demystified-hands-intro-dids-btcr-did-method-kim-hamilton-duffy-webinar-5/)
> * [medium.com/@kimdhamilton](https://medium.com/@kimdhamilton)
> * [medium.com/@kimdhamilton/btcr-did-method-updates-d0fd14386139](https://medium.com/@kimdhamilton/btcr-did-method-updates-d0fd14386139)


![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421103132.png)

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421103729.png)

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421104318.png)

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421104440.png)


### 會議論文
* [Rebooting the Web of Trust VI: Santa Barbara (March 2018)](https://github.com/WebOfTrustInfo/rwot6-santabarbara)
* [Rebooting the Web of Trust VII: Toronto (September 2018)
](https://github.com/WebOfTrustInfo/rwot7-toronto)

### 黑客松作品
* [WebOfTrustInfo/btcr-hackathon-2019](https://github.com/WebOfTrustInfo/btcr-hackathon-2019)
* [w3c-ccg/did-hackathon-2018/blob/master/README.md](https://github.com/w3c-ccg/did-hackathon-2018/blob/master/README.md)


### btcr
* [WebOfTrustInfo/btcr-did-tools-js](https://github.com/WebOfTrustInfo/btcr-did-tools-js)
* [WebOfTrustInfo/btcr-tx-playground.github.io](https://github.com/WebOfTrustInfo/btcr-tx-playground.github.io)
* [WebOfTrustInfo/txref-conversion-js](https://github.com/WebOfTrustInfo/txref-conversion-js)
* [**decentralized-identity/uni-resolver-driver-did-btcr**](https://github.com/decentralized-identity/uni-resolver-driver-did-btcr)
* [WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/btcr_0_1.pdf](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/btcr_0_1.pdf)
* [w3c-ccg.github.io/didm-btcr/](https://w3c-ccg.github.io/didm-btcr/)
![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421110641.png)

### Use Case
> [w3c.github.io/did-spec-registries/#did-methods](https://w3c.github.io/did-spec-registries/#did-methods)

**重要**
幣安DID 設計：[ontology-tech/DID-solidity/binance-did/doc/zh/design_zh.md](https://github.com/ontology-tech/DID-solidity/blob/binance-did/doc/zh/design_zh.md)
* [proxy-patterns](https://blog.openzeppelin.com/proxy-patterns/)
![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421153605.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421153736.png)

清單：
- 網易 [netease-chain/Future-DID-Method-Specification/blob/main/README.md](https://github.com/netease-chain/Future-DID-Method-Specification/blob/main/README.md)
- IBM Digital Health Pass DID方法（hpass）[IBM/hpass/blob/main/doc/did-spec.md](https://github.com/IBM/hpass/blob/main/doc/did-spec.md)
- Binance DID方法規範 [ontology-tech/DID-method-specs/blob/master/did-bnb/DID-Method-bnb.md](https://github.com/ontology-tech/DID-method-specs/blob/master/did-bnb/DID-Method-bnb.md)
    - DID-財務穩固 [ontology-tech/DID-solidity/tree/binance-did](https://github.com/ontology-tech/DID-solidity/tree/binance-did)
        - DID-Binance-solidity接口文檔 [ontology-tech/DID-solidity/blob/binance-did/doc/zh/interface_zh.md](https://github.com/ontology-tech/DID-solidity/blob/binance-did/doc/zh/interface_zh.md)
        - DID-Binance-solidity設計文檔 [ontology-tech/DID-solidity/blob/binance-did/doc/zh/design_zh.md](https://github.com/ontology-tech/DID-solidity/blob/binance-did/doc/zh/design_zh.md)
- Corda DID方法 [/corda-did-method](https://htmlpreview.github.io/?https://github.com/persistentsystems/corda-did-method/blob/master/corda_did_method.html)
- 雲杉系統有限公司 [did-did.spruceid.com/](https://did-did.spruceid.com/)
- Ethereum
    - Emtrust Wai DID方法規範 （Hyperledger Fabric）[Halialabs/did-spec](https://github.com/Halialabs/did-spec/blob/gh-pages/readme.md)
    - ETHO DID方法規範 [ontology-tech/DID-method-specs](https://github.com/ontology-tech/DID-method-specs/blob/master/did-etho/DID-Method-etho.md)
    - did：erc725方法  [WebOfTrustInfo/rwot6-santabarbara/blob/master/topics-and-advance-readings/DID-Method-erc725.md](https://github.com/WebOfTrustInfo/rwot6-santabarbara/blob/master/topics-and-advance-readings/DID-Method-erc725.md)
    - ETHDID方法規範 [decentralized-identity/ethr-did-resolver/did-method-spec.md](https://github.com/decentralized-identity/ethr-did-resolver/blob/master/doc/did-method-spec.md)
    - ERC：輕型標識 ＃1056 [ethereum/EIPs/issues/1056](https://github.com/ethereum/EIPs/issues/1056)
- Gataca DID方法規範 [gataca-io/gataca-did-method](https://github.com/gataca-io/gataca-did-method)
- Git DID方法規範 [dhuseby/did-git-spec/blob/master/did-git-spec.md](https://github.com/dhuseby/did-git-spec/blob/master/did-git-spec.md)
- Github DID方法規範  [docs.github-did.com/did-method-spec/](https://docs.github-did.com/did-method-spec/)

ion:
![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421164401.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421164424.png)

---

## 代幣分類架構圖
[InterWorkAlliance/TokenTaxonomyFramework](https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/main/token-taxonomy.md)

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210420161424.png?token=AM6DPO2FVYDXSPANC6WFLSDAP2GZ4)

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210420162004.png?token=AM6DPO4TW2EI4PPBXM3CLUDAP2HPE)

---

## Claims

![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421140855.png) ![](https://raw.githubusercontent.com/awesome-doge/picgo/main/20210421140958.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/%E6%88%AA%E5%9C%96%202021-04-21%20%E4%B8%8B%E5%8D%883.26.48.png)![](https://raw.githubusercontent.com/awesome-doge/picgo/main/%E6%88%AA%E5%9C%96%202021-04-21%20%E4%B8%8B%E5%8D%883.25.46.png)

---

## 系統設計與實現


**物件**
1. 所有者
> 考慮多種 所有者
* DID 設計
  * 方法設計
  * 初始化參數設計
2. 被所有者
> 考慮多種 nft型態
* DID 設計
  * 方法設計
  * 初始化參數設計

* 增發需求
* 驗證發行者需求
* 驗證藝術家需求
* 驗證總發行量需求
* 驗證第幾個發行數需求
* 驗證Link Data 需求

---

**整體結構**：

- 選定一條鏈
- 選定應用的主題
- 註冊應用的主題

**特色化應用**：

結合 HD Wallet 結構 [GrgChain/DID-method-specs](https://github.com/GrgChain/DID-method-specs/blob/master/README.md)

```jsx
eg: device leg summer source assault drill pilot include excess sausage immense year m/1 m/2
```

1. 主錢包
2. 恢復錢包

**流程**：

1. 初始化錢包
2. 獲取登錄令牌
3. 更新文件服務
4. 重置文檔公鑰
