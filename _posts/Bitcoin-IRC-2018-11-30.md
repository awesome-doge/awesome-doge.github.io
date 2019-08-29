---
title: Bitcoin IRC 2018.11.30
date: 2018-11-30 03:13:00
tags: [Bitcoin IRC, bitcoin]
categories: Bitcoin IRC Meeting
---

(英文)
03:00 wumpus: #startmeeting
03:00 lightningbot: Meeting started Thu Nov 29 19:00:25 2018 UTC.  The chair is wumpus. Information about MeetBot at http://wiki.debian.org/MeetBot.
03:00 lightningbot: Useful Commands: #action #agreed #help #info #idea #link #topic.
03:00 sipa: oh, meeting!
03:00 dongcarl: hi
03:00 moneyball: hi
03:01 wumpus: #bitcoin-core-dev Meeting: wumpus sipa gmaxwell jonasschnelli morcos luke-jr btcdrak sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator
03:01 moneyball: suggested topic: proposed meeting topics ahead of time

<!-- more --> 

03:01 meshcollider: hi
03:01 BlueMatt: topics: 0.17.1
03:01 wumpus: #topic high priority for review
03:02 wumpus: current PRs: #14670 #13932 #14336 #14646
03:02 gribble: https://github.com/bitcoin/bitcoin/issues/14670 | http: Fix HTTP server shutdown by promag · Pull Request #14670 · bitcoin/bitcoin · GitHub
03:02 gribble: https://github.com/bitcoin/bitcoin/issues/13932 | Additional utility RPCs for PSBT by achow101 · Pull Request #13932 · bitcoin/bitcoin · GitHub
03:02 gribble: https://github.com/bitcoin/bitcoin/issues/14646 | Add expansion cache functions to descriptors (unused for now) by sipa · Pull Request #14646 · bitcoin/bitcoin · GitHub
03:02 gribble: https://github.com/bitcoin/bitcoin/issues/14336 | net: implement poll by pstratem · Pull Request #14336 · bitcoin/bitcoin · GitHub
03:02 kanzure: hi.
03:03 wumpus: anyone want to add or remove anything?
03:04 sipa: lgtm
03:04 meshcollider: Pieter already has one but it'd be great to have #14565
03:04 gmaxwell: whats the overlap with 0.17.1 tag?
03:04 gribble: https://github.com/bitcoin/bitcoin/issues/14565 | Overhaul importmulti logic by sipa · Pull Request #14565 · bitcoin/bitcoin · GitHub
03:04 chenpo: hi
03:05 wumpus: does the 0.17.1 tag have any non-backports left?
03:05 gmaxwell: #14380  
03:05 gribble: https://github.com/bitcoin/bitcoin/issues/14380 | fix assert crash when specified change output spend size is unknown by instagibbs · Pull Request #14380 · bitcoin/bitcoin · GitHub
03:05 gmaxwell: is what I was thinking of.
03:05 wumpus: https://github.com/bitcoin/bitcoin/milestone/39
03:06 wumpus: let's add that one then
03:06 meshcollider: 14782 is sort-of not a backport
03:06 jnewbery: hi
03:06 wumpus: meshcollider: which one is the most-blocking?
03:07 wumpus: #14646 seems like it needs to go in before something else so looks like a typical candidate at least
03:07 gribble: https://github.com/bitcoin/bitcoin/issues/14646 | Add expansion cache functions to descriptors (unused for now) by sipa · Pull Request #14646 · bitcoin/bitcoin · GitHub
03:07 meshcollider: Yeah don't remove that one
03:08 gmaxwell: The broken getbalance behavior should get fixed. It's an actual bug.
03:08 wumpus: that's only broken on 0.17 and not master?
03:08 provoostenator: #14602
03:08 gribble: https://github.com/bitcoin/bitcoin/issues/14602 | Bugfix: Correctly calculate balances when min_conf is used, and for getbalance("*") by luke-jr · Pull Request #14602 · bitcoin/bitcoin · GitHub
03:09 achow101: hi
03:09 wumpus: wait, I added #14782 which is the 0.17 backport
03:09 gribble: https://github.com/bitcoin/bitcoin/issues/14782 | [0.17] Bugfix: Correctly calculate balances when min_conf is used, and for getbalance("*") by luke-jr · Pull Request #14782 · bitcoin/bitcoin · GitHub
03:09 jnewbery: I'm not clear what the behaviour is 'supposed' to be. There's no documentation or test coverage
03:09 gmaxwell: wumpus: not yet, there is another PR
03:09 wumpus: why is a backport open before something is merged into master? is it signifiantly different?
03:09 provoostenator: Ah yes, it's already marked for backport.
03:09 meshcollider: The 0.17 backport of it is different yes
03:09 meshcollider: Because of the accounts removal
03:09 sipa: maybe the getbalance behaviour needs to be topic on its own>?
03:09 wumpus: right
03:10 gmaxwell: jnewbery: thats a fine concern, but it's not cool to break functionality just because there wasn't enough tests to stop you from doing so
03:10 meshcollider: ping luke-jr
03:10 wumpus: if there's any doubt it probably needs to stay as it was
03:10 gmaxwell: The alternative of going and reverting the breaking change is unfortunately too disruptive (I already tried).
03:10 meshcollider: Re-implementing the old behaviour without reintroducing account parameters is the issue
03:10 jnewbery: the new behaviour in the fix is different from pre-0.17
03:11 meshcollider: And it has some weird parameter type polymorphism
03:11 wumpus: well for 0.18, changing the behavior can be discussed if there's agood reason
03:11 sipa: gmaxwell: well given the removal of accounts, i think it's fair to say that anyone passing not-nothing as the account parameter to getbalance needs to change, and you can get the 0-conf behavior using getunconfirmedbalance
03:11 jnewbery: so before we decide whether it should be merged, we should figure out what the behavious should be, document it and cover it with tests so it's not regressed
03:11 provoostenator: getunconfirmedbalance _only_ includes unconfirmed balance afaik
03:11 sipa: oh
03:12 wumpus: for 0.17 it'd be good to go back to the old behavior because it was not announced in the release notes that it would change
03:12 sipa: ignore my suggestion, again
03:12 meshcollider: Add them together then :)
03:12 gmaxwell: if you add them you'll double count
03:12 meshcollider: wumpus: that's why the 0.17 backport was opened already
03:12 provoostenator: It's useful in practice to be able to get the balance including unconfirmed, so you can compose a PSBT while you're waiting for confirmation.
03:12 BlueMatt: also for 0.17.1 this seems a bit too late to be figuring out
03:12 BlueMatt: we can revisit for 0.17.2 if there is one
03:12 provoostenator: (without doing math)
03:13 BlueMatt: but 0.17.0 currently cannot be self-built and bitcoin-qt opened on latest fedora/ubuntu release
03:13 BlueMatt: both of which have been out for a bit now
03:13 gmaxwell: It isn't just a question of unconfirmed or not, it's a question of your balance suddenly showing zero when you make a small payment.. because now your change is unconfirmed.
03:13 sipa: gmaxwell: getbalance includes change
03:13 sipa: just not unconfirmed incoming payments
03:14 sipa: that was the distinction between getbalance and getbalance *, afaik
03:14 wumpus: #topic getbalance
03:14 gmaxwell: Right
03:14 gmaxwell: sipa: and thats also why you can't add getunconfirmedbalance.
03:14 jnewbery: for those without context, this is (mostly) my fault for removing accounts. The first parameter to getbalance was 'account', it was marked DEPRECATED with a warning saying 'don't use this'. I removed it and it turns out people were using it to sum up untrusted coins
03:14 sipa: you can simulate "getbalance *" using "getbalance minconf=1" + "getunconfirmedbalance" i guess
03:14 wumpus: BlueMatt: yes, let's discuss what to in include in 0.17.1 in the 0.17.1 topic
03:15 meshcollider: But the actual difference wasn't just unspent, it was untrusted, right?
03:15 sipa: meshcollider: indeed
03:15 meshcollider: Unconfirmed*
03:15 jnewbery: getbalance -minconf=0 includes unconfirmed but not untrusted coins (eg your change)
03:15 jnewbery: getbalance * 0 would (prior to 0.17) include untrusted
03:16 jnewbery: so for example if someone sent you an output, then RBF'ed it, you'd still see that in your getbalance * 0
03:16 meshcollider: as you pointed out on the PR though john, does that also include conflicting transactions and stuff too?
03:16 jnewbery: or RBF'ed it to you, you'd double count it
03:16 jnewbery: or you could have a negative balance
03:16 meshcollider: Thats not sane behaviour to keep then :/
03:17 wumpus: that sounds pretty broken
03:17 gmaxwell: I didn't think it included conflicteds, but actually it makes sense.
03:17 jnewbery: I don't know why people were using getbalance * 0, or what they were using it for. I've asked a few times on the PR but no-one can answer
03:17 gmaxwell: If you recall when we removed accounts I raised a concern that didn't we still need move to fixed people's negative balances... because we still had those reported from time to time.
03:17 jnewbery: ok, I've fixed that :)
03:18 gmaxwell: jnewbery: to see unconfirmed payments... it's certantly what I always did before I gave up on balances and just switched to looking at the unspent outputs directly
03:18 ryanofsky: It sounded to me like people were just using it to get unconfirmed balance without having two make two calls
03:18 provoostenator: That's exactly how I use it.
03:18 sipa: how about adding a "requiretrusted" parameter to getbalance...?
03:18 gmaxwell: ryanofsky: not just without having to make two calls, because getbalance included 0 conf trusted coins.
03:18 provoostenator: If you want to prepare a transaction to spend all, you need to enter the amount to send.
03:18 gmaxwell: ryanofsky: and the minconf parameter was added later
03:19 jnewbery: I think it's fine to have a balance including unconfirmeds if they're trusted (ie all inputs were yours). Having a balance containing unconfirmeds that aren't trusted and so can be double-accounted or worse doesn't make sense to me
03:19 meshcollider: sipa: the PR introduces a bool for trustedness
03:19 sipa: meshcollider: oh!
03:19 jnewbery: I strongly discourage any 'balance' that contains untrusted coins
03:19 sipa: does it allow counting untrusted, while excluding conflicting etc?
03:19 meshcollider: No
03:19 gmaxwell: jnewbery: I don't understand "trusted and so can be double-accounted" -- even a trusted payment could be conflicted
03:20 provoostenator: jnewbery: why? Isn't that implied when the user enters 0 instead of 1 confirmations?
03:20 meshcollider: unconfirmed != untrusted though
03:20 gmaxwell: jnewbery: we _show_ unconfirmed payments in the wallet, so it's somewhat odd and confusing that we don't have "pending balance"
03:21 wumpus: the GUI does have a 'unconfirmed balance' IIRC?
03:21 sipa: showing untrusted balance sounds perfectly reasonable, but it shouldn't include conflicting/... things
03:21 meshcollider: We could break the getbalance output and return an array of "confirmed":, "unconfirmed":, "conflicting:
03:21 jnewbery: for me 'pending balance' doesn't make sense if it can double-count conflicting transactions. It's worse that not having a pending balance at all
03:22 meshcollider: ^
03:22 sipa: jnewbery: i agree
03:22 morcos: yes, its not clear to me what the problem is with using getbalance and getunconfirmedbalance when using -cli and the GUI already does the right thing?
03:22 gmaxwell: In any case, you wanted the use case, the reason people use getbalance "*" is to (Attempt) to learn their pending balance.  What they'll have assuming nothing goes wrong.  Now if that was also double counting conflicteds and ending up negative, I think thats a bug. (and probably the origin of the negative balances I was concerned about before)
03:22 wumpus: users don't know what 'untrusted balance' is supposed to be, I think exposing these kind of implementation details on the interface is a bit confusing
03:22 provoostenator: I agree double counting is undesirable.
03:22 jnewbery: it will make users think their money has disappeared because once one of those conflicting transactions is confirmed their balance goes down
03:22 morcos: can someone clearly point out exactly what we can not do now (other than we didn't properly explain what was changing)
03:22 meshcollider: luke-jr: should be here to argue the other side
03:22 sipa: jnewbery: i think no getbalance* call should evr include conflicted things
03:22 provoostenator: It should probably use mempool rules to figure out which transaction to ignore.
03:23 sipa: provoostenator: some things do
03:23 meshcollider: IMO setting min_conf to 0 is enough?
03:23 gmaxwell: sipa: wait. I would think that it would include one side of a conflict...
03:23 sipa: gmaxwell: oh sure; terminology
03:23 wumpus: isn't it supposed to make one side of a conflict non-conflicting?
03:23 sipa: i guess by non-conflicting i mean "in the mempool" ?
03:23 wumpus: right
03:24 gmaxwell: Good! jnewbery's comment about balances going down confused me
03:24 sipa: gmaxwell: or do you think unconfirmed untrusted not-in-the-mempool unconflicted things should be counted?
03:24 jnewbery: sorry, I've got to step away now. My main point is that the expected behaviour should be well documented and covered by tests
03:24 gmaxwell: sipa: no. I don't.
03:24 sipa: ok, good
03:24 jnewbery: I've written a test script for wallet balances, but we need to agree what the behaviour *should* be before merging any of this stuff
03:25 meshcollider: Agreed
03:25 provoostenator: If something gets confirmed against what you would expect fromt he mempool then a balance change is fine imo, but not otherwise.
03:25 sipa: so how about getbalance requires the minconf as directed, and (if trusted is directed, trusted, otherwise in-the-mempool)
03:26 provoostenator: sipa: the only criteria for "trusted" is whether it's change, right?
03:26 gmaxwell: I think if sipa is right that the behavior can be emulated by getbalance minconf=1 + getunconfirmed then at least we have a workaround.  Though it's always confusing to have a deault behavior which cannot be explained by some setting of the arguments
03:26 sipa: provoostenator: or confirmed
03:27 gmaxwell: "What is the default minconf setting of getbalance? Mu.  getbalance output shows minconf=0 for trusted outputs, and minconf=1 for others.  so trusted defaults to true? No, there is no trusted argument."
03:28 sipa: gmaxwell: #14602 includes a trusted_only argument that is true by default
03:28 gribble: https://github.com/bitcoin/bitcoin/issues/14602 | Bugfix: Correctly calculate balances when min_conf is used, and for getbalance("*") by luke-jr · Pull Request #14602 · bitcoin/bitcoin · GitHub
03:28 provoostenator: I know the wallet makes a distinction between change and non-change when it comes to spending, which is fine, but I don't think we should do that for balance. So by default minconf=0 should show change and non-change, but not replaced-by.
03:28 ryanofsky: just want to note, it looks like we didn't delete the GetLegacyBalance function, so it would be trivial to restore the old getbalance "*" behavior, if we can't figure out something better right now
03:28 gmaxwell: I know 14602 does. I'm trying to imagine a world where we keep things as they are and try to release note ourselves out of it
03:29 provoostenator: (as for 0.17 I'm fine with release-noting our way of it)
03:29 sipa: oh, i was just trying to establish what the desired behavior is before we go discuss what to do about it
03:30 provoostenator: sipa: that's a good idea
03:30 sipa: and i think there is at least a rough conclusion? allow counting untrusted, but never count not-in-mempool?
03:31 gmaxwell: Right, I think the desired behavior is that balances shows confirmed + trusted-in-mempool-0conf.  And that you be able to adjust the threshold for confirmed and turn the trusted-in-mempool-zeroconf on and off. And if you make the confirmed=0, it should still only count in-mempool
03:31 provoostenator: (and maybe add a 4th argument along the lines of unconfirmed_change_only
03:31 gmaxwell: (and potentially the arguments should just be  minconf_for_not_you=1 minconf_for_from_you=0 )
03:32 sipa: i think the default of minconf=0 but trusted_only=true makes sense; if you choose trusted_only=false it should still only include confirmed or mempool things
03:32 morcos: sipa: the problem with never counting not-in-mempool is if you spend a 10 BTC input to pay 0.001 BTC, and that tx doesn't go in your mempool then your balance goes down by 10 mysteriously, but thats hard to solve
03:32 sipa: morcos: yeah...
03:32 gmaxwell: morcos: yes, I think thats hard to solve, also it's kinda good that it goes down in that you're actually screwed for the moment :P
03:33 gmaxwell: like if that txn doesn't confirm, your funds are actually stuck.
03:33 gmaxwell: (until you abandon the transaction)
03:33 wumpus: right
03:34 gmaxwell: I guess I can argue the consequences either way, I can imagine someone losing a wallet file with lots of bitcoin in it because it showed a low balance due to some easily abandoned transactions.
03:34 sipa: so i think we can work out how to implement this for 0.17 and 0.18 on the PRs or issues; no need for further design here?
03:34 gmaxwell: I thought luke's PR basically implemented what we came up with here. But I'm not sure.
03:35 sipa: gmaxwell: i'm not sure about the mempool part
03:35 wumpus: gmaxwell: people are likely to use 'getbalance' without parameters in that case, to check wallet balance, not the specific combo that this is about
03:35 gmaxwell: certantly if we're showing all unconfirmeds, including both sides of a conflict, thats bad. :P
03:36 provoostenator: Luke's PR adds a trusted_only as a first parameter. I find that a fairly confusing term, so hopefully we can avoid it with the ^
03:36 sipa: with the what?
03:37 wumpus: trusted_only sounds really confusing to users, if you make a parameter like that you need to carefully explain in the RPC help what 'truste'd means in this setting
03:37 sipa: agree, it needs documentation for sure
03:37 wumpus: it's far from obvious, I don't know if we picked a good term for it
03:37 provoostenator: With what you said: "allow counting untrusted, but never count not-in-mempool"
03:38 provoostenator: It's already a default, so maybe just a matter of renaming and documenting it.
03:38 sipa: provoostenator: it can certainly be explained more friendly as "Whether unconfirmed payments from others are excluded"
03:38 provoostenator: 1. zero_conf_change_only (default: false)
03:39 wumpus: sipa: that sounds much better
03:39 sipa: i think we're getting in the weeds here
03:39 wumpus: yes, time for next otpic?
03:39 sipa: agree
03:39 provoostenator: Next topic sounds good.
03:39 wumpus: #topic 0.17.1
03:39 BlueMatt: release time!
03:39 wumpus: 20 minutes left
03:40 BlueMatt: cool, release in 20 minutes? :p
03:40 provoostenator: BlueMatt is the main reason Ubutnu?
03:40 meshcollider: Lol
03:40 BlueMatt: provoostenator: also fedora, debian testing, .......
03:40 provoostenator: Because an alternative could be 0.17.0.2 like we did with MacOS. Though I'm fine with proper 0.17.1 too
03:40 wumpus: still lots of backports open https://github.com/bitcoin/bitcoin/milestone/39 I guess they need review, or at least merging
03:40 BlueMatt: provoostenator: also there are a number of other bugs and backports that are done, etc
03:40 sipa: we have a bunch of bugfixes lined up too
03:40 wumpus: nah let's do a proper release
03:40 sipa: it may be time for a 0.17.1
03:40 BlueMatt: things already merged on master probably worth backporting
03:40 wumpus: it's too late for 0.17.0.2 IMO
03:40 BlueMatt: cause there are a bunch there
03:41 provoostenator: Right, that would involve branching off of the 0.17.0.1 tag and get weird.
03:41 wumpus: .z releases are really 'oops we did a release and need to fix this thing up'
03:41 BlueMatt: but, at least IMO, its super annoying that you cant build+run bitcoin-qt on the now-several-months-old versions of various OSs, and I presume other rolling distros (eg arch) also have this issue
03:41 wumpus: not for month later
03:41 instagibbs: I keep crashing, get 14380 in please ;P
03:41 BlueMatt: so I would prefer we not wait around for fixing getbalance :p
03:41 wumpus: I agree with BlueMatt on this
03:42 BlueMatt: #14380 looks more than merge-able from where I'm sitting in the ack department
03:42 gribble: https://github.com/bitcoin/bitcoin/issues/14380 | fix assert crash when specified change output spend size is unknown by instagibbs · Pull Request #14380 · bitcoin/bitcoin · GitHub
03:42 BlueMatt: and not too hard to backport
03:42 sipa: can people have a look at #14780 too?
03:42 gribble: https://github.com/bitcoin/bitcoin/issues/14780 | PSBT backports to 0.17 by sipa · Pull Request #14780 · bitcoin/bitcoin · GitHub
03:42 sipa: (i'm mostly unfamiliar with the backports process)
03:43 wumpus: there is no agreement on getbalance yet, it can wait for 0.17.2
03:43 wumpus: sipa: sure!
03:43 sipa: thanks
03:43 wumpus: sipa: please make sure you include the commit metadata (Github-Pull: #.... and Rebased-From: <commit>)
03:44 BlueMatt: next topic: the wall of text I just posted to bitcoin-dev :p
03:44 wumpus: (see the commits in other backport PRs such as https://github.com/bitcoin/bitcoin/pull/14835)
03:44 sipa: BlueMatt: not there
03:44 wumpus: next topic is moneyball's
03:44 moneyball: hi
03:44 BlueMatt: err, topic suggestion
03:44 BlueMatt: anything else on 0.17.1?
03:45 BlueMatt: or just generally a "lets take things that we can merge today, do backports, and get this thing going"
03:45 provoostenator: BlueMatt: "IRC logs have been disabled due to the EU General Data Protection Regulation (GDPR)."
03:45 wumpus: BlueMatt: +1
03:45 provoostenator: +1
03:45 wumpus: #topic proposed meeting topics ahead of time (moneyball)
03:46 moneyball: I’d like to suggest that people can propose Core weekly meeting topics anytime throughout the week in this IRC channel using #proposedmeetingtopic tag. I will collect these throughout the week, add them to a gist that anyone can have a look at during the week. The primary intended benefit of this is to allow people to know which topics are going to be discussed ahead of time allowing them to prepare.
03:46 moneyball: Any concerns?
03:46 BlueMatt: seems reasonable
03:46 provoostenator: +1
03:46 BlueMatt: easier than remembering to mention them in meeting
03:46 Chris_Stewart_5: +1
03:46 meshcollider: +1
03:46 BlueMatt: next topic? #thatwaseasy
03:47 wumpus: yes, good idea, let's see how it goes
03:47 moneyball: Ok I will start doing it!
03:47 wumpus: BlueMatt: ok what was your proposal, I'm not in #bitcoin-dev
03:47 provoostenator: And there's no logs..
03:47 BlueMatt: oh, i meant bitcoin-dev ml but it hasnt passed moderation yet
03:47 BlueMatt: anyway, I can tl;dr it in two lines
03:47 BlueMatt: in lightning (and other related payment channel-y systems) you have the general issue of pre-signing transactions
03:48 BlueMatt: so you have to predict what the feerate on the network will be in the future at the time your counterparty misbehaves
03:48 wumpus: #topic pre-signing transactions (BlueMatt)
03:48 BlueMatt: this is....obviously insane
03:48 BlueMatt: instead, we'd (obviously) like to use cpfp
03:48 BlueMatt: but there are the cpfp rbf-pinning-ish issues where your counterparty can fill up the package with big-bug-low-ish-feerate txn
03:48 BlueMatt: so that you cant cpfp it yourself
03:49 BlueMatt: I'd like to propose we tweak the cpfp/rbf rules
03:49 BlueMatt: The last transaction which is added to a package of dependent transactions in the mempool must:
03:49 BlueMatt: * Have no more than one unconfirmed parent,
03:49 BlueMatt: * Be of size no greater than 1K in virtual size.
03:49 BlueMatt: (we'd, in practice, first decrease the package size limits by 1 1K-virtual-size transaction, then make it so that the last one must meet those rules)
03:49 BlueMatt: this allows for cpfp by letting each side of a lightning channel independantly cpfp without considering what the other side may be doing
03:49 provoostenator: Current RBF rules for reference: https://github.com/bitcoin/bips/blob/master/bip-0125.mediawiki#Implementation_Details
03:50 BlueMatt: that may be too much to think about before reading the full ml post, but mostly it just covers background material
03:50 BlueMatt: /fin
03:50 BlueMatt: (oh, also this fix requires package relay, which is another can of worms itself)
03:50 sipa: here is another earlier proposed modification: https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-February/015717.html
03:50 sipa: BlueMatt: oh dear
03:51 BlueMatt: well, luckily only one-deep package relay and only for small-ish packages
03:51 BlueMatt: or at least small dependents
03:51 instagibbs: sorry how does cpfp get pinned again?
03:51 instagibbs: RBF pinning I know
03:52 BlueMatt: instagibbs: A -> B where B is 100KB but low feerate, but high fee. its the same issue for lightning
03:52 BlueMatt: cause you cant add to the package cause the package is max size
03:52 instagibbs: ah
03:52 sipa: my response to this is "eh... sure.... but how?"
03:52 instagibbs: so it's not something you can attach B'
03:52 BlueMatt: so you have to add to the package by rbf which means you have to increase total size, if you can even do that, which you'd have to tweak rbf rules to let you replace B with C, but you cant do that today
03:52 BlueMatt: sipa: hmm?
03:52 sipa: you need package relay...
03:53 sipa: that's not just a small few-lines policy change
03:53 provoostenator: An alternative, I forgot what the problem was, is to drop RBF rule "3. The replacement transaction pays an absolute fee of at least the sum paid by the original transactions." and only consider fee rate of the replacement, regardless of size.
03:53 sdaftuar: so i think package relay is a whole other topic
03:53 BlueMatt: I have another bitcoin-dev post coming discussing package relay, but we have a few options there, if we just want to solve package relay for contracting applications like lightning, we can do so with limited consideration, I think
03:53 BlueMatt: if we want a more general solution I still think its possible but requires more in-depth ATMP refactoring
03:54 sipa: and P2P changes...
03:54 BlueMatt: assuming we do at least one of those two, this is a simple (I think) policy change that I'm hoping people here dont object to
03:54 BlueMatt: possibly, though actaully not neccessarily
03:54 BlueMatt: but, probably
03:54 sipa: this sounds very preliminary to me
03:54 BlueMatt: i presume you mean the package relay part?
03:54 BlueMatt: the policy rule here is pretty straightforward, I think?
03:55 BlueMatt: and not very preliminary, again assuming some form of package relay
03:55 sipa: i don't understand how you can say it's not preliminary, while relying on something we have no idea about yet
03:55 meshcollider: Shall we discuss next week instead after reading the ml
03:55 gmaxwell: MAGIC
03:55 BlueMatt: heh, sdaftuar and I have been batting package relay back and forth for months, but, whatever
03:56 BlueMatt: agreed we need a harder proposal for package relay
03:56 sdaftuar: well i think it'd be useful to layout the design goals for a package relay ssytem
03:56 BlueMatt: anyway, yes, we'll discuss package relay on the ml and then come back to this
03:56 sipa: BlueMatt: yes i'd like to see a proposal for that :)
03:56 gmaxwell: BlueMatt: the point is that the policy change justification is a black box to us for the moment. :P
03:56 BlueMatt: also what sdaftuar said
03:56 BlueMatt: this is also a motivator for package relay
03:56 BlueMatt: as its yet another thing to feed into the design goals
03:56 BlueMatt: gmaxwell: I mean if you presume package relay it isnt at all a black box?
03:56 BlueMatt: huh
03:57 BlueMatt: anyway, -> ml
03:57 provoostenator: Topic suggestion: dandelion stempool relay :-P
03:57 sdaftuar hides
03:57 BlueMatt: 4 minutes, GO
03:57 BlueMatt: err, 3
03:57 instagibbs: sdaftuar, you ahve 3 minutes to resolve it
03:58 wumpus: #topic wallet maintainer
03:58 wumpus: meshcollider has shown interest in becoming wallet maintainer!
03:59 provoostenator: Awesome
03:59 sipa offers condolences
03:59 sipa: :)
03:59 provoostenator: Anyoe against, no, done. End meeting :-)
03:59 wumpus: which is great news, I think he'd be good at his, many of his his contributions have been to the wallet
03:59 meshcollider: :)
03:59 wumpus: and he's been active contributor for quite a while
04:00 sipa: more seriously, sounds great to me
04:00 achow101: +1
04:00 wumpus: yes!
04:00 bitcoin-git: [bitcoin] vim88 opened pull request #14846: Docs: Adds development guidelines about Scripts shebang to developer-notes.md. (master...add_scripts_development_guidelines) https://github.com/bitcoin/bitcoin/pull/14846
04:00 wumpus: ok, that was a quick topic, was intending to bring it up sooner but BlueMatt kind of ninja'd it :)
04:00 wumpus: #endmeeting

(中文 google 亂翻)
03:00 wumpus：#startmeeting 
03:00 lightningbot：會議開始於11月29日星期四19:00:25 2018 UTC。椅子是wumpus。有關MeetBot的信息，請訪問http://wiki.debian.org/MeetBot。
03:00 lightningbot：有用的命令：#action #agreed #help #info #idea #link #topic。
03:00 sipa：哦，見面！
03:00 dongcarl：hi 
03:00 moneyball：嗨
03:01 wumpus：#bitcoin-core-dev會議：wumpus sipa gmaxwell jonasschnelli morcos luke-jr btcdrak sdaftuar jtimon cfields petertodd kanzure bluematt instagibbs phantomcircuit codeshark michagogo marcofalke paveljanik NicolasDorier jl2012 achow101 meshcollider jnewbery maaku fanquake promag provoostenator 
03:01 moneyball：建議主題：提議會議主題提前
03:01 meshcollider：hi 
03:01 BlueMatt：主題：0.17.1 
03:01 wumpus：#topic高優先級審查
03:02 wumpus：當前PR：＃14670＃13932＃14336＃14646 
03:02 gribble：https： //github.com/bitcoin/bitcoin/issues/14670 | http：通過promag修復HTTP服務器關閉·Pull Request＃14670·比特幣/比特幣·GitHub 
03:02抱怨：https：//github.com/bitcoin/bitcoin/issues/13932 | 其他實用工具RPC for PSBT by achow101·Pull Request＃13932·bitcoin / bitcoin·GitHub 
03:02 gribble：https：//github.com/bitcoin/bitcoin/issues/14646 | 通過sipa將擴展緩存函數添加到描述符（暫時未使用）·Pull Request＃14646·bitcoin / bitcoin·GitHub 
03:02 gribble：https://github.com/bitcoin/bitcoin/issues/14336 | net：通過pstratem實現民意調查·拉請求＃14336·比特幣/比特幣·GitHub 
03:02 kanzure：嗨。
03:03 wumpus：有人想添加或刪除任何內容嗎？
03:04 sipa：lgtm 
03:04 meshcollider：Pieter已經有一個但是很高興有＃14565 
03:04 gmaxwell：重疊與0.17.1標籤有什麼關係？
03:04抱怨：https：//github.com/bitcoin/bitcoin/issues/14565 | 通過sipa大修importmulti logic·Pull Request＃14565·bitcoin / bitcoin·GitHub 
03:04 chenpo：hi 
03:05 wumpus：0.17.1標籤是否有任何非後退？
03:05 gmaxwell：＃14380 
03:05 gribble：https：//github.com/bitcoin/bitcoin/issues/14380| 當instagibbs指定更改輸出支出大小未知時修復斷言崩潰·拉請求＃14380·比特幣/比特幣·GitHub 
03:05 gmaxwell：是我在想的。
03:05 wumpus：https：//github.com/bitcoin/bitcoin/milestone/39
03:06 wumpus：讓我們添加一個然後
03:06 meshcollider：14782是排序 - 不是一個backport 
03:06 jnewbery：hi 
03 ：06 wumpus：meshcollider：哪一個阻擋最多？
03:07 wumpus：＃14646似乎需要在其他東西之前進入所以看起來像一個典型的候選人至少
03:07抱怨：https：//github.com/bitcoin/bitcoin/issues/14646| 通過sipa將擴展緩存函數添加到描述符（現在不用）·Pull Request＃14646·bitcoin / bitcoin·GitHub 
03:07 meshcollider：是的，不要刪除那個
03:08 gmaxwell：破壞的getbalance行為應該得到修復。這是一個真正的錯誤。
03:08 wumpus：這只是在0.17而不是主人？
03:08 provoostenator：＃14602 
03:08 gribble：https：//github.com/bitcoin/bitcoin/issues/14602 | 修正：正確計算使用min_conf時的餘額，以及通過luke-jr獲取getbalance（“ ”）的數據。拉請求＃14602·比特幣/比特幣·GitHub 
03:09 achow101：嗨
03:09 wumpus：等等，我添加了＃14782是0.17 backport 
03:09 gribble：https：//github.com/bitcoin/bitcoin/issues/14782| [0.17]錯誤修正：使用min_conf時正確計算餘額，並且通過luke-jr 正確計算getbalance（“ ”）·Pull Request＃14782·bitcoin / bitcoin·GitHub 
03:09 jnewbery：我不清楚這是什麼行為'應該是。沒有文件或測試報導
03:09 gmaxwell：wumpus：還沒有，還有另一個公關
03:09 wumpus：為什麼在某些東西被合併到主人之前是一個後端打開？它有顯著的不同嗎？
03:09 provoostenator：啊，是的，已經標記為後退。
03:09 meshcollider：它的0.17 backport是不同的是
03:09 meshcollider：因為帳戶刪除
03:09 sipa：也許getbalance行為需要自己的主題>？
03:09 wumpus：對
03:10 gmaxwell：jnewbery：這是一個很好的關注，但是因為沒有足夠的測試來阻止你這麼做而打破功能並不酷
.03：10 meshcollider：ping luke-jr 
03:10 wumpus：if there is any懷疑它可能需要留下來，因為它是
03:10 gmaxwell：不幸的是，過去和恢復突破性變化的替代方案太具有破壞性（我已經嘗試過）。
03:10 meshcollider：重新實現舊行為而不重新引入帳戶參數是問題
03:10 jnewbery：修復中的新行為不同於0.17之前的
03:11 meshcollider：它有一些奇怪的參數類型多態
03： 11 wumpus：好的0.18，如果有充分的理由可以討論改變行為
03:11 sipa：gmaxwell：考慮到賬戶的刪除，我認為可以說任何通過非平衡作為賬戶參數的人都需要改變，你可以使用getunconfirmedbalance 
03:11 獲得0-conf行為jnewbery：所以在我們決定是否應該合併之前，我們應該弄清楚它應該是什麼樣的，記錄它並用測試覆蓋它所以它沒有退化
03:11 provoostenator：getunconfirmedbalance 只包括未經證實的平衡afaik 
03:11 sipa：哦
03:12 wumpus：對於0.17，回到原來的行為是好的，因為在發行說明中沒有宣布它會改變
03:12 sipa：忽略我的建議，再次
03:12 meshcollider：將它們加在一起然後 ：）
03:12 gmaxwell：如果你添加它們你將重複計算
03:12 meshcollider：wumpus：這就是為什麼0.17 
反擊已經打開03:12 provoostenator：在實踐中能夠獲得包括未經證實的平衡是有用的，所以你你在等待確認時可以組成PSBT。
03:12 BlueMatt：也是0.17.1這似乎有點太晚了，無法弄清楚
03:12 BlueMatt：如果有一個
03:12的挑釁者，我們可以重訪0.17.2 :(不做數學）
03:13 BlueMatt ：但是0.17.0目前無法自行構建並且在最新的fedora / ubuntu發佈時打開比特幣qt 
03:13 BlueMatt：兩者現在已經有點了
03:13 gmaxwell：這不僅僅是一個未經證實的問題，這是一個問題，當你進行小額支付時，你的餘額突然顯示為零......因為現在你的改變未經證實。
03:13 sipa：gmaxwell：getbalance包括更改
03:13 sipa：只是沒有未經證實的收款
03:14 sipa：這是getbalance和getbalance之間的區別，afaik 
03:14 wumpus：#topic getbalance 
03:14 gmaxwell：Right 
03 ：14 gmaxwell：sipa：這就是為什麼你不能添加getunconfirmedbalance。
03:14 jnewbery：對於那些沒有上下文的人來說，這（主要）是我刪除帳戶的錯。getbalance的第一個參數是'account'，它標記為DEPRECATED，並帶有警告“不要使用此”。我刪除它，事實證明人們用它來總結不信任的硬幣
03:14 sipa：你可以使用“getbalance minconf = 1”+“getunconfirmedbalance”



模擬“getbalance”我猜 03:14 wumpus：BlueMatt：是的，讓我們討論在0.17.1主題 03:15 meshcollider 中包含0.17.1中的內容：但實際的差異不僅僅是未花費，而且是不可信的，對吧？ 03:15 sipa：meshcollider：確實 03:15 meshcollider：未經證實
03:15 jnewbery：getbalance -minconf = 0包括未經證實但不可信的硬幣（例如你的變化）
03:15 jnewbery：getbalance * 0會（在0.17之前）包含不受信任的
03:16 jnewbery：所以例如如果有人發給你一個輸出，然後RBF'，你仍然會看到你的getbalance * 0 
03： 16 meshcollider：正如你在約翰指出的PR那樣，那還包括衝突的交易和東西嗎？
03:16 jnewbery：或RBF'ed給你，你要重複它
03:16 jnewbery：或者你可以有一個負餘額
03:16 meshcollider：那是不理智的行為，以保持當時：/ 
03:17 wumpus：聽起來很
糟糕03:17 gmaxwell：我認為它不包括衝突，但實際上它是有道理的。
03:17 jnewbery：我不知道為什麼人們使用getbalance * 0，或者他們使用它的原因。我曾多次詢問PR，但沒有人可以回答
03:17 gmaxwell：如果你記得當我們刪除帳戶時我提出了一個問題，我們仍然不需要轉移到固定人的負餘額......因為我們還有不時報導的那些。
03:17 jnewbery：好的，我已經解決了這個問題:) 
03:18 gmaxwell：jnewbery：看到未經證實的付款......這是我在放棄餘額之前總是做的事情，只是直接切換到未使用的輸出
03： 18 ryanofsky：聽起來像是人們只是用它來獲得未經證實的平衡而沒有兩次打兩次電話
03:18 provoostenator：這正是我如何使用它。
03:18 sipa：如何為getbalance添加“requiretrusted”參數......？
03:18 gmaxwell：ryanofsky：不僅不需要打兩個電話，因為getbalance包括0 conf可信硬幣。
03:18 provoostenator：如果你想準備一筆全部交易，你需​​要輸入要發送的金額。
03:18 gmaxwell：ryanofsky：minconf參數後來被添加
03:19 jnewbery：我認為如果他們被信任（即所有輸入都是你的），那麼平衡包括未經證實的人是沒關係的。包含不受信任的未經證實的餘額，因此可能是雙重記錄或更糟糕對我來說沒有意義
03:19 meshcollider：sipa：PR為可信度引入了bool 
03:19 sipa：meshcollider：哦！
03:19 jnewbery：我強烈反對任何包含不受信任的硬幣的“餘額” 
03:19 sipa：它是否允許計算不受信任，同時排除衝突等？
03:19 meshcollider：No 
03:19 gmaxwell：jnewbery：我不明白“信任，所以可以雙重考慮” - 即使是可信賴的付款也可能會發生衝突
03:20 provoostenator：jnewbery：為什麼？當用戶輸入0而不是1次確認時，這是不是暗示了？
03:20 meshcollider：未經證實！=不信任雖然
03:20 gmaxwell：jnewbery：我們在錢包中顯示未經證實的付款，所以我們沒有“待定餘額” 
03:21 wumpus 有點奇怪和混亂：GUI確實有一個'未經證實的平衡'IIRC？
03:21 sipa：顯示不受信任的平衡聽起來完全合理，但它不應該包含衝突/ ......事物
03:21 meshcollider：我們可以打破getbalance輸出並返回“已確認”數組：“未經證實”：“衝突” ：
03：21 jnewbery：對於我來說，“未結餘額”是沒有意義的，如果它可以重複計算相互衝突的交易。更糟糕的是沒有待定餘額
03:22 meshcollider：^ 
03:22 sipa：jnewbery：i同意
03:22 morcos：是的，我不清楚在使用-cli時使用getbalance和getunconfirmedbalance是什麼問題，而GUI已經做對了嗎？
03：22 gmaxwell：無論如何，你想要用例，人們使用getbalance的原因““是（嘗試）學習他們未決的餘額。他們假設什麼都不會出錯。現在如果這也是重複計算衝突並最終結果為負，我認為這是一個錯誤。（可能是負餘額的來源）我以前擔心過）
03:22 wumpus：用戶不知道應該是什麼'不信任的平衡'，我認為在界面上暴露這些實現細節有點令人困惑
03:22 provoostenator：我同意重複計算是不可取的。
03:22 jnewbery：它會使用戶認為他們的錢已經消失了，因為一旦這些衝突的事務的一個證實其資產負債下山
03:22 morcos：可有人明確指出到底是什麼，我們現在不能做的（除我們沒有正確解釋發生了什麼變化）
03:22 meshcollider：luke-jr：應該在這裡爭論另一方
03:22 sipa：jnewbery：我認為沒有getbalance *召喚應該包括衝突的東西
03:22 provoostenator：它應該使用mempool規則來弄清楚要忽略的交易。
03:23 sipa：provoostenator：有些事做
03:23 meshcollider：IMO將min_conf設置為0就夠了嗎？
03:23 gmaxwell：sipa：等等。我認為這將包括衝突的一方...... 
03:23 sipa：gmaxwell：哦肯定; 術語
03:23 wumpus：是不是應該讓衝突的一方不衝突？
03:23 sipa：我認為非衝突我的意思是“在mempool”？
03:23 wumpus：對
03:24 gmaxwell：好！jnewbery關於餘額下降的評論讓我感到困惑
03:24 sipa：gmaxwell：或者你認為未經證實的不受信任的非mempool沒有衝突的事情應該被計算在內嗎？
03:24 jnewbery：抱歉，我現在必須離開。我的主要觀點是，預期的行為應該有充分的記錄，並通過測試
03:24 gmaxwell：sipa：no。我不。
03:24 sipa：好的，好的
03:24 jnewbery：我已經為錢包餘額寫了一個測試腳本，但是我們需要同意在合併任何這些東西之前應該採取什麼行為
03:25 meshcollider：同意
03:25 provoostenator ：如果某些東西得到了證實，你可以從他的mempool那裡得到證實，那麼平衡變化很好，但不是。
03:25 sipa：所以getbalance如何需要minconf按照指示，並且（如果信任被指導，信任，否則在mempool中）
03:26 provoostenator：sipa：“信任”的唯一標準是它是否會改變，對？
03:26 gmaxwell：我認為如果sipa是正確的，可以通過getbalance minconf = 1 + getunconfirmed來模擬行為，那麼至少我們有一個解決方法。雖然有一種騷擾行為總是讓人感到困惑，這種行為無法通過參數的某些設置來解釋
03：26 sipa：provoostenator：或確認
03:27 gmaxwell：“getbalance的默認minconf設置是什麼？畝。getbalance輸出顯示可信輸出的minconf = 0，其他的minconf = 1。所以信任默認為true？不，沒有值得信賴的論點。“
03:28 sipa：gmaxwell：＃14602包含一個trusted_only參數，默認情況下為真
03:28 gribble：https：//github.com/bitcoin/bitcoin/issues/14602 | 修正：使用min_conf時正確計算餘額，並使用luke-jr正確計算getbalance（“ ”）·Pull Request＃14602·比特幣/比特幣·GitHub 
03:28 provoostenator：我知道錢包區分變化和不變化當涉及到支出時，這很好，但我不認為我們應該為平衡做到這一點。所以默認情況下minconf = 0應該顯示變化和不變，但不能替換為
.03：28 ryanofsky：只是想要注意，看起來我們沒有刪除GetLegacyBalance函數，所以恢復舊的getbalance是微不足道的““行為，如果我們現在無法找到更好的東西
03:28 gmaxwell：我知道14602。我試圖想像一個我們保持
現狀的世界，並嘗試釋放自己的註釋03:29 provoostenator :(至於0.17我很好釋放 - 注意我們的方式）
03:29 sipa ：哦，在我們討論如何應對之前，我只想確定所期望的行為
03:30 provoostenator：sipa：這是個好主意
03:30 sipa：我認為至少有一個粗略的結論？允許計算不受信任，但從不計算不在mempool？
03:31 gmaxwell：是的，我認為所需的行為是餘額顯示已確認+ trusted-in-mempool-0conf。並且您可以調整已確認的閾值並打開和關閉可信任的mempool-zeroconf。如果你確認= 0，它仍然應該只計入in-mempool 
03:31 provoostenator :(並且可能在unconfirmed_change_only 
03:31 gmaxwell 的行中添加第4個參數:(並且可能參數應該是minconf_for_not_you = 1 minconf_for_from_you = 0）
03:32 sipa：我認為默認的minconf = 0但trusted_only = true是有意義的;如果你選擇trusted_only = false它應該仍然只包括確認或mempool的東西
03:32 morcos：sipa：從不計算不在mempool的問題是，如果你花費10 BTC輸入來支付0.001 BTC，並且tx沒有進入你的mempool那麼你的餘額神秘地下降了10，但是多數民眾贊成難以解決
03:32 sipa：morcos：是的... 
03:32 gmaxwell：morcos：是的，我認為這很難解決，也有點好，因為你實際上已經被搞砸了：P 
03 ：33 gmaxwell：就像txn沒有確認一樣，你的資金實際上已被卡住了。
03:33 gmaxwell :(直到你放棄交易）
03:33 wumpus：right 
03:34 gmaxwell：我想我可以用任何方式論證後果，我可以想像有人丟失了一個帶有大量比特幣的錢包文件，因為它顯示由於一些容易放棄的交易導致的低餘額。
03:34 sipa：所以我認為我們可以在PR或問題上找出0.17和0.18的實現方法。這裡不需要進一步的設計？
03:34 gmaxwell：我認為盧克的公關基本上實現了我們在這裡提出的建議。但我不確定。
03:35 sipa：gmaxwell：我不確定mempool部分
03:35 wumpus：gmaxwell：在這種情況下，人們可能會使用沒有參數的'getbalance'來檢查錢包餘額，而不是具體的組合
03:35 gmaxwell：如果我們展示所有未經證實的人，包括衝突雙方，那就太糟糕了。：P 
03:36 provoostenator：Luke的PR添加了trusted_only作為第一個參數。我發現這是一個相當混亂的術語，所以希望我們可以用^ 
03:36 sipa 避免它：用什麼？
03:37 wumpus：trusted_only聽起來真的讓用戶感到困惑，如果你做了一個類似的參數你需要在RPC幫助中仔細解釋這個設置中的truste意味著什麼
03:37 sipa：同意，它需要文檔肯定
03 ：37 wumpus：它遠非顯而易見，我不知道我們是否選擇了一個好的術語
03:37 provoostenator：用你所說的：“允許計數不受信任，但永遠不要算不在mempool” 
03:38 provoostenator ：它已經是默認設置，所以可能只是重命名和記錄它。
03:38 sipa：provoostenator：它當然可以被解釋為更友好的“是否排除了來自他人的未經證實的付款” 
03:38 provoostenator：1。zero_conf_change_only（默認：false）
03:39 wumpus：sipa：
03:39 sipa：我想我們在這裡雜草
03:39 wumpus：是的，下一次otpic的時間到了嗎？
03:39 sipa：同意
03:39 provoostenator：下一個主題聽起來不錯。
03:39 wumpus：#topic 0.17.1 
03:39 BlueMatt：發佈時間！
03:39 wumpus：還剩20分鐘
03:40 BlueMatt：很酷，20分鐘後釋放？：p 
03:40 provoostenator：BlueMatt是Ubutnu的主要原因？
03:40 meshcollider：Lol 
03:40 BlueMatt：provoostenator：還有fedora，debian測試，... 
03:40 provoostenator：因為替代可能是0.17.0.2，就像我們用MacOS做的那樣。雖然我也很好，適當的0.17.1 
03:40 wumpus：仍有很多backports打開https://github.com/bitcoin/bitcoin/milestone/39我想他們需要審查，或者至少合併
03:40 BlueMatt：provoostenator：還有一些其他的bug和backports已經完成，等等
03:40 sipa：我們有一堆錯誤修正排隊
03:40 wumpus ：nah讓我們做一個正確的釋放
03:40 sipa：這可能是時間0.17.1 
03:40 BlueMatt：事情已經合併在主人
身上可能值得向後移動03:40 wumpus：現在已經太遲了0.17.0.2 IMO 
03:40 BlueMatt：因為那裡有一堆
03:41 provoostenator：對，這將涉及從0.17.0.1標籤分支並變得奇怪。
03:41 wumpus：.z版本真的是'oops我們做了一個發布，需要解決這個問題'
03:41 BlueMatt：但是，至少IMO，它超級煩人，你不能建立+運行比特幣-qt現在幾個月的版本的各種操作系統，我認為其他滾動發行版（如拱）也有這個問題
03:41 wumpus：不是一個月之後
03:41 instagibbs：我一直在崩潰，請得到14380; P 
03:41 BlueMatt：所以我希望我們不要等待修復getbalance：p 
03:41 wumpus：我同意與BlueMatt在這
03:42 BlueMatt：＃14380看起來不僅可以合併，我坐在ack部門
03:42抱怨：https：//github.com/bitcoin/bitcoin/issues/14380 | 當instagibbs指定更改輸出支出大小未知時修復斷言崩潰·請求＃14380·比特幣/比特幣·GitHub
03:42 BlueMatt：並不太難以向後移動
03:42 sipa：人們也可以看看＃14780嗎？
03:42抱怨：https：//github.com/bitcoin/bitcoin/issues/14780 | PSBT通過sipa向後移動到0.17·Pull請求＃14780·比特幣/比特幣·GitHub 
03:42 sipa :(我大部分都不熟悉
後退流程）03:43 wumpus：還沒有就getbalance達成協議，它可以等待0.17.2 03:43 
wumpus：sipa：當然！
03:43 sipa：謝謝
03:43 wumpus：sipa：請確保包含提交元數據（Github-Pull：＃...和Rebased-From：<commit>）
03:44 BlueMatt：下一主題：文本牆我剛剛發佈到bitcoin-dev：p 
03:44 wumpus :(參見其他後端PR中的提交，如https://github.com/bitcoin/bitcoin/pull/14835）
03:44 SIPA：BlueMatt：不是有
03:44 wumpus：下一個話題是魔球的
03:44點球成金：喜
03:44 BlueMatt：錯了，話題的建議
03 ：44 BlueMatt：0.17.1還有什麼？
03:45 BlueMatt：或者通常只是“讓我們今天可以合併的東西，做
後退，然後讓這件事情繼續下去” 03:45 provoostenator：BlueMatt：“由於歐盟通用數據保護法規，IRC日誌已被禁用（ GDPR）。“ 
03:45 wumpus：BlueMatt：+1 
03:45 provoostenator：+1 
03:45 wumpus：#topic提議會議主題提前（moneyball）
03:46 moneyball：我想建議人們可以使用#proposedmeetingtopic標籤隨時在這個IRC頻道中提出核心每週會議主題。我將在整個星期收集這些內容，將它們添加到任何人都可以在一周內查看的要點中。這樣做的主要目的是讓人們知道要提前討論哪些主題，以便他們做好準備。
03:46 moneyball：有什麼問題嗎？
03:46 BlueMatt：似乎合理
03:46 provoostenator：+1 
03:46 BlueMatt：比在記憶中提到他們更容易
03:46 Chris_Stewart_5：+1 
03:46 meshcollider：+1 
03:46 BlueMatt：下一個話題？#thatwaseasy 
03:47 wumpus：是的，好主意，讓我們看看它是怎麼回事
03:47 moneyball：好的我會開始做的！
03:47 wumpus：BlueMatt：好的，你的提議是什麼，我不在＃bitcoin-dev 
03:47 provoostenator：而且沒有日誌...... 
03:47 BlueMatt：哦，我的意思是比特幣 - dev ml但它還沒有通過審核但是
03:47 BlueMatt：無論如何，我可以把它
打成兩行03:47 BlueMatt：在閃電（和其他相關支付渠道-y系統）你有簽署前交易的一般問題
03:48 BlueMatt：所以你需要預測未來當對方行為不端時，網絡上的費用是
多少03:48 wumpus：#topic預簽署交易（BlueMatt）
03:48 BlueMatt：這是......顯然瘋了
03:48 BlueMatt：相反，我們（顯然）喜歡使用cpfp
03:48 BlueMatt：但是有一些cpfp rbf-pinning-ish問題，你的對手可以用大錯誤填充這個包-th-ish-feerate txn 
03:48 BlueMatt：所以你不能自己cpfp 
03:49 BlueMatt：我想建議我們調整cpfp / rbf規則
03:49 BlueMatt：添加到mempool中依賴事務包的最後一個事務必須：
03：49 BlueMatt：*只有一個未經證實的父母，
03：49 BlueMatt：*虛擬大小不超過1K。
03:49 BlueMatt :(實際上，我們首先將包大小限制減少1個1K的虛擬大小事務，然後使其最後一個必須符合這些規則）
03:49 BlueMatt：這允許cpfp通過讓閃電通道的每一側獨立cpfp而不考慮對方可能正在做什麼
03:49 provoostenator：當前RBF規則供參考：https：//github.com/bitcoin/bips /blob/master/bip-0125.mediawiki#Implementation_Details
03:50 BlueMatt：在閱讀完整的ml帖子之前想想可能太多了，但大部分只是涵蓋了背景材料
03:50 BlueMatt：/ fin 
03:50 BlueMatt :(哦，這個修復也需要包中繼，這是另一種蠕蟲本身）
03:50 sipa：這是另一個早先提出的修改：https：//lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-February /015717.html
03:50 sipa：BlueMatt：親愛的
03:51 BlueMatt：好吧，幸運的是只有一個深度的包裹繼電器，只適用於小型包裝
03:51 BlueMatt：或至少小家屬
03:51 instagibbs：抱歉cpfp如何再次固定？
03:51 instagibbs：RBF固定我知道
03:52 BlueMatt：instagibbs：A - > B其中B是100KB但是費用低，但費用很高。它同樣的問題閃電
03:52 BlueMatt：因為你不能添加到包因為包是最大尺寸
03:52 instagibbs：啊
03:52 sipa：我對此的回應是“呃......當然......但是怎麼樣？” 
03:52 instagibbs：所以這不是你可以附加的東西B'
03:52 BlueMatt：所以你必須通過rbf添加到包中，這意味著你必須增加總大小，如果你甚至可以這樣做，你必須調整rbf規則讓你用C替換B，但是你今天不能這樣做
03:52 BlueMatt：sipa：嗯？
03:52 sipa：你需要包裹繼電器... 
03:53 sipa：這不僅僅是一個小的幾行政策改變
03:53 provoostenator：另一種選擇，我忘了問題是什麼，是放棄RBF規則“3。替換交易支付至少原始交易支付的絕對費用。“並且只考慮替換的費率，無論大小。
03:53 sdaftuar：所以我認為包中繼是另一個話題
03:53 BlueMatt：我還有另一個討論封裝繼電器的bitcoin-dev帖子，但是我們有一些選擇，如果我們只是想解決像閃電這樣的合同應用的封裝繼電器，我們可以這麼做，但我認為
03 ：53 BlueMatt：如果我們想要一個更通用的解決方案我仍然認為它可能但需要更深入的ATMP重構
03:54 sipa：和P2P變化... 
03:54 BlueMatt：假設我們至少做到了這兩個中的一個，這是一個簡單的（我認為）政策變化，我希望這裡的人不要反對
03:54 BlueMatt：可能，雖然行動不是必要的
03:54 BlueMatt：但是，可能
03:54 sipa：這對我來說聽起來非常初步
03： 54 BlueMatt：我認為你的意思是包中繼部分？
03:54 BlueMatt：我認為這裡的政策規則非常簡單明了嗎？
03:55 BlueMatt：並不是非常初步，再次假設某種形式的包裹接力
03:55 sipa：我不明白你怎麼能說它不是初步的，而依靠我們不知道的東西
03:55 meshcollider：我們下週要去討論毫升
03:55 gmaxwell：MAGIC 
03:55 BlueMatt：嘿，sdaftuar和我已經打了幾個月的來回接力，但是，無論
03:56 BlueMatt：同意我們需要更加努力封裝繼電器的提議
03:56 sdaftuar：我認為佈置封裝繼電器系統的設計目標是有用的
03:56 BlueMatt：無論如何，是的，我們將在ml上討論包裝繼電器然後回到這個
03:56 sipa：BlueMatt：是的我想看到一個提議:) 
03:56 gmaxwell：BlueMatt ：關鍵在於政策變更理由對我們來說是一個黑盒子。：P 
03:56 BlueMatt：也是什麼sdaftuar說
03:56 BlueMatt：這也是包裹接力的動力
03:56 BlueMatt：作為它的另一件事來融入設計目標
03:56 BlueMatt：gmaxwell：我的意思是你認為包中繼它不是一個黑盒子？
03:56 BlueMatt：呵呵
03:57 BlueMatt：無論如何， - > ml 
03:57 provoostenator：主題建議：蒲公英stempool relay :-P 
03:57 sdaftuar hides
03:57 BlueMatt：4分鐘，GO 
03:57 BlueMatt：錯誤，3 
03:57 instagibbs：sdaftuar，你需要3分鐘才能解決它
03:58 wumpus：#topic wallet maintainer 
03:58 wumpus：meshcollider已表現出對成為錢包維護者！
03:59 provoostenator：Awesome 
03:59 sipa offer哀悼
03:59 sipa：:) 
03:59 provoostenator：Anyoe反對，不，完成。結束會議:-) 
03:59 wumpus：這是個好消息，我覺得他很擅長他，很多他的貢獻都去了錢包
03:59 meshcollider：:) 
03:59 wumpus：他已經積極的貢獻者相當一段時間
04:00 sipa：更嚴重，聽起來很棒我
04:00 achow101：+1 
04:00 wumpus：是的！
04:00 bitcoin-git：[bitcoin] vim88打開了拉取請求＃14846：文檔：將有關Scripts shebang的開髮指南添加到developer-notes.md。（主... add_scripts_development_guidelines）https://github.com/bitcoin/bitcoin/pull/14846
04:00 wumpus：好的，這是一個快速的話題，打算早點提起它但BlueMatt有點忍者:) 
04:00 wumpus：#endmeeting