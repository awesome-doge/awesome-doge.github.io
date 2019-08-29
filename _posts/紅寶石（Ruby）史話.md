---
title: '紅寶石（Ruby）史話 [轉linux.cn]'
date: 2019-01-21 15:54:55
tags: [linux.cn, IBM]
categories: linux.cn
---
儘管我很難說清楚為什麼，但 Ruby 一直是我最喜愛的一門程式語言。如果用音樂來類比的話，Python 給我的感覺像是<ruby>朋克搖滾<rt>punk rock</rt></ruby>，簡單、直接，但略顯單調，而 Ruby 則像是爵士樂，從根本上賦予了程式設計師表達自我的自由，雖然這可能會讓程式碼變複雜，編寫出來的程式對其他人來說不直觀。

Ruby 社群一直將<ruby>靈活表達<rt>freedom of expression</rt></ruby>視為其核心價值。可我不認同這對於 Ruby 的開發和普及是最重要的。建立一門程式語言也許是為了更高的效能，也許是為了在抽象上節省更多的時間，可 Ruby 就有趣在它並不關心這些，從它誕生之初，它的目標就是讓程式設計師更快樂。

<!-- more --> 

### 松本·行弘

<ruby>松本·行弘<rt>Yukihiro Matsumoto</rt></ruby>，亦稱為 “Matz”，於 1990 年畢業於筑波大學。筑波是東京東北方向上的一個小城市，是科學研究與技術開發的中心之一。筑波大學以其 STEM 計劃廣為流傳。松本·行弘在筑波大學的資訊科學專業學習過，且專攻程式語言。他也在 Ikuo Nakata 的程式語言實驗室工作過。（LCTT 譯註：STEM 是<ruby>科學<rt>Science</rt></ruby>、<ruby>技術<rt>Technology</rt></ruby>、<ruby>工程<rt>Engineering</rt></ruby>、<ruby>數學<rt>Mathematics</rt></ruby>四門學科英文首字母的縮寫。）

松本從 1993 年開始製作 Ruby，那時他才剛畢業幾年。他製作 Ruby 的起因是覺得那時的指令碼語言缺乏一些特性。他在使用 Perl 的時候覺得這門語言過於“玩具”，此外 Python 也有點弱，用他自己的話說：

> 我那時就知道 Python 了，但我不喜歡它，因為我認為它不是一門真正的面向物件的語言。面向物件就像是 Python 的一個附件。作為一個程式語言狂熱者，我在 15 年裡一直是面向物件的忠實粉絲。我真的想要一門生來就面向物件而且易用的指令碼語言。我為此特地尋找過，可事實並不如願。[^1]

所以一種解釋松本創造 Ruby 的動機就是他想要創造一門更好，且面向物件的 Perl。

但在其他場合，松本說他創造 Ruby 主要是為了讓他自己和別人更快樂。2008 年，松本在谷歌技術講座結束時放映了這張幻燈片：

![][1]

他對聽眾說到，

> 我希望 Ruby 能幫助世界上的每一個程式設計師更有效率地工作，享受程式設計並感到快樂。這也是製作 Ruby 語言的主要意圖。[^2]

松本開玩笑的說他製作 Ruby 的原因很自私，因為他覺得其它的語言乏味，所以需要創造一點讓自己開心的東西。

這張幻燈片展現了松本謙虛的一面。其實，松本是一位摩門教踐行者，因此我很好奇他傳奇般的友善有多少歸功於他的宗教信仰。無論如何，他的友善在 Ruby 社群廣為流傳，甚至有一條稱為 MINASWAN 的原則，即“<ruby>松本人很好，我們也一樣<rt>Matz Is Nice And So We Are Nice</rt></ruby>”。我想那張幻燈片一定震驚了來自 Google 的觀眾。我想谷歌技術講座上的每張幻燈片都充滿著程式碼和執行效率的指標，來說明一個方案比另一個更快更有效，可僅僅放映崇高的目標的幻燈片卻寥寥無幾。

Ruby 主要受到 Perl 的影響。Perl 則是由 Larry Wall 於 20 世紀 80 年代晚期創造的語言，主要用於處理和轉換基於文字的資料。Perl 因其文字處理和正則表示式而聞名於世。對於 Ruby 程式設計師，Perl 程式中的很多語法元素都不陌生，例如符號 `$`、符號 `@`、`elsif` 等等。雖然我覺得，這些不是 Ruby 應該具有的特徵。除了這些符號外，Ruby 還借鑑了 Perl 中的正則表示式的處理和標準庫。

但影響了 Ruby 的不僅僅只有 Perl 。在 Ruby 之前，松本製作過一個僅用 Emacs Lisp 編寫的郵件客戶端。這一經歷讓他對 Emacs 和 Lisp 語言執行的內部原理有了更多的認識。松本說 Ruby 底層的物件模型也受其啟發。在那之上，松本添加了一個 Smalltalk 風格的資訊傳遞系統，這一系統隨後成為了 Ruby 中任何依賴 `#method_missing` 的操作的基石。松本也表示過 Ada 和 Eiffel 也影響了 Ruby 的設計。

當時間來到了給這門新語言命名的時候，松本和他的同事 Keiju Ishitsuka 挑選了很多個名字。他們希望名字能夠體現新語言和 Perl、shell 指令碼間的聯絡。在[這一段非常值得一讀的即時訊息記錄][2]中，Ishitsuka 和 松本也許花了太多的時間來思考 <ruby>shell<rt>貝殼</rt></ruby>、<ruby>clam<rt>蛤蠣</rt></ruby>、<ruby>oyster<rt>牡蠣</rt></ruby>和<ruby>pearl<rt>珍珠</rt></ruby>之間的關係了，以至於差點把 Ruby 命名為“<ruby>Coral<rt>珊瑚蟲</rt></ruby>”或“<ruby>Bisque<rt>貝類濃湯</rt></ruby>”。幸好，他們決定使用 Ruby，因為它就像 pearl 一樣，是一種珍貴的寶石。此外，<ruby>Ruby<rt>紅寶石</rt></ruby> 還是 7 月的生辰石，而 <ruby>Pearl<rt>珍珠</rt></ruby> 則是 6 月的生辰石，採用了類似 C++ 和 C# 的隱喻，暗示著她們是改進自前輩的程式語言。（LCTT 譯註：Perl 和 Pearl 發音相同，所以也常以“珍珠”來借喻 Perl；shell 是作業系統提供的使用者介面，這裡指的是命令列介面；更多有關生辰石的[資訊](https://zh.wikipedia.org/zh-hans/%E8%AA%95%E7%94%9F%E7%9F%B3)。）

### Ruby 西漸

Ruby 在日本的普及很快。1995 年 Ruby 剛剛釋出後不久後，松本就被一家名為 Netlab 的日本軟體諮詢財團（全名 Network Applied Communication Laboratory）僱用，並全職為 Ruby 工作。到 2000 年時，在 Ruby 釋出僅僅 5 年後，Ruby 在日本的流行度就超過了 Python。可這時的 Ruby 才剛剛進入英語國家。雖然從 Ruby 的誕生之初就存在討論它的日語郵件列表，但是英語的郵件列表直到 1998 年才建立起來。起初，在英語的郵件列表中交流的大多是日本的 Ruby 狂熱者，可隨著 Ruby 在西方的逐漸普及而得以改變。

在 2000 年，Dave Thomas 出版了第一本涵蓋 Ruby 的英文書籍《Programming Ruby》。因為它的封面上畫著一把鋤頭，所以這本書也被稱為鋤頭書。這是第一次向身處西方的程式設計師們介紹了 Ruby。就像在日本那樣，Ruby 的普及很快，到 2002 年時，英語的 Ruby 郵件列表的通訊量就超過了日語郵件列表。

時間來到了 2005 年，Ruby 更流行了，但它仍然不是主流的程式語言。然而，Ruby on Rails 的釋出讓一切都不一樣了。Ruby on Rails 是 Ruby 的“殺手級應用”，沒有別的什麼項目能比它更推動 Ruby 的普及了。在 Ruby on Rails 釋出後，人們對 Ruby 的興趣爆發式的增長，看看 TIOBE 監測的語言排行：

![][3]

有時人們開玩笑的說，Ruby 程式全是基於 Ruby-on-Rails 的網站。雖然這聽起來就像是 Ruby on Rails 佔領了整個 Ruby 社群，但在一定程度上，這是事實。因為編寫 Rails 應用時使用的語言正是 Ruby。Rails 欠 Ruby 的和 Ruby 欠 Rails 的一樣多。

Ruby 的設計哲學也深深地影響了 Rails 的設計與開發。Rails 之父 David Heinemeier Hansson 常常提起他第一次與 Ruby 的接觸的情形，那簡直就是一次傳教。他說，那種經歷簡直太有感召力了，讓他感受到要為松本的傑作（指 Ruby）“傳教”的使命。[^3] 對於 Hansson 來說，Ruby 的靈活性簡直就是對 Python 或 Java 語言中自上而下的設計哲學的反抗。他很欣賞 Ruby 這門能夠信任自己的語言，Ruby 賦予了他自由選擇<ruby>程式表達方式<rt>express his programs</rt></ruby>的權力。

就像松本那樣，Hansson 聲稱他創造 Rails 時因為對現狀的不滿並想讓自己能更開心。他也認同讓程式設計師更快樂高於一切的觀點，所以檢驗 Rails 是否需要新增一項新特性的標準是“<ruby>更燦爛的笑容標準<rt>The Principle of The Bigger Smile</rt></ruby>”。什麼功能能讓 Hansson 更開心就給 Rails 新增什麼。因此，Rails 中包括了很多非正統的功能，例如 “Inflector” 類和 `Time` 擴充套件（“Inflector”類試圖將單個類的名字對映到多個數據庫表的名字；`Time` 擴充套件允許程式設計師使用 `2.days.ago` 這樣的表示式）。可能會有人覺得這些功能太奇怪了，但 Rails 的成功表明它的確能讓很多人的生活得更快樂。

因此，雖然 Rails 的火熱帶動了 Ruby 的普及看起來是一個偶然，但事實上 Rails 體現了 Ruby 的很多核心準則。此外，很難看到使用其他語言開發的 Rails，正是因為 Rails 的實現依賴於 Ruby 中<ruby>類似於宏的類方法呼叫<rt>macro-like class method calls</rt></ruby>來實現模型關聯這樣的功能。一些人認為這麼多的 Ruby 開發需要基於 Ruby on Rails 是 Ruby 生態不健康的表現，但 Ruby 和 Ruby on Rails 結合的如此緊密並不是沒有道理的。

### Ruby 之未來  

人們似乎對 Ruby（及 Ruby on Rails）是否正在消亡有著異常的興趣。早在 2011 年，Stack Overflow 和 Quora 上就充斥著程式設計師在諮詢“如果幾年後不再使用 Ruby 那麼現在是否有必要學它”的話題。這些擔憂對 Ruby 並非沒有道理，根據 TIOBE 指數和 Stack Overflow 趨勢，Ruby 和 Ruby on Rails 的人氣一直在萎縮，雖然它也曾是熱門新事物，但在更新更熱的框架面前它已經黯然失色。

一種解釋這種趨勢的理論是程式設計師們正在捨棄動態類型的語言轉而選擇靜態類型的。TIOBE 指數的趨勢中可以看出對軟體質量的需求在上升，這意味著出現在執行時的異常變得難以接受。他們引用 TypeScript 來說明這一趨勢，TypeScript 是 JavaScript 的全新版本，而創造它的目的正是為了保證客戶端執行的程式碼能受益於編譯所提供的安全保障。

我認為另一個更可能的原因是比起 Ruby on Rails 推出的時候，現在存在著更多有競爭力的框架。2005 年它剛剛釋出的時候，還沒有那麼多用於建立 Web 程式的框架，其主要的替代者還是 Java。可在今天，你可以使用為 Go、Javascript 或者 Python 開發的各種優秀的框架，而這還僅僅是主流的選擇。Web 的世界似乎正走向更加分散式的結構，與其使用一塊程式碼來完成從資料庫讀取到頁面渲染所有事務，不如將事務拆分到多個元件，其中每個元件專注於一項事務並將其做到最好。在這種趨勢下，Rails 相較於那些專攻於 JavaScript 前端通訊的 JSON API 就顯得過於寬泛和臃腫。

總而言之，我們有理由對 Ruby 的未來持樂觀態度。因為不管是 Ruby 還是 Rails 的開發都還很活躍。松本和其他的貢獻者們都在努力開發 Ruby 的第三個主要版本。新的版本將比現在的版本快上 3 倍，以減輕制約著 Ruby 發展的效能問題。雖然從 2005 年起，越來越多的 Web 框架被開發出來，但這並不意味著 Ruby on Rails 就失去了其生存空間。Rails 是一個富有大量功能的成熟的工具，對於一些特定類型的應用開發一直是非常好的選擇。

但就算 Ruby 和 Rails 走上了消亡的道路，Ruby 讓程式設計師更快樂的信條一定會存活下來。Ruby 已經深遠的影響了許多新的程式語言的設計，這些語言的設計中能夠看到來自 Ruby 的很多理念。而其他的新生語言則試著變成 Ruby 更現代的實現，例如 Elixir 是一個強調函數語言程式設計範例的語言，仍在開發中的 Crystal 目標是成為使用靜態類型的 Ruby 。世界上許多程式設計師都喜歡上了 Ruby 及其語法，因此它的影響必將會在未來持續很長一段時間。

喜歡這篇文章嗎？這裡每兩週都會發表一篇這樣的文章。請在推特上關注我們 [@TwoBitHistory][4] 或者訂閱我們的 [RSS][5]，這樣新文章釋出的第一時間你就能得到通知。

[^1]: http://ruby-doc.org/docs/ruby-doc-bundle/FAQ/FAQ.html
[^2]: https://www.youtube.com/watch?v=oEkJvvGEtB4?t=30m55s
[^3]: http://rubyonrails.org/doctrine/

--------------------------------------------------------------------------------

via: https://twobithistory.org/2017/11/19/the-ruby-story.html

作者：[Two-Bit History][a]
選題：[lujun9972][b]
譯者：[wwhio](https://github.com/wwhio)
校對：[wxy](https://github.com/wxy)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原創編譯，[Linux中國](https://linux.cn/) 榮譽推出

[a]: https://twobithistory.org
[b]: https://github.com/lujun9972
[1]: https://twobithistory.org/images/matz.png
[2]: http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-talk/88819
[3]: https://twobithistory.org/images/tiobe_ruby.png
[4]: https://twitter.com/TwoBitHistory
[5]: https://twobithistory.org/feed.xml