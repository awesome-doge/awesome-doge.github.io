---
title: Bitcoin IRC 2018.12.07
date: 2018-12-07 04:33:57
tags: [Bitcoin IRC, bitcoin]
categories: Bitcoin IRC Meeting
---

(英文)
03:00 wumpus: #startmeeting
03:00 lightningbot: Meeting started Thu Dec  6 19:00:24 2018 UTC.  The chair is wumpus. Information about MeetBot at http://wiki.debian.org/MeetBot.
03:00 lightningbot: Useful Commands: #action #agreed #help #info #idea #link #topic.
03:00 wumpus: #bitcoin-core-dev Meeting: wumpus sipa gmaxwell jonasschnelli morcos luke-jr sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator aj Chris_Stewart_5 dongcarl gwillen jamesob ken281221 ryanofsky gleb
<!-- more --> 
03:00 sipa: hi
03:00 jnewbery: hi
03:00 gleb: hi
03:00 meshcollider: hi
03:00 jamesob: hi
03:00 Teddy_: ji
03:00 dongcarl: hi
03:00 wumpus: topics? (one has been proposed in https://gist.github.com/moneyball/071d608fdae217c2a6d7c35955881d8a)
03:01 chenpo: hi
03:01 achow101: hi
03:01 meshcollider: gleb also mentioned earlier in the week he wanted to talk about dandelion but i'm not sure if that was a meeting topic or just a general desire :)
03:02 moneyball: Hi
03:02 gleb: meshcollider: More of a second. I can't really drive the discussion because I don't remember all the specifics
03:02 provoostenator: hi
03:03 wumpus: #topic high priority for review
03:03 wumpus: 6 PRs on the list right now: https://github.com/bitcoin/bitcoin/projects/8
03:03 phantomcircuit: hi
03:04 wumpus: if there's anything to add or remove, please let me know
03:04 gmaxwell: welp, I can't seem to reach github right now. :(
03:04 ChanServ has changed mode: -o wumpus
03:04 jnewbery: I added #14565 today since it was blocking a bunch of other people's PRs
03:04 gribble: https://github.com/bitcoin/bitcoin/issues/14565 | Overhaul importmulti logic by sipa · Pull Request #14565 · bitcoin/bitcoin · GitHub
03:04 wumpus: gmaxwell: strange! no problems here it seems
03:04 meshcollider: yeah there are like 4 PRs stacked on that
03:05 jnewbery: also #14886 since sipa's was blocked on adding test coverage
03:05 sipa: #14782 #13932 #14336 #14646 #14565 #14886
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14886 | [tests] Refactor importmulti tests by jnewbery · Pull Request #14886 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14782 | [0.17] Bugfix: Correctly calculate balances when min_conf is used, and for getbalance("*") by luke-jr · Pull Request #14782 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/13932 | Additional utility RPCs for PSBT by achow101 · Pull Request #13932 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14336 | net: implement poll by pstratem · Pull Request #14336 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14646 | Add expansion cache functions to descriptors (unused for now) by sipa · Pull Request #14646 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14565 | Overhaul importmulti logic by sipa · Pull Request #14565 · bitcoin/bitcoin · GitHub
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14886 | [tests] Refactor importmulti tests by jnewbery · Pull Request #14886 · bitcoin/bitcoin · GitHub
03:05 wumpus: yes, those
03:05 sipa: That's the high priority list
03:06 MarcoFalke: I'd like to add #14480, since it seems required for some other work
03:07 gribble: https://github.com/bitcoin/bitcoin/issues/14480 | refactor: Drop boost::this_thread::interruption_point and boost::thread_interrupted in main thread by ken2812221 · Pull Request #14480 · bitcoin/bitcoin · GitHub
03:07 MarcoFalke: Also, the getbalance fixes need rebase for some days now
03:07 MarcoFalke: usually we take them off of hipri?
03:08 wumpus: ok, added
03:08 sipa: maybe we should first discuss what's left to do for 0.17.1?
03:08 sipa: or as a separate topic
03:08 achow101: #13932 can be removed for now. I won't have time to work on it for another week or two
03:08 gribble: https://github.com/bitcoin/bitcoin/issues/13932 | Additional utility RPCs for PSBT by achow101 · Pull Request #13932 · bitcoin/bitcoin · GitHub
03:08 wumpus: nothing on the high priority list is required for 0.17.1, that's a separate topic
03:08 wumpus: achow101: ok
03:09 MarcoFalke: removed #14782
03:09 gribble: https://github.com/bitcoin/bitcoin/issues/14782 | [0.17] Bugfix: Correctly calculate balances when min_conf is used, and for getbalance("*") by luke-jr · Pull Request #14782 · bitcoin/bitcoin · GitHub
03:09 wumpus: makes sense
03:09 wumpus: #topic 0.17.1
03:10 phantomcircuit: #14336 is done
03:10 MarcoFalke: meshcollider wanted to get in two more fixes
03:10 gribble: https://github.com/bitcoin/bitcoin/issues/14336 | net: implement poll by pstratem · Pull Request #14336 · bitcoin/bitcoin · GitHub
03:10 wumpus: there's nothing open on the 0.17.1 milestone at least
03:10 gmaxwell: MarcoFalke: what are the two outstanding?
03:11 sipa: meshcollider: i haven't paid that much attention lately; do you have a backport for 14424?
03:11 MarcoFalke: https://github.com/bitcoin/bitcoin/issues?q=label%3A%22Needs+backport%22+is%3Aclosed
03:11 meshcollider: Im about to open one
03:11 MarcoFalke: the ones with tag "17.1"
03:12 wumpus: I think it's really due time to release 0.17.1
03:12 wumpus: we wanted to do the release weeks agao AFAIK, we should avoid adding new things to it again and again
03:13 sipa: yeah, i think it's too late to add new things
03:13 jnewbery: wumpus: +1
03:13 gmaxwell: I don't think these are new unfortunately, somehow they fell of the radar. They are good, but we shouldn't delay more.
03:13 gmaxwell: s/of/off/
03:13 meshcollider: fair enough :)
03:13 sipa: gmaxwell: exactly
03:13 wumpus: but it's fine with me to wait another day or so for more backports
03:14 gmaxwell: (like 14689 I asked it to be tagged for backport 17 days ago, it was tagged 15 days ago, but just got missed)
03:14 gmaxwell: wumpus: could we do the RC today otherwise?
03:14 wumpus: gmaxwell: yes, the version has been bumped, afaik everything has been done for the release process, just needs tagging
03:14 bitcoin-git: [bitcoin] MeshCollider opened pull request #14889: [0.17] Backport #14424 (Stop requiring imported pubkey to sign non-PKH schemes) (0.17...201812_backport_14424) https://github.com/bitcoin/bitcoin/pull/14889
03:14 meshcollider: ill tag that for 0.17.2 then
03:15 MarcoFalke: In the future we should really backport in the same order as they are merged to master
03:15 wumpus: but if there are known serious fixes that affect a lot of users of course they should still be backported
03:15 MarcoFalke: Ideally a bot would do that
03:15 gmaxwell: well it's the backport is done and works, waiting a couple hours to tag 0.17.1 wouldn't be an issue.
03:15 wumpus: MarcoFalke: I used to do that with a script
03:16 gmaxwell: MarcoFalke: I think in this case, things got needs backport tags out of order.  I went and pinged a dozen PRs to get tagged, and some were and some took a few days, and some took a week.
03:16 wumpus: (e.g. it takes a list of PRs and cherry-picks the commits in the order the commits appear in master)
03:16 gmaxwell: and some got backported in the meantime.
03:16 MarcoFalke: Yeah, we should be more careful with tagging bug fixes to the right milestone
03:17 wumpus: but it's more complex for things that can't just be cherry picked
03:17 wumpus: whose PRs really need extra work
03:17 wumpus: and we had a few of those, this time
03:17 meshcollider: e.g. this one which relied on some keyorigininfo
03:17 MarcoFalke: Right when there is a bug fix it should say when it was introduced and what the target branch is
03:18 wumpus: yes
03:19 MarcoFalke: We should also require a test with each bug fix and travis and other testers should check that the test fails withou the code changes
03:19 wumpus: I tend to ask for that
03:19 gmaxwell: That should help reduce the number of fixes which will make backporting easier... :P
03:19 MarcoFalke: Similar to the scripted-diff prefix we could add a bug-fix: prefix that must do just that
03:19 gmaxwell: (I don't disagree, though some things are pretty hard to test.)
03:20 MarcoFalke: Yeah
03:20 wumpus: anyhow we're drifting off topic, what still needs to be done for 0.17.1?
03:20 wumpus: I guess someone needs to backport #14689 and #14424
03:21 gribble: https://github.com/bitcoin/bitcoin/issues/14689 | Require a public key to be retrieved when signing a P2PKH input by achow101 · Pull Request #14689 · bitcoin/bitcoin · GitHub
03:21 gribble: https://github.com/bitcoin/bitcoin/issues/14424 | Stop requiring imported pubkey to sign non-PKH schemes by sipa · Pull Request #14424 · bitcoin/bitcoin · GitHub
03:21 meshcollider: i just did the second, #14889
03:21 gribble: https://github.com/bitcoin/bitcoin/issues/14889 | [0.17] Backport #14424 (Stop requiring imported pubkey to sign non-PKH schemes) by MeshCollider · Pull Request #14889 · bitcoin/bitcoin · GitHub
03:21 gmaxwell: In any case, if people think they can review that backport that just went up, presumably it could go in.  I think if we have things that could go into today then RC we should, we certantly shouldn't _wait_.
03:21 provoostenator: Are there up to date Gitian instructions for Docker? I'd like to try both Bionic in a VM and Docker this time.
03:21 gmaxwell: I can try to test the backport of 14424 as soon as the meeting is over.
03:22 wumpus: gitian with docker? I'm not aware of anyone doing that
03:22 wumpus: gmaxwell: thanks!
03:22 MarcoFalke: provoostenator: build-gitian.py (in our master brach)
03:22 MarcoFalke: --docker or something
03:22 gmaxwell: wumpus: want to basically just tag 0.17.1 in N hours (you pick N) with whatever is merged by then?
03:23 gmaxwell: (presumaby N set before you go to bed)
03:24 wumpus: gmaxwell: sounds good to me
03:24 sipa: sgtm
03:24 wumpus: MarcoFalke: ah yes, I keep forgetting about that script
03:25 wumpus: #topic next CoreDev meetup (moneyball)
03:25 moneyball: hi
03:26 moneyball: i wanted to get feedback on having the next CoreDev June 5-7 in Amsterdam right before Breaking Bitcoin conference
03:26 wumpus: good idea!
03:26 moneyball: i think Europe is a good location as the past 4 CoreDevs haven't been in Europe
03:26 moneyball: and yes wumpus surely likes it :)
03:26 jnewbery: ACK
03:27 moneyball: it also gives the opportunity to attend BB if interested
03:28 moneyball: so "save the date" on your calendars, and let me know here or over DM if you have any thoughts or feedback
03:29 phantomcircuit: moneyball, BB ?
03:29 wumpus: combining it with a conference is useful
03:29 moneyball: https://twitter.com/breakingbitcoin/status/1070060118866305026
03:30 sipa: ack amsterdam
03:30 sipa: :)
03:31 wumpus: I think we agree then :) any other topics?
03:33 wumpus: PSA: if, during the course of the week, you have any ideas for next week's meeting let moneyball know, he'll add it to the list on https://gist.github.com/moneyball/071d608fdae217c2a6d7c35955881d8a
03:34 wumpus: I've also added that link to the topic here
03:34 jnewbery: use tag #proposedmeetingtopic so Steve can grep
03:35 wumpus: would be good to add that to the gist
03:35 wumpus: can't put much more in the topic itself
03:37 wumpus: any other topics?
03:38 wumpus: #endmeeting
03:38 lightningbot: Meeting ended Thu Dec  6 19:38:44 2018 UTC.  Information about MeetBot at http://wiki.debian.org/MeetBot . (v 0.1.4)
03:38 lightningbot: Minutes:        http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.html
03:38 lightningbot: Minutes (text): http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.txt
03:38 lightningbot: Log:            http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.log.html

(中文亂翻)
03:00 wumpus：#startmeeting 
03:00 lightningbot：會議開始於12月6日星期四19:00:24 2018 UTC。 椅子是wumpus。 有關MeetBot的信息   http://wiki.debian.org/MeetBot 。 
03:00 lightningbot：有用的命令：#action #agreed #help #info #idea #link #topic。 
03:00 wumpus：#bitcoin-core-dev會議：wumpus sipa gmaxwell jonasschnelli morcos luke-jr sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator aj Chris_Stewart_5 dongcarl gwillen jamesob ken281221 ryanofsky gleb 
03:00 sipa：嗨 
03:00 jnewbery：嗨 
03:00 gleb：嗨 
03:00 meshcollider：嗨 
03:00 jamesob：嗨 
03:00 Teddy_：ji 
03:00 dongcarl：嗨 
03:00 wumpus：主題？ （已提出一個   https://gist.github.com/moneyball/071d608fdae217c2a6d7c35955881d8a ） 
03:01 chenpo：嗨 
03:01 achow101：嗨 
03:01 meshcollider：gleb也在本週早些時候提到他想談蒲公英，但我不確定這是一個會議主題還是只是一般的願望:) 
03:02 moneyball：嗨 
03:02 gleb：meshcollider：更多的一秒鐘。 我不能真正推動討論，因為我不記得所有具體細節 
03:02 provoostenator：嗨 
03:03 wumpus：#topic審查的重中之重 
03:03 wumpus：現在名單上的6個PR：   https://github.com/bitcoin/bitcoin/projects/8 
03:03 phantomcircuit：嗨 
03:04 wumpus：如果有任何要添加或刪除的內容，請告訴我 
03:04 gmaxwell：welp，我現在似乎無法到達github。 :( 
03:04 ChanServ改變了模式：-o wumpus 
03:04 jnewbery：我今天添加了＃14565，因為它阻止了其他一些人的PR 
03:04抱怨：   https://github.com/bitcoin/bitcoin/issues/14565   | 通過sipa大修importmulti邏輯·Pull Request＃14565·比特幣/比特幣·GitHub 
03:04 wumpus：gmaxwell：奇怪！ 這似乎沒問題 
03:04 meshcollider：是的，有4個PR堆疊在上面 
03:05 jnewbery：也是＃14886，因為sipa在添加測試覆蓋率時被阻止了 
03:05 sipa：＃14782＃13932＃14336＃14646＃14565＃14886 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14886   | [測試]重構由jnewbery進行多項測試·Pull Request＃14886·比特幣/比特幣·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14782   | [0.17]修正：使用min_conf時正確計算餘額 ，luke-jr 正確計算getbalance（“ ”）·Pull Request＃14782·比特幣/比特幣·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/13932   | 用於PSBT的附加實用程序RPC by achow101·Pull Request＃13932·bitcoin / bitcoin·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14336   | net：通過pstratem實現民意調查·拉請求＃14336·比特幣/比特幣·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14646   | 通過sipa將擴展緩存函數添加到描述符（暫時未使用）·Pull Request＃14646·bitcoin / bitcoin·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14565   | 通過sipa大修importmulti邏輯·Pull Request＃14565·比特幣/比特幣·GitHub 
03:05抱怨：   https://github.com/bitcoin/bitcoin/issues/14886   | [測試]重構由jnewbery進行多項測試·Pull Request＃14886·比特幣/比特幣·GitHub 
03:05 wumpus：是的，那些 
03:05 sipa：這是高優先級列表 
03:06 MarcoFalke：我想添加＃14480，因為它似乎需要其他一些工作 
03:07抱怨：   https://github.com/bitcoin/bitcoin/issues/14480   | 重構：通過ken2812221在主線程中刪除boost :: this_thread :: interruption_point和boost :: thread_interrupted·Pull Request＃14480·bitcoin / bitcoin·GitHub 
03:07 MarcoFalke：此外，getbalance修復 現在 需要幾天的折扣 
03:07 MarcoFalke：通常我們會把它們從hipri身上帶走？ 
03:08 wumpus：好的，補充道 
03:08 sipa：也許我們應該首先討論0.17.1還剩下什麼？ 
03:08 sipa：或作為一個單獨的主題 
03:08 achow101：＃13932暫時可以刪除。 我將沒有時間再工作一兩個星期 
03:08抱怨：   https://github.com/bitcoin/bitcoin/issues/13932   | 用於PSBT的附加實用程序RPC by achow101·Pull Request＃13932·bitcoin / bitcoin·GitHub 
03:08 wumpus：0.17.1需要高優先級列表中的任何內容，這是一個單獨的主題 
03:08 wumpus：achow101：好的 
03:09 MarcoFalke：刪除＃14782 
03:09抱怨：   https://github.com/bitcoin/bitcoin/issues/14782   | [0.17]修正：使用min_conf時正確計算餘額 ，luke-jr 正確計算getbalance（“ ”）·Pull Request＃14782·比特幣/比特幣·GitHub 
03:09 wumpus：有道理 
03:09 wumpus：#topic 0.17.1 
03:10 phantomcircuit：＃14336完成了 
03:10 MarcoFalke：meshcollider希望再獲得兩個補丁 
03:10抱怨：   https://github.com/bitcoin/bitcoin/issues/14336   | net：通過pstratem實現民意調查·拉請求＃14336·比特幣/比特幣·GitHub 
03:10 wumpus：至少在0.17.1里程碑上沒有任何開放 
03:10 gmaxwell：MarcoFalke：這兩個突出的是什麼？ 
03:11 sipa：meshcollider：我最近沒有那麼多關注; 你有14424的後退嗎？ 
03:11 MarcoFalke：   https://github.com/bitcoin/bitcoin/issues?q=label%3A"Needs+backport"+is%3Aclosed 
03:11 meshcollider：我要打開一個 
03:11 MarcoFalke：帶有“17.1”標籤的人 
03:12 wumpus：我認為現在應該發布0.17.1 
03:12 wumpus：我們想要發布週agao AFAIK，我們應該避免一次又一次地添加新東西 
03:13 sipa：是的，我認為添加新東西為時已晚 
03:13 jnewbery：wumpus：+1 
03:13 gmaxwell：不幸的是，我不認為這些是新的，不知怎的，他們已經失去了雷達。 他們很好，但我們不應該拖延更多。 
03:13 gmaxwell：s / of / off / 
03:13 meshcollider：足夠公平:) 
03:13 sipa：gmaxwell：確切地說 
03:13 wumpus：但是我可以再等一天左右更多的後退 
03:14 gmaxwell :(就像14689我要求它在17天前標記為後退，它在15天前被標記，但是錯過了） 
03:14 gmaxwell：wumpus：我們今天可以做RC嗎？ 
03:14 wumpus：gmaxwell：是的，版本已經被撞了，afaik已經為發布過程做了一切，只需要標記 
03:14 bitcoin-git：[比特幣] MeshCollider打開拉請求＃14889：[0.17] Backport＃14424（停止要求導入的pubkey簽署非PKH方案）（0.17 ... 201812_backport_14424）   https://github.com/bitcoin/bitcoin/pull/14889 
03:14 meshcollider：生病標籤為0.17.2然後 
03:15 MarcoFalke：未來我們應該按照他們合併為主人的順序向後移動 
03:15 wumpus：但是如果有一些已知的嚴重修復程序會影響很多用戶，他們當然應該向後移植 
03:15 MarcoFalke：理想情況下，機器人會這樣做 
03:15 gmaxwell：好吧，這是後退完成並且正常工作，等待幾個小時標記0.17.1不會是一個問題。 
03:15 wumpus：MarcoFalke：我曾經用劇本做過 
03:16 gmaxwell：MarcoFalke：我想在這種情況下，需要的東西需要後退標籤。 我去了十幾個PR來標記，有些是，有些花了幾天，有些需要一個星期。 
03:16 wumpus :(例如，它按照提交在主人中出現的順序列出了PR和櫻桃選擇提交） 
03:16 gmaxwell：有些人在此期間得到了回复。 
03:16 MarcoFalke：是的，我們應該更加謹慎地將錯誤修復標記到正確的里程碑 
03:17 wumpus：但對於那些不能被挑選出來的東西來說，它更複雜 
03:17 wumpus：他們的PR真的需要額外的工作 
03:17 wumpus：這次我們有幾個 
03:17 meshcollider：例如，這個依賴於一些keyorigininfo 
03:17 MarcoFalke：當有錯誤修復時，應該說它何時被引入以及目標分支是什麼 
03:18 wumpus：是的 
03:19 MarcoFalke：我們還應該要求對每個bug修復進行測試，travis和其他測試人員應該檢查測試是否因代碼更改而失敗 
03:19 wumpus：我傾向於要求這樣做 
03:19 gmaxwell：這應該有助於減少修復的數量，這將使後移更容易......：P 
03:19 MarcoFalke：類似於scripted-diff前綴，我們可以添加一個bug-fix：前綴，必須做到這一點 
03:19 gmaxwell :(我不同意，雖然有些事情很難測試。） 
03:20 MarcoFalke：是的 
03:20 wumpus：無論如何我們正在脫離主題，還需要為0.17.1做些什麼？ 
03:20 wumpus：我想有人需要向後移動＃14689和＃14424 
03:21抱怨：   https://github.com/bitcoin/bitcoin/issues/14689   | 通過achow101簽署P2PKH輸入時需要檢索公鑰·Pull Request＃14689·bitcoin / bitcoin·GitHub 
03:21抱怨：   https://github.com/bitcoin/bitcoin/issues/14424   | 停止要求導入的pubkey通過sipa簽署非PKH方案·Pull Request＃14424·bitcoin / bitcoin·GitHub 
03:21 meshcollider：我剛做了第二次，＃14889 
03:21抱怨：   https://github.com/bitcoin/bitcoin/issues/14889   | [0.17] Backport＃14424（停止要求導入的pubkey簽署非PKH方案）MeshCollider·Pull Request＃14889·bitcoin / bitcoin·GitHub
03:21 gmaxwell：無論如何，如果人們認為他們可以審查剛剛上升的那個後端，可能它會進入。我想如果我們有可以進入今天的東西然後RC我們應該，我們絕對不應該   等待 。 
03:21 provoostenator：是否有針對Docker的最新Gitian說明？ 我想這次嘗試在VM和Docker中使用Bionic。 
03:21 gmaxwell：我可以在會議結束後儘快測試14424的後端。 
03:22 wumpus：gitian和docker？ 我不知道有人這樣做 
03:22 wumpus：gmaxwell：謝謝！ 
03:22 MarcoFalke：provoostenator：   build-gitian.py   （在我們的主人腦中） 
03:22 MarcoFalke： - docker什麼的 
03:22 gmaxwell：wumpus：想要基本上只用N小時標記0.17.1（你選N）用什麼合併然後呢？ 
03:23 gmaxwell :(在你睡覺前N設定） 
03:24 wumpus：gmaxwell：聽起來不錯 
03:24 sipa：sgtm 
03:24 wumpus：MarcoFalke：啊，是的，我一直忘記那個劇本 
03:25 wumpus：#topic next CoreDev meetup（moneyball） 
03:25 moneyball：嗨 
03:26 moneyball：我希望獲得有關在Breaking Bitcoin會議之前在阿姆斯特丹舉辦下一屆CoreDev 6月5日至7日的反饋 
03:26 wumpus：好主意！ 
03:26 moneyball：我認為歐洲是一個很好的位置，因為過去的4個CoreDevs還沒有出現在歐洲 
03:26 moneyball：是的wumpus肯定喜歡它:) 
03:26 jnewbery：確認 
03:27 moneyball：如果有興趣，它還有機會參加BB 
03:28 moneyball：所以在你的日曆上“保存日期”，如果您有任何想法或反饋，請告訴我這里或DM 
03:29 phantomcircuit：moneyball，BB？ 
03:29 wumpus：將它與會議相結合很有用 
03:29錢球：   https://twitter.com/breakingbitcoin/status/1070060118866305026 
03:30 sipa：ack amsterdam 
03:30 sipa：:) 
03:31 wumpus：我認為我們同意:)任何其他話題？ 
03:33 wumpus：PSA：如果，在本週的過程中，你對下週的會議有任何想法讓錢球知道，他會把它添加到列表上   https://gist.github.com/moneyball/071d608fdae217c2a6d7c35955881d8a 
03:34 wumpus：我還在這裡添加了這個主題的鏈接 
03:34 jnewbery：使用標籤#proposedmeetingtopic讓史蒂夫可以grep 
03:35 wumpus：將其添加到要點會很好 
03:35 wumpus：不能在話題中加入更多內容 
03:37 wumpus：還有其他主題嗎？ 
03:38 wumpus：#endmeeting 
03:38 lightningbot：會議於12月6日星期四19:38:44 2018 UTC結束。 有關MeetBot的信息   http://wiki.debian.org/MeetBot   。 （v 0.1.4） 
03:38 lightningbot：分鐘：    http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.html 
03:38 lightningbot：分鐘（文字）：   http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.txt 
03:38 lightningbot：日誌：    http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-06-19.00.log.html