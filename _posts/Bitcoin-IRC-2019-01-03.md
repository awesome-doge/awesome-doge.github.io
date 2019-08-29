---
title: Bitcoin IRC 2019.01.03
date: 2019-01-04 21:24:34
tags: [Bitcoin IRC, bitcoin]
categories: Bitcoin IRC Meeting
---

19:01:48 wumpus: #startmeeting
19:01:48 lightningbot: Meeting started Thu Jan  3 19:01:48 2019 UTC.  The chair is wumpus. Information about MeetBot at http://wiki.debian.org/MeetBot.
19:01:48 lightningbot: Useful Commands: #action #agreed #help #info #idea #link #topic.
19:01:54 moneyball: happy 10 year genesis block
19:02:07 meshcollider: hi
19:02:07 jonasschnelli: \o/
19:02:17 wumpus: #bitcoin-core-dev Meeting: wumpus sipa gmaxwell jonasschnelli morcos luke-jr sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator aj Chris_Stewart_5 dongcarl gwillen jamesob ken281221 ryanofsky gleb

<!-- more --> 

19:02:29 jamesob: hi
19:02:32 promag: hi
19:02:35 instagibbs: happy 10 years wumpus, who i assume is satoshi
19:02:36 wumpus: yes \o/
19:02:45 instagibbs: hi
19:02:48 wumpus: lol instagibbs
19:04:11 wumpus: #topic high priority for review
19:05:33 wumpus: #11082 #14491 #14941
19:05:36 gribble: https://github.com/bitcoin/bitcoin/issues/11082 | Add new bitcoin_rw.conf file that is used for settings modified by this software itself by luke-jr Â· Pull Request #11082 Â· bitcoin/bitcoin Â· GitHub
19:05:39 gribble: https://github.com/bitcoin/bitcoin/issues/14491 | Allow descriptor imports with importmulti by MeshCollider Â· Pull Request #14491 Â· bitcoin/bitcoin Â· GitHub
19:05:40 wumpus: are the current PRs
19:05:40 phantomcircuit: hi
19:05:41 gribble: https://github.com/bitcoin/bitcoin/issues/14941 | rpc: Make unloadwallet wait for complete wallet unload by promag Â· Pull Request #14941 Â· bitcoin/bitcoin Â· GitHub
19:05:58 wumpus: promag would like to add #14941
19:06:00 gribble: https://github.com/bitcoin/bitcoin/issues/14941 | rpc: Make unloadwallet wait for complete wallet unload by promag Â· Pull Request #14941 Â· bitcoin/bitcoin Â· GitHub
19:06:06 wumpus: eh wait, that's already on there?
19:06:09 jamesob: can I nominate jimpo's BIP157/8-related PRs that've been hanging out for a while? maybe starting with #14111?
19:06:11 gribble: https://github.com/bitcoin/bitcoin/issues/14111 | index: Create IndexRunner class for activing indexes. by jimpo Â· Pull Request #14111 Â· bitcoin/bitcoin Â· GitHub
19:06:13 promag: fanquake added
19:06:42 achow101: #15006
19:06:43 gribble: https://github.com/bitcoin/bitcoin/issues/15006 | Add option to create an encrypted wallet by achow101 Â· Pull Request #15006 Â· bitcoin/bitcoin Â· GitHub
19:07:24 jamesob: also ryanofsky's next step in the process separation project, #14711
19:07:26 gribble: https://github.com/bitcoin/bitcoin/issues/14711 | Remove uses of chainActive and mapBlockIndex in wallet code by ryanofsky Â· Pull Request #14711 Â· bitcoin/bitcoin Â· GitHub
19:07:27 achow101: I guess #14938 should go first as 15006 depends on it
19:07:30 gribble: https://github.com/bitcoin/bitcoin/issues/14938 | Support creating an empty wallet by Sjors Â· Pull Request #14938 Â· bitcoin/bitcoin Â· GitHub
19:09:17 wumpus: #14938 first then?
19:09:19 gribble: https://github.com/bitcoin/bitcoin/issues/14938 | Support creating an empty wallet by Sjors Â· Pull Request #14938 Â· bitcoin/bitcoin Â· GitHub
19:09:19 wumpus: right
19:09:23 jonasschnelli: yes
19:10:29 jamesob: oops I'm sorry -- that jimpo PR isn't critical path for BIP157; I meant #14085
19:10:31 gribble: https://github.com/bitcoin/bitcoin/issues/14085 | index: Fix for indexers skipping genesis block. by jimpo Â· Pull Request #14085 Â· bitcoin/bitcoin Â· GitHub
19:10:33 wumpus: ok added the mentioned ones
19:10:52 wumpus: jamesob: ok, will replace it then
19:11:05 jamesob: wumpus: thanks. fwiw ultimately I'm after #14121, but that PR is a dep
19:11:08 gribble: https://github.com/bitcoin/bitcoin/issues/14121 | Index for BIP 157 block filters by jimpo Â· Pull Request #14121 Â· bitcoin/bitcoin Â· GitHub
19:11:42 wumpus: right, better to put that one then, the idea of high priority for review is PRs that are dependencies of others
19:12:50 wumpus: https://github.com/bitcoin/bitcoin/projects/8
19:13:12 wumpus: #topic having users create their wallets instead of automatically creating a default wallet (achow101)
19:13:40 achow101: this was discussed briefly when I first mentioned it
19:13:44 jonasschnelli: I like the concept
19:13:56 achow101: the end goal is to make wallets that were "born encrypted"
19:14:08 luke-jr: I suspect it may be confusing to some users
19:14:30 wumpus: I think both should be possible
19:14:37 jonasschnelli: I don't think it confuses users... we could still trigger the "create" wallet process at first launch in the GUI
19:15:09 wumpus: ideally, if you want the default wallet, that's fine, if you want to create something customized and start with nothing, that should be possible
19:15:43 jonasschnelli: but that sounds after a lot of configuration options.. do you mean a -nodefaultwallet options?
19:15:45 wumpus: I think having to set an encryption key at first used has been argued against in the past though
19:16:08 achow101: My idea is to get rid of the default wallet entirely. I don't think there really should be a default wallet
19:16:29 meshcollider: Can't a default wallet setup box or something pop up like the datadir one on first launch
19:16:39 achow101: and having the default wallet with createwallet can be confusing. users may mistakenly send things to the default wallet when they meant to use some other wallet
19:16:43 wumpus: meshcollider: exactly; that could be skippable
19:16:48 jonasschnelli: I agree... wallets should probably created intentionally since its an important data file
19:17:06 gmaxwell: jonasschnelli: doing something automatically on first _launch_ would largely defeat the point.
19:17:22 gmaxwell: jonasschnelli: the behavior I've been recommending is triggering it when the user attempts to get an address.
19:17:26 jonasschnelli: gmaxwell: only in the GUI (wizzard) ....
19:17:34 wumpus: I think changing this is too late for 0.18
19:17:38 gmaxwell: jonasschnelli: yes, that still defeats the point.
19:17:41 jonasschnelli: though I'm not convince... only if we "confuse" users with removing the default wallet
19:17:58 achow101: gmaxwell: so I investigated the create wallet on use stuff before and I think it would be rather fragile or require a lot more refactoring
19:18:12 jonasschnelli: But yeah,.. I agree with you gmaxwell
19:18:21 gmaxwell: achow101: But do you not agree that it's the right behavior?
19:18:34 promag: gmaxwell: also for rpc clients?
19:19:07 achow101: gmaxwell: yes. but I think that having the user explicitly create the wallet is a suitable replacement too
19:19:27 gmaxwell: promag: I have less strong opinions on that, I could go either way.  The RPC can't prompt you to answer more questions (like encryption), while the gui can.
19:19:57 wumpus: but for RPC the client could use createwallet explicitly to create the first wallet
19:19:58 ryanofsky: Will add my +1 for Greg's idea. I think creating a default wallet when needed is more user friendly.
19:20:03 gmaxwell: achow101: what exactly does that mean?  do you mean getnewaddress should be missing from the UI otherwise, or it should silently fail?
19:20:09 promag: gmaxwell: I'd love to remove the implicit wallet endpoint
19:20:43 jonasschnelli: When the wallet is auto-creating when it's needed, there is (probably) no place for additional options
19:20:46 achow101: gmaxwell: i mean that getnewaddress would give you an error saying "do createwallet first"
19:20:54 gmaxwell: achow101: because if the GUI would offer the options but pop up a message, then that could simply start wallet creation: so I don't see where the additional refactoring comes in there for the gui.
19:21:26 wumpus: this is similar to say, SQL servers, they don't usually create a default database either but assume the client will create one
19:21:50 wumpus: for RPC that makes perfect sense, for the GUI, I don't know
19:22:07 promag: achow101: not only that imo, all wallet methods
19:22:08 achow101: gmaxwell: in the gui, i imagine it would be like the disablewallet ui but a button that says "click here to make a wallet"
19:22:22 gmaxwell: promag: if the endpoint is gone, then users will just get a command not found. We can do that, but kinda lugly.
19:22:41 jonasschnelli: I think the GUI with no wallet will require (decent) refactoring to show the receive tab in order to let the user click on "new address"
19:22:50 gmaxwell: achow101: If it's made conspicious enough, thats fine with me I suppose.
19:23:07 gmaxwell: We just need to be careful to not make the software unusable for new users.
19:23:13 wumpus: gmaxwell: that is an implementation detail depending on how it's handled, it could just as well return a message to create a wallet first
19:23:28 achow101: the point is that it's going to be totally obvious that you need to make a new wallet. there shouldn't be any magic in the background
19:23:30 gmaxwell: like they shouldn't have to dig through menus to make expected options appear or anything like that.
19:23:34 jonasschnelli: Why not do it like other wallets,... if the GUI detects no wallet, allow to load or create a wallet
19:23:49 wumpus: jonasschnelli: exactly
19:23:58 wumpus: that makes perfect sense for the GUI
19:24:01 gmaxwell: jonasschnelli: when?
19:24:09 wumpus: at start, when there's no wallet.dat
19:24:12 luke-jr: maybe after the first-launch screen it should open some new wallet wizard with a Skip button
19:24:19 jonasschnelli: When the GUI loads and no wallet has been detected (but was compiled with wallet support)
19:24:22 jonasschnelli: Ask: new / open
19:24:24 wumpus: and no -disablewallet or -nowallet or such was specified
19:24:30 jonasschnelli: yes
19:24:36 gmaxwell: The point of not creating the wallet on start is so that the wallet will not be created unencrypted, and also so that you don't end up with a lot of unusued wallet files laying around.
19:24:47 wumpus: gmaxwell: right
19:24:58 wumpus: that's one advantage of never creating wallet.dat without prompting
19:25:05 gmaxwell: And you don't prompt for an encrypted key at initial start because users will set something random forget it, then months later send funds to it.
19:25:17 achow101: gmaxwell: that would be part of the ui prompt
19:25:28 jonasschnelli: That is a critical point
19:25:31 achow101: gmaxwell: something like what electrum does on its first start
19:25:38 gmaxwell: (Electrum insututed a complicated UI flow that forces users to write down a recovery code to address that issue)
19:25:44 promag: gmaxwell: actually I'm working on "File -: Reopen Wallet -: ..." which requires saving a history.. if this is empty it could prompt the wizard
19:26:20 jonasschnelli: Electrum is too much handholding IMO
19:26:51 gmaxwell: Electrum's behavior was driven by massive amounts of funds loss that happened when prompting users for encryption keys months before using the wallet.
19:27:16 wumpus: it'd be possible to skip wallet creation completely
19:27:23 jonasschnelli: That would speak for the create-on-first-new-address
19:27:35 gmaxwell: jonasschnelli: or just having a clear create button.
19:27:38 achow101: as I said earlier, I think the ideal solution would be to just have a button in the main ui that says "click here to make a wallet"
19:27:43 gmaxwell: Or having error messages on use that tell you to create.
19:28:00 wumpus: yes that was suggested, show the GUI in zero-wallet mode and have a 'create wallet' mode
19:28:01 gmaxwell: Though if you are going to have an error message, it could just start the create dialog.
19:28:13 wumpus: button
19:28:23 luke-jr: use the webcam to make the user prove they wrote down the passphrase /s
19:28:28 gmaxwell: That sounds okay to me, the implementation just needs to be conspicious.
19:28:33 jonasschnelli: Ideally the GUI is completely usable (explore) without a wallet... and the wallet is created on first address
19:28:35 promag: regarding the -wallet arg, should it stay "load or create"?
19:28:38 wumpus: luke-jr: doesn't everyone have a sticker over those xD
19:28:52 gmaxwell: luke-jr: electrum disables copy/paste and then makes you reenter on another screen. less computer vision required. :P
19:29:25 gmaxwell: promag: probably load or create, maybe introduce a -walletfile that doesn't create?
19:29:45 gmaxwell: and consider depricating the create version later?
19:30:10 luke-jr: gmaxwell: I've always found that super annoying for network passwords (but haven't given it a lot of thought for wallet passphrases, or seeds) since it prevents password management
19:30:10 achow101: promag: imo it should just be a load option. no create
19:30:38 phantomcircuit: gmaxwell, i have so many completely empty wallet files backed up it's silly
19:30:56 achow101: promag: maybe even error when the wallet file can't be found to load
19:31:18 promag: achow101: maybe lazy creation - on actual usage?
19:31:39 wumpus: I think we're starting to go in circles
19:31:51 jonasschnelli: jup
19:31:54 wumpus: any other topics?
19:32:11 promag: anyway, too late for 0.18, and too many breaking changes
19:32:37 wumpus: yes, let's aim to have the creat-with-password RPC in 0.18, but don't change any defaults
19:32:54 jonasschnelli: ack
19:34:06 promag: I'd like some feedback here #14941, so far only ryanofsky reviewed
19:34:08 gribble: https://github.com/bitcoin/bitcoin/issues/14941 | rpc: Make unloadwallet wait for complete wallet unload by promag Â· Pull Request #14941 Â· bitcoin/bitcoin Â· GitHub
19:34:59 wumpus: #action review #14941
19:35:01 gribble: https://github.com/bitcoin/bitcoin/issues/14941 | rpc: Make unloadwallet wait for complete wallet unload by promag Â· Pull Request #14941 Â· bitcoin/bitcoin Â· GitHub
19:36:15 wumpus: ok if there's no other topics, let's close the meeting early
19:36:18 gmaxwell: achow101: error on failure is nice.
19:37:02 promag: o/
19:37:44 wumpus: yes, having it wait for the unload before returning is certainly better conceptually, having it asynchronous only causes complexity
19:38:21 wumpus: (and indeed, leaves no way to return errors)
19:39:03 wumpus: #endmeeting