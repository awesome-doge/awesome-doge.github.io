---
title: Bitcoin IRC 2018.12.14
date: 2018-12-14 03:57:29
tags: [Bitcoin IRC, bitcoin]
categories: Bitcoin IRC Meeting
---

總的來說

* 在吵 不同版本的key 模式，到底要在哪裡激活 gui?bitcoin.conf?(好像沒結論)
* 放棄vista 支持，win7 可以支援到2020
* 是否要寫 core 自帶的一員檢視器 ，被打槍，因為已經很多區塊鏈檢視器了
* 在討論要不要做 address index，屆時各式各樣的index 都被搬出來說一輪...，是不反對，而且變動不大，但要想清楚sql結構
* 在支援 address index 之前，決定先搞 bip157  bip158

<!-- more --> 

03:00 wumpus: #startmeeting
03:00 lightningbot: Meeting started Thu Dec 13 19:00:20 2018 UTC.  The chair is wumpus. Information about MeetBot at http://wiki.debian.org/MeetBot.
03:00 lightningbot: Useful Commands: #action #agreed #help #info #idea #link #topic.
03:00 moneyball: hi
03:00 wumpus: proposed topic: drop Windows Vista support, make minimum supported Windows 7
03:01 moneyball: just one topic proposed during the week - jamesob
03:01 gmaxwell: wumpus: ping people.
03:01 wumpus: #bitcoin-core-dev Meeting: wumpus sipa gmaxwell jonasschnelli morcos luke-jr sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator aj Chris_Stewart_5 dongcarl gwillen jamesob ken281221 ryanofsky gleb

03:01 provoostenator: (ah well, good way to get more people to review that RNG PR post merge)
03:01 achow101: hi
03:01 meshcollider: hi
03:01 jonasschnelli: hi
03:02 luke-jr: hi
03:02 chenpo: hi
03:02 wumpus: #topic High priority for review
03:02 provoostenator: Let's call the topic Asta la la Vista :-)
03:03 wumpus: https://github.com/bitcoin/bitcoin/projects/8 three PRs left on the list right now: #14336 #14565 #14573
03:03 gribble: https://github.com/bitcoin/bitcoin/issues/14336 | net: implement poll by pstratem · Pull Request #14336 · bitcoin/bitcoin · GitHub
03:03 gribble: https://github.com/bitcoin/bitcoin/issues/14565 | Overhaul importmulti logic by sipa · Pull Request #14565 · bitcoin/bitcoin · GitHub
03:03 gribble: https://github.com/bitcoin/bitcoin/issues/14573 | qt: Add Window menu by promag · Pull Request #14573 · bitcoin/bitcoin · GitHub
03:03 wumpus: provoostenator: good idea
03:03 sipa: hi
03:03 wumpus: the poll one should be (almost?) ready to merge
03:04 provoostenator: Nominating #11082
03:04 gribble: https://github.com/bitcoin/bitcoin/issues/11082 | Add new bitcoin_rw.conf file that is used for settings modified by this software itself by luke-jr · Pull Request #11082 · bitcoin/bitcoin · GitHub
03:04 provoostenator: Needs rebase, but really could use more review before that.
03:04 wumpus: provoostenator: already needs rebase now
03:04 wumpus: (and has, for 24 days)
03:05 jonasschnelli: provoostenator: Maybe take that over from luke-jr
03:05 sipa: does it need concept discussion?
03:05 jonasschnelli: probably...
03:05 provoostenator: I will eventually, but I have 15 other thing on my list. I also think it needs concept discussion.
03:06 luke-jr: it doesn't need taking over, although if someone wants to rebase it sooner, I can push that
03:06 provoostenator: Though we've had IRC chats about it before and everyone seemed to think it was at least a reasonable approach, compared to alterantives.
03:06 wumpus: if it needs concept discussion, it definitely doesn't belong on the high priority for review list
03:06 wumpus: yes, I think it's a reasonable approach
03:06 provoostenator: Alright, maybe add it after rebase?
03:06 wumpus: I dread making init option parsing even more involved, but it's better than the alternatives
03:07 provoostenator: Dynamic wallet loading also needs this to make it good UX.
03:07 sipa: yeah, fair
03:07 wumpus: this needs *very* good tests
03:07 provoostenator: Otherwise you'd have to manually load each time you start.
03:07 sipa: provoostenator: i was expecting that to go in the qt settings
03:07 wumpus: especially for the qt case ast hat's even crazier
03:08 wumpus: how many levels of overlapping options can you have :)
03:08 provoostenator: It has a bunch of Boost tests, but can probably use some QT tests and functional tests.
03:08 wumpus: though this is supposed to get rid of most of the qt settings I guess?
03:08 gmaxwell: obviously we should store what wallets get loaded in wallet.dat...
03:08 jonasschnelli: Overlapping options is already problematic on the QT layer...
03:08 provoostenator: Well, fewer levels thanks to my followup #12833
03:08 luke-jr: wumpus: in a subsequent PR
03:08 sipa: gmaxwell: wahaha
03:08 gribble: https://github.com/bitcoin/bitcoin/issues/12833 | [qt] move QSettings to bitcoin_rw.conf where possible by Sjors · Pull Request #12833 · bitcoin/bitcoin · GitHub
03:09 wumpus: gmaxwell: yesss
03:09 wumpus: luke-jr: right
03:09 provoostenator: But I'm reluctant to add more settings, as that makes rebasing 12833 a pain.
03:09 wumpus: luke-jr: so eventually it'll replace non-pure-user-interface settings in the qt settings, I mean?
03:10 provoostenator: (and that one also needs tests, I haven't delved into how to write QT tests yet, can someone make me a Python framework?)
03:10 luke-jr: wumpus: ideally
03:10 provoostenator: Yeah the idea is to get rid of QTsettings, with the exception of the datadir.
03:10 jonasschnelli: I guess the QT settings files will always be there for window sizes and such... but non critical settings for sure
03:10 wumpus: qtsettings is fine for *ui* settings
03:10 wumpus: such as the last position of the window
03:10 provoostenator: And what jonasschnelli says.
03:10 wumpus: and things like that
03:10 jonasschnelli: indeed
03:10 wumpus: but not for settings shared with the core
03:11 provoostenator: But not stuff that's shared with bitcoind like prune=
03:11 jonasschnelli: yes
03:11 wumpus: such as dbcache, etc
03:11 wumpus: right.
03:11 jonasschnelli: That was just a bypass of not having a way to write to a config section
03:11 luke-jr: ?
03:12 jonasschnelli: We wanted dbcache, proxys in Qt but didn't had a way to write to the config, so we added another layer
03:12 wumpus: yep
03:12 jonasschnelli: Which is no longer a clever approach once we have rw_config
03:12 sipa: i'd be more comfortable if the set of modifiable settings (the list of wallets?) were distinct from those that aren't
03:12 wumpus: we definitely don't want to write to bitcoin.conf directly, but having a separate configuration file that's writable is fine
03:13 sipa: and have the GUI (where you really want everything to be modifable) directly modify bitcoin.conf
03:13 wumpus: noooooo
03:13 wumpus: don't write to bitcoin.conf, never
03:13 sipa: if you use the GUI, the GUI manages the settings
03:13 wumpus: conf should be read only
03:13 sipa: if you don't, the config file does
03:13 wumpus: we've been over this, please
03:13 sipa: right, or have a separate config entirely
03:13 wumpus: let's not change the idea now
03:13 sipa: i really dislike having a UI edit things at the same level as the user is supposed to
03:13 sipa: okay.
03:14 sipa shuts up
03:14 wumpus: we can have this discussion for a few years then never decide to do anything
03:14 provoostenator: There's also a bunch of settings that can go straight into the wallet payload, like RBF and address type (though not their defaults).
03:14 provoostenator: (or maybe even their defaults)
03:15 provoostenator: #13044
03:15 gribble: https://github.com/bitcoin/bitcoin/issues/13044 | [RFC] Long term plan for wallet command-line args · Issue #13044 · bitcoin/bitcoin · GitHub
03:15 jonasschnelli: maybe this also raises the question how to distinct global settings between wallets
03:15 provoostenator: That also simplifies QT, because wallet settings can be updated without any of the QTSettings stuff.
03:16 wumpus: I'm unconfortable with writing to bitcoin.conf directly, as it is specified with -conf, which might point to a read-only configuration file, it should not be assumed it is writable
03:16 wumpus: putting settings in the wallet again?
03:16 gmaxwell: ugh
03:16 sipa: ugh
03:16 wumpus: yea deja vu...
03:16 gmaxwell: putting settings in the wallet I think is even worse now that we have multiwallet.
03:16 jonasschnelli: wumpus: there are the wallet flags now...
03:16 provoostenator: wumpus: yes, that was the idea. Wallets have meta data entries. We already put binary flags in the wallet.
03:16 jonasschnelli: but yeah...not settings
03:17 sipa: provoostenator: originally all settings were in the wallet, it was pretty bad :)
03:17 luke-jr: it might make sense for some subset of settings
03:17 wumpus: sure, wallet-specific metadata should be stored in the wallet
03:17 wumpus: but not settings
03:17 gmaxwell: so you load another wallet and then your software starts behaving differently, madness!
03:17 provoostenator: Yes, obviously only wallet settings.
03:17 jamesob: write to wallet.conf.qt in datadir, have that override -conf settings?
03:17 gmaxwell: yea sure wallet specific metadata sure fine whatever.
03:17 jamesob: *bitcoin.conf.qt
03:17 wumpus: jamesob: that's exactly the idea behind the bitcoin_rw.conf
03:17 jonasschnelli: I just though about address type per wallet,... how do we handle different address types with different wallets?
03:17 luke-jr: eg, you might have a non-segwit wallet, and a segwit wallet
03:17 provoostenator: See the list in the issue I linked to above.
03:17 jonasschnelli: *thought
03:18 jamesob: wumpus: my bad, getting to the meetin glate
03:18 wumpus: jamesob: it contains writable settings which override what is in bitcoin.conf
03:18 wumpus: jamesob: this means being able to edit settings through RPC as well as the GUI
03:18 jamesob: oh cool
03:18 provoostenator: Some of these make sense int he wallet: addresstype, changetype, discardfee, fallbackfee, keypool, mintxfee, paytxfee, txconfirmtarget, etc. For others it doesn't make sense.
03:19 gmaxwell: I don't see how fee settings make much sense in a wallet.
03:19 wumpus: I'm not sure
03:19 gmaxwell: Addresstype I could buy. maybe.
03:19 provoostenator: gmaxwell: to make them behave consistently.
03:19 jonasschnelli: Addresstype certenly,... fees, probably not
03:19 sipa: addresstype will go away in the brave new world future anyway
03:19 wumpus: yes
03:19 gmaxwell: keypool no, it almost could go away.
03:19 jonasschnelli: But I know a lot of people running a SW and a non-SW wallet in parallel
03:19 provoostenator: But maybe fee preferences are more mempool weather dependent than wallet specific.
03:19 gmaxwell: jonasschnelli: sounds brain damaged.
03:20 gmaxwell: jonasschnelli: do you mean they just want to get keys with different address types?
03:20 jonasschnelli: It may be,... but it's just how transition phases happens
03:20 provoostenator: "keypool" might be replaced with a descriptor specific keypool, but I don't think that changes anything. Unless we stop using hardened derivation at the address level.
03:20 wumpus: jamesob: please review #11082 :)
03:20 gribble: https://github.com/bitcoin/bitcoin/issues/11082 | Add new bitcoin_rw.conf file that is used for settings modified by this software itself by luke-jr · Pull Request #11082 · bitcoin/bitcoin · GitHub
03:20 gmaxwell: in any case, changing wallets doesn't change what network you're on, so changing txfee settings doesn't really follow logically.
03:20 sipa: provoostenator: yes keypool will go away as well
03:21 wumpus: gmaxwell: agree
03:21 luke-jr: gmaxwell: maybe if you're worried the wallets will get linked by behaviour?
03:21 gmaxwell: provoostenator: keypool was configurable in the first place because it interacted with backup durability.
03:21 jonasschnelli: gmaxwell: I guess they want a SW wallet that derives P2SH(P2WPKH) and and their old wallet that derives P2PKH... (and not mix them)
03:21 jamesob: wumpus: roger that
03:21 provoostenator: I do like the idea of giving config / rw_config wallet specific sections.
03:21 wumpus: scoping settings on the wallet will be confusing for users, should imo be avoided if possible
03:22 gmaxwell: provoostenator: so it's not clear to me that forward caching of keys would be configurable in the future, or at least that it would be anything but an advanced thing that users usually shouldn't mess with.
03:22 wumpus: if anything it's very difficult to come up with a good user interface for that
03:22 sipa: i think all of those can either be reasonably done at the node level, or turn into descriptor-specific things in the wallet (and thus not need config)
03:22 provoostenator: gmaxwell: ah I see, making it "just work" could make sense
03:22 luke-jr suggests ignoring wallet-specific settings for initial rwconf purposes <.<
03:22 wumpus: luke-jr: yes, I agree
03:22 gmaxwell: yea agreed.
03:23 wumpus: luke-jr: one step at a time
03:23 wumpus: we've been on this step for years
03:23 wumpus: every time it's the same discussion, though I haven't heard the idea of settings in the wallet seriously proposed for a while :)
03:23 gmaxwell: to the extent that there are wallet specific things they probably should be in the wallet so they move with the wallet.  Regardless, they don't need to be part of the rwconf discussion.
03:24 provoostenator: Agree regarding getting rwconf out the door without adding anything to it.
03:24 jonasschnelli: wumpus: since its only addresstype that may be relevant and will go away over time,... I take back the argument that settings per wallet are relevant
03:24 wumpus: jonasschnelli: thank you
03:25 gmaxwell: (I'm just doubtful that there actually are more than a couple wallet specific things, addresstypes seem the most realistic of the ones mentioned here)
03:25 provoostenator: Indeed, that seems the most important thing to keep consistent per wallet for privacy reasons.
03:25 jonasschnelli: boolean things like disable-privatekeys can be handles with the 64bit wallet flags
03:25 jonasschnelli: *handled
03:26 provoostenator: One day everyone will send to bech32 addresses, and then we'll do v1 SegWit to start the problem over again :-)
03:26 sipa: jonasschnelli: even that we don't need post descriptors
03:26 wumpus: at the least, settings that are part of the wallet *should not* be part of the global options sytem
03:26 wumpus: otherwise it just becomes too many levels
03:26 sipa: you'd just not a have a descriptor with private keys if you don't want private keys
03:26 gmaxwell: provoostenator: no, because v1 segwit doesnt' change the address type, bech32 already supports it.
03:26 gmaxwell: (shocking, we already anticipated that problem... :P )
03:27 luke-jr: gmaxwell: but p2sh^2 could (independnetly of segwitv1)
03:27 gmaxwell: provoostenator: I'm sure there will be some broken sites, but it should be much less of an issue.
03:27 jonasschnelli: sipa: is that similar of saying "you don't need to import private keys if you don't want to have private keys"?
03:28 jonasschnelli: disable-private key seems to be another layer,... a footgun protection. But seems like we are going OT
03:28 sipa: jonasschnelli: it would turn no-private-keys into a flag for wallet creation perhaps, to determine what descriptors a new wallet is born with; but it wouldn't affect anything later
03:28 provoostenator: gmaxwell: but you still don't want to e.g. consistently use or not use schnorr, so you still need to maintain a preference. Even if it's all bech32.
03:28 provoostenator: *do want
03:28 luke-jr: so back to rwconf.. <.<
03:28 sipa: anyway, sure - we could keep it as a footgun protection, but it seems kind of pointless
03:28 gmaxwell: provoostenator: yes but thats just a property of which keys/descriptors are in the wallet.
03:28 sipa: yeah, getting offtopic, sorry
03:28 provoostenator: gmaxwell: good point
03:28 wumpus: I think it's time to move to the next topic
03:29 provoostenator: Descriptors are very useful.
03:29 meshcollider: sipa: I assume you'd still need a way to fail if you try and import private keys though
03:29 provoostenator: That's the foodgun protection.
03:29 provoostenator: footgun
03:30 provoostenator: I see two topics proposed here https://gist.github.com/moneyball/071d608fdae217c2a6d7c35955881d8a
03:30 provoostenator: jamesob and moneyball
03:30 wumpus: #topic Asta la la Vista
03:30 jamesob: Terminator movies?
03:31 provoostenator: Dropping Vista support
03:31 wumpus: so the idea to move the minimum supported windows to W7 recently came up in #14922
03:31 gribble: https://github.com/bitcoin/bitcoin/issues/14922 | [WIP] windows: Set _WIN32_WINNT to 0x0601 (Windows 7) by ken2812221 · Pull Request #14922 · bitcoin/bitcoin · GitHub
03:31 sipa: vista extended support ended on april 11, 2017
03:31 wumpus: apparently this was already changed in the release notes #12546
03:31 gribble: https://github.com/bitcoin/bitcoin/issues/12546 | [docs] Minor improvements to Compatibility Notes by randolf · Pull Request #12546 · bitcoin/bitcoin · GitHub
03:31 sipa: end of mainstream support was in 2009
03:31 luke-jr: for Linux, we just support latest stable distros, so if we mirror that for Windows, we can move to Win10 :P
03:32 sipa: it was also one of the least popular windows releases...
03:32 wumpus: so I think dropping support for Vista is pretty non-controversial
03:32 wumpus: yes
03:32 wumpus: it wasn't even popular at the time
03:32 achow101: +1
03:32 jonasschnelli: ack
03:32 meshcollider: Yep
03:32 sipa: so i think there is no real to keep it
03:32 provoostenator: I'm a Mac fanboy, so conflict of interest :-)
03:32 sipa: i actually expect less opposition than the opposition we got from dropping XP support
03:33 gmaxwell: People are still using XP, I think less so than vista.
03:33 luke-jr: sipa: this may be the first time we actually break XP, note
03:33 wumpus: luke-jr: W7 is still used quite a lot by people unwilling to move to W10
03:33 gmaxwell: er more so than vista.
03:33 gmaxwell: the bigger issue will be W10 which is kinda spyware land windows from what I'm told.
03:33 wumpus: yes
03:33 meshcollider: Most people consider W7 as a strict improvement over vista so there should be minimal resistance :)
03:33 sipa: is there anything between w7 and w10?
03:33 luke-jr: 8.1
03:34 wumpus: there's a windows 8 but I don't think it ever caught on much
03:34 sipa: ah yes
03:34 sipa: anyway, ack dropping vista support
03:34 wumpus: ok
03:35 sipa: based on what i read; not a windows user myself
03:35 gmaxwell: that PR will it make it actually not work when it does otherwise?
03:35 bitcoin-git: [bitcoin] MarcoFalke opened pull request #14953: test: Make g_insecure_rand_ctx thread_local (master...Mf1812-testThreadLocal) https://github.com/bitcoin/bitcoin/pull/14953
03:35 MarcoFalke: Should fix the thread sanitizer issue ^
03:35 gmaxwell: That isn't what we mean by supported on other platforms, on linux if you want to try running on really old stuff, you can try but you're own your own.
03:35 wumpus: yes it sets the minimum API level so that it won't start in <W7, and makes it possible to use newer APIs
03:35 luke-jr pokes MarcoFalke
03:36 gmaxwell: ah it gates newer APIs.  Is there a reason to not announce we don't support vista, but only bump that flag when we actually go to use one of those apis?
03:36 gmaxwell: (just blocking software where it otherwise works doesn't really feel in the spirit of open source)
03:36 wumpus: you're pedaling back now?
03:36 luke-jr: gmaxwell: IIRC some PR wants to use Win7 API
03:37 gmaxwell: luke-jr: okay.
03:37 wumpus: FWIW qt is also going to break vista support
03:37 luke-jr: I did suggest making the change in *that* PR..;
03:37 wumpus: this is for 0.18
03:37 wumpus: which is still a few months away
03:37 gmaxwell: wumpus: no wumpus, I'm not "pedaling back"   but the logic given above that we don't support older linux doesn't actually apply to actively breaking older windows.
03:37 gmaxwell: If it's going to be broken by other changes in any case, thats fine then.
03:37 luke-jr: eg, ionice_win bumps the Windows API version too, but wasn't merged yet
03:37 wumpus: gmaxwell: fair enough but luke-jr was talking about supporting *only* windows 10
03:38 wumpus: which is kind of extreme
03:38 wumpus: W7 as bottom should be in line with all modern software
03:38 luke-jr: wumpus: just mentioning it as a comparison to how we handle Linux distros ;)
03:38 gmaxwell: from all I've heard running bitcoin on windows 10 sounds like it's probably a bad idea in general.
03:38 meshcollider: From the PR, "#14881 is using inet_pton and it's only for Vista or later. So I create this PR just for that."
03:38 gribble: https://github.com/bitcoin/bitcoin/issues/14881 | Tests: Contract testing for the procedure AddTimeData by mmachicao · Pull Request #14881 · bitcoin/bitcoin · GitHub
03:39 gmaxwell: wumpus: okay, concern withdrawn. I just thought it would be sad to gratitiously break it, but since we have a reason to to do, good to go.
03:39 luke-jr: gmaxwell: but only Windows 10 is actually supports anymore IIRC
03:39 wumpus: luke-jr: yes, I know it was not seriously, but would be in line with what we do for wsay, MacOSX, but mac users like upgrading a lot more than windows users
03:39 luke-jr: supported*
03:39 wumpus: luke-jr: what does microsoft still officially support? only W10? are you sure?
03:40 luke-jr double checks
03:40 luke-jr: Win 8.1: Mainstream support ended on January 9, 2018
03:40 luke-jr: apparently you can pay for support until 2023
03:40 achow101: windows 7 will have security updates until jan 2020
03:40 wumpus: great
03:41 luke-jr: maybe I misunderstand extended support
03:41 luke-jr: Win 7: Mainstream support ended on January 13, 2015. Extended support until January 14, 2020 (January 2023 for Professional and Enterprise, users will need to pay for security updates).[5][6]
03:41 wumpus: so w7 is still more or less relevant
03:41 achow101: yes
03:42 achow101: and i'm pretty sure a lot of people still use it too
03:42 wumpus: right
03:42 wumpus: let's move to next topic
03:42 wumpus: #topic "add address index" PRs (jamesob)
03:43 jamesob: I've talked to a number of companies who're clamoring for an address index and we've got four attempts buuuut
03:43 jamesob: sipa has potentially disabused me of the notion that an addr index is a legitimate approach to just about anything that isn't debugging or analysis
03:43 jonasschnelli: jamesob: you mean unspent address index?
03:44 jamesob: sure, or a more general script descriptor index
03:44 jonasschnelli: I agree with sipa
03:44 achow101: jamesob: for what are the companies trying to use an address index for?
03:44 wumpus: an address index over the full block chain never was a good idea, one over the utxo set was considered but never made itin yet
03:44 jamesob: in any case, I think we should have some sort of recommendation (and ideally a maintained piece of software) to recommend to the folks who want to do addr-indexy thing
03:44 jamesob: s
03:45 luke-jr: jamesob: "don't do that" :p
03:45 gmaxwell: I think unspents indexes are fine, generally, but shouldn't be a priority for the project over other concerns.. if someone wants to come and do the work for them, and to do them well, great.
03:45 jamesob: achow101: afaict mostly watching for activity on various addresses
03:45 jonasschnelli: jamesob: you could do the address index externaly via p2p..... look at https://github.com/jonasschnelli/bitcoincore-indexd (experiment)
03:45 provoostenator: Always happy to test and review those address index PRs. I think that on top of the new index scheme it's not too bad to maintain.
03:45 luke-jr: what if we have a full TXO/script index, and only expose it in the GUI as a block explorer? (ie, no RPC to be abused)
03:45 gmaxwell: jamesob: our general recommendation for watching is to import them into a watching wallet.
03:45 wumpus: *watcing activiity* shouldn't require an index of everything over the whole block chain
03:45 provoostenator: Or we could come up with a plugin system for indexes, though that's also a can of worms.
03:45 jamesob: jonasschnelli: indeed, as well as projects like electrs
03:46 wumpus: wasn't there some external project addressing this?
03:46 jonasschnelli: I think we should not load a complete address index on the shoulders of Core
03:46 gmaxwell: jamesob: and I think if there are limitations on importing for watching, we'd like to improve those.
03:46 luke-jr: provoostenator: I thought we had that now
03:46 sipa: gmaxwell: yup!
03:46 wumpus: it's a *huge* database in any case
03:46 jonasschnelli: But I agree, externally makes it a bit more complex
03:46 jamesob: in the next few weeks I'm going to be getting in touch with companies to get a more concrete idea of the usecases, so I'll report back with what I find
03:46 provoostenator: luke-jr: have what? People can compile their own client of course, but that's pretty high bar and can easily lead to rebase nightmares.
03:47 wumpus: bitcoin core is not meant as a chain analysis platform
03:47 luke-jr: wumpus: I did it in ~2 GB a year or so ago, IIRC
03:47 wumpus: you can do forensics using your own tools
03:47 jamesob: wumpus: very much agree
03:47 gmaxwell: jonasschnelli: right the problem for externally, is that implementing blockchain consistency is non-trivial and in my expirence most people who want to build an index don't want to deal with that.
03:47 gmaxwell: jamesob: more information on the actual usecases would be very helpful.
03:47 wumpus: it's non trivial but not rocket science either
03:47 jonasschnelli: Sadly people expect fast BIP44 recovery (incl. history). This seems to be the most prominent real-world usecase for an address index
03:48 wumpus: it shouldn't be that anything non-trivial needs to end up[ in bitcoin core
03:48 wumpus: we're not the world of non-trivial solutions
03:48 gmaxwell: jonasschnelli: most (I believe most, many at least) electrum servers don't do history, so I'm not entirely clear on the including history part of your comment.
03:48 provoostenator: Let's also not forget to update #14053 with concept ACK / NACK so people don't waste time on trying it if it's undesirable.
03:48 gmaxwell: wumpus: heh.
03:48 gribble: https://github.com/bitcoin/bitcoin/issues/14053 | Add address-based index (attempt 4?) by marcinja · Pull Request #14053 · bitcoin/bitcoin · GitHub
03:48 jonasschnelli: gmaxwell: IMO they do (index everything)
03:49 jonasschnelli: (not electrum personal server though)
03:49 wumpus: I mean this is another thing that's been *years*
03:49 gmaxwell: jonasschnelli: no, I know that for a fact-- many electrum servers don't index history.
03:49 wumpus: really, no one has been able to build a solution to this?
03:49 gmaxwell: (I just don't know if its most of them)
03:49 wumpus: not one of all those companies that want it?
03:49 jamesob: provoostenator: and its sibling #14035
03:49 luke-jr: wumpus: people capable of it don't want it :p
03:49 gribble: https://github.com/bitcoin/bitcoin/issues/14035 | Utxoscriptindex by mgrychow · Pull Request #14035 · bitcoin/bitcoin · GitHub
03:49 sipa: wumpus: blockstream.info uses electrs, which seems to work very well
03:49 gmaxwell: wumpus: I think the process of learning enough to do it well does a pretty good job of convincing you that you don't want it.
03:49 wumpus: gmaxwell: heh
03:49 provoostenator: jonasschnelli: BIP44 recovery can be handled once we have descriptor support for importmulti and slightly more sane behavior (or a replacement for) the keypool.
03:50 wumpus: sipa: that's a good suggestion then!
03:50 gmaxwell: provoostenator: history recovery requires a scan of the chain, or a phenominally expensive index.
03:50 jonasschnelli: provoostenator: you can't recover the history without an address index or a complete rescan (which is not possible for pruned peers)
03:50 wumpus: https://github.com/romanz/electrs
03:50 provoostenator: Ok, rescan for pruned nodes isn't there yet.
03:50 gmaxwell: jonasschnelli: note that an index is also not compatible with pruning. :P
03:50 wumpus: alrady had it bookmarked apparently :)
03:50 jonasschnelli: The only light here is the scantxoutset where you can recover within seconds but not the spent-history
03:51 provoostenator: Though you could use the neutrino filters for that and then refetch the relevant blocks.
03:51 jonasschnelli: gmaxwell: it could be,... if we just keep the pointers and load the data via p2p once requested
03:51 gmaxwell: jonasschnelli: I think we'd get a lot more bang for our buck working on making 'wallet without history before x' (pruned wallet) a first class supported thing.
03:51 jonasschnelli: gmaxwell: completely agree on this
03:51 gmaxwell: jonasschnelli: transfering 200GB of data to do the input is not really reasonable...
03:52 gmaxwell: (and then not saving it... this would be pretty harmful to the p2p network if people were actually patient enough to use it. :) )
03:52 jonasschnelli: gmaxwell: I mean there is a PR that enabled txindex with pruning... and fetches the tx over p2p once requested outside the kept block area
03:52 jonasschnelli: which is slow.... but for debugging proposes okay
03:52 luke-jr: (this makes me think again of the concept of prune-to-slow-storage where you can plug in a USB drive when/if you need old data..)
03:52 gmaxwell: jonasschnelli: oh, I didn't recall that PR.
03:53 wumpus: luke-jr: prune-to-tape *hides*
03:53 provoostenator: luke-jr: slow storage being the internet? :-)
03:53 jonasschnelli: #13014
03:53 gribble: https://github.com/bitcoin/bitcoin/issues/13014 | Allow txindex in prune mode by jonasschnelli · Pull Request #13014 · bitcoin/bitcoin · GitHub
03:53 luke-jr: provoostenator: could be local
03:53 gmaxwell: jonasschnelli: bip 157 filtering could be used similarly.
03:54 gmaxwell: jonasschnelli: e.g. saved the bip157 filters locally, and scan against them.
03:54 jonasschnelli: yes... less disk space, more time spent on filtering... but same idea
03:54 luke-jr: hmm
03:54 luke-jr: what data do they want returned from the index? maybe we don't need to retain/fetch the block
03:55 luke-jr: eg, if the client would be happy with a list of block numbers or txids..
03:55 jamesob: are any of the BIP157/158 PRs on the high prio list? if not, they should be
03:55 gmaxwell: wumpus: sadly, freeking tape costs about as much as HDDs today...  LTO7 tapes (6TB) cost about $70.
03:55 wumpus: gmaxwell: ouch
03:55 provoostenator: So the wallet recovery flow would be: add descriptors, download BIP-157 filters (if you didn't keep them), process filters, fetch a few blocks. User can immediately use their wallet to receive and send.
03:55 wumpus: gmaxwell: I guess they're more reliable though
03:55 luke-jr: jamesob: making light wallets stronger has a negative impact on Bitcoin :/
03:56 gmaxwell: provoostenator: I don't really think thats a viable long term workflow either...  rather if you couldn't afford the space to keep them you probably don't want the time/bandwidth to download them.
03:56 sipa: luke-jr: BIP158 helps our local wallet too
03:56 provoostenator: luke-jr: not making them possible sends most people to web wallets, not to full nodes.
03:56 jamesob: luke-jr: better light wallets might help adoption
03:56 gmaxwell: luke-jr: I'm only interested in it for the local wallets.
03:57 luke-jr: jamesob: better to not have that adoption..
03:57 luke-jr: sipa / gmaxwell: yes, that's a point
03:57 provoostenator: gmaxwell: recovery should be a rare thing anyway, I assume it only happens after a disaster. In which case you'd probably download the whole chain again anyway.
03:57 sipa: provoostenator: it should be.
03:57 gmaxwell: jamesob: history has shown otherwise, bip158 doesn't make lite wallets fundimentally more usable than they are now.  They're still massively worse than server driven wallets like electrum or web wallets.
03:58 gmaxwell: provoostenator: right but thats also a reason that fetching them when you don't have them isn't that interesting, IMO.
03:58 jamesob: good point - but I guess if existing light wallets switched to bip157 it'd at least ease load on existing full nodes
03:58 gmaxwell: jamesob: what light wallets?
03:58 provoostenator: gmawell is that _because_ of bip158 or just because there aren't that many developers working on light (non web, non electrum) wallets? That could change over time.
03:58 wumpus: 1 minute to go
03:59 jamesob: anything using bloom-filter-based SPV
03:59 gmaxwell: jamesob: at least connections I see there is virtually no acutal usage of p2p lite wallets anymore.
03:59 wumpus: please wrap up the meeting
03:59 jamesob: I'll report on any compelling usecases I find for addr index, but I suspect sipa et al are right that that's usually just the Wrong way
03:59 gmaxwell: provoostenator: P2p lite wallets that scan the chain just end up with a very poor user expirence.
04:00 jamesob: in the meantime I recommend we give concept ACK/NACK to outstanding PRs which are related
04:00 gmaxwell: and that doesn't really have anything to do with bip158 vs bip37.
04:00 gmaxwell: (in fact BIP158 is somewhat worse, but slightly less of a privacy disaster)
04:00 wumpus: #endmeeting
04:00 lightningbot: Meeting ended Thu Dec 13 20:00:37 2018 UTC.  Information about MeetBot at http://wiki.debian.org/MeetBot . (v 0.1.4)
04:00 lightningbot: Minutes:        http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-13-19.00.html
04:00 lightningbot: Minutes (text): http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-13-19.00.txt
04:00 lightningbot: Log:            http://www.erisian.com.au/meetbot/bitcoin-core-dev/2018/bitcoin-core-dev.2018-12-13-19.00.log.html
04:01 provoostenator: gmaxwell: I was thinking mostly about Lightning wallets that rely on a lightweight wallet but don't have support for on chain (other than topping up channels). Those don't need to care about unconfirmed transactions.
04:01 wumpus: jamesob: I think poeople have become tired of arguing, or even explicitly NACKing those things
04:01 gmaxwell: (it's worse because it takes a client more time to scan the chain than with BIP37, as it has to get quite a bit more data)
04:01 gmaxwell: wumpus: +1
04:02 jamesob: wumpus: makes sense. I'll come up with a reply to both PRs that tries to explain why they're not a fit for core
04:02 wumpus: at least I have, I mean, if you've been in this since 2011 or so, and have to keep telling people something is abad idea while it becomes ever a worse idea (due to block chain growth)
04:02 jamesob: and maybe we can think about adding something to the developer guidelines about indexing
04:02 gmaxwell: UTXO-iyx indexes I generally concept ack (at least if they're ones that aren't specific about 'addresses' but work for spk's generally), history ones, I have NAKed.
04:02 wumpus: gmaxwell: yep
04:03 sipa: provoostenator: yes, i think BIP157 may be useful for a new class of clients that may become popular