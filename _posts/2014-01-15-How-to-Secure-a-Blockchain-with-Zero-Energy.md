---
title: How to Secure a Blockchain with Zero Energy
author: Max
date: 2014-01-15
layout: post
summary: I outline the shortcomings of proof-of-stake-esq systems and some challenges they must overcome.
---


Originally published in the [Bitcoin Magazine](http://bitcoinmagazine.com/9317/how-to-secure-a-blockchain-with-zero-energy/) on January 15th, 2014. Reposted here on 1st April, 2014.

[Proof of Work](https://en.bitcoin.it/wiki/Proof_of_Work) (PoW) is the only external method of powering the distributed consensus engine known as a blockchain. However, at least two alternatives have been proposed, and both are *internal* to the network (Proof of Stake (PoS), and Proof of Burn (PoB)). This is important as it uses virtual resources obtained within the network as a substitute for PoW, meaning they these methods consume virtually no energy, which has [been a](http://bitcoinmagazine.com/8994/determining-electrical-cost-bitcoin-mining/) [concern](http://www.bitcarbon.org/introduction.html) of late. The figures suggested will only occur in a system of absolute equilibrium (the market is saturated with the most efficient ASICs that are possible to produce), though even if the reality is one or two orders of magnitude lower than predicted, it is still alarming and still must be addressed.

## Proof of Stake and Proof of Burn

Both PoS and PoB use similar mechanisms. The auditor makes a sacrifice - in the case of PoS it is [coindays](http://bitcoin.stackexchange.com/questions/845/what-are-bitcoin-days-destroyed) (which are difficult to acquire; also a good [measure of economic activity](https://bitcointalk.org/index.php?topic=6172.msg90789#msg90789)), and in the case of PoB it is coins themselves (which are also difficult to acquire). Ultimately, any Proof of {something} must require a cost, whether that be electricity, coin days, or coins themselves.

Herein I suggest a fourth method, very similar to how a term deposit works (in that dusty old banking system).

## Monetary Velocity and Value of Money

The [equation of exchange](http://en.wikipedia.org/wiki/Equation_of_exchange) tells us that as velocity increases the price should decrease, and when prices decrease the value of each unit of currency increase - this is only the case *provided the monetary supply remains constant*. In a late-stage currency we would expect a relatively low level of monetary inflation / deflation (as opposed to price inflation / deflation - an important distinction), so we'll discard the concern of constant monetary supply.

In a [Proof of Stake](https://en.bitcoin.it/wiki/Proof_of_Stake) fuelled network one is required to hold currency for some time before it is able to be used to mint a block. Because it cannot be used in a transaction it is essentially removed from the monetary supply as it is unavailable for a period of time (not technically true because one can spend it up until it is used to mint a block, be the economic effect is the same either way in terms of velocity). Because the money supply will *effectively* (but doesn't actually) decrease, prices should also fall by a small amount. One can imagine the network saying "Here is a small reward for temporarily removing your coins from the supply and making us all a little more wealthy, *in addition to auditing and securing the network*."

[Proof of Burn](https://en.bitcoin.it/wiki/Proof_of_burn) is used in a similar fashion: coins are destroyed in an unspendable transaction which is *not immediately obvious* to the network (the author suggests using a [P2SH](https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki) address). At some later date this is revealed and used to create a block. The miner is then rewarded with new coins and/or transactions fees (presumably more than the coins they've burned, else they've made a loss). This is like the network saying "Here's a small reward for temporarily removing your coins from the supply and making us a little more wealthy, *in addition to auditing and securing the network*". Huh, that sounds familiar.

While they may sound very similar, there are a few differences in terms of public knowledge. In both cases it is unknown how many coins have been left waiting in the wings (similar to how it is impossible to tell how many bitcoins have been lost or abandoned over the years), though PoB provides a little more specificity allowing us to determine a narrower range of candidates (unspent P2SH addresses) than PoS (which includes all unspent transactions). The volume of coins in each case is also an indicator, as in both cases there will be some effective minimum required. However, PoB implies the number of coins burnt cannot be set in advance as both the date of redemption and volume of burnt coins are unknown. PoS does not destroy coins and so any extra volume of coindays destroyed is less important. These differences are subtle, but may become important as the systems are explored more deeply.

Economically speaking, the basis of both proofing systems relies on relinquishing the ability to use coins for some time. In PoS this is voluntary and the funds are spendable at any time, whereas in PoB uses a rather more permanent operation so the user commits immediately to mining a block in the future, regardless of whether it is profitable or not (provided they meet the difficulty requirement, else the coins may be lost forever; perhaps pooled mining might alleviate this concern, though), but the length of time till that utility will be used is unknown. In this case, as the ability to use coins is relinquished, there is no possibility they will increase monetary velocity and thus should (in theory) increase the value of the each coin in the total supply.

## Proof of Deposit

[Proof of Deposit](https://bitcointalk.org/index.php?topic=386460.0) (or PoD) fills a medium between the two methods. Simply put, PoD blocks have a difficulty proportional (or equal) to the amount of coins that must be offered for ‘deposit’ and have a known block reward. Deposited coins remain untouchable for some length of time and the block reward is delivered to the miner (either immediately or over a period of time like a dividend or interest payments). As there is one deposit per block there are a limited number of deposits available each year, and if deposits are appearing too fast then the return must be too high, so the difficulty is increased (which implies the return is lowered) and thus demand decreases. Our personified network might once again say “Here’s a small reward for temporarily removing your coins from the supply and making us a little more wealthy, in addition to auditing and securing the network.”

### That’s getting awfully familiar…

Why yes, it is. This should come as no surprise, though. What resources are there internal to a currency besides the currency itself? Economically speaking, there’s very little substantive difference between these three methods, and their monetary implications are very similar; the main difference is the physical actions that help it propagate. If, however, humans are psychologically biased to one way over another, then those physical actions are exactly the things that will count in a showdown between these proofing methods.

## Does it even work?

This is really the only important question here. If none of these schemes work, do we have a reason to care? A discerning reader like yourself might have noticed something peculiar about these three methods: you need money to make money. Without internal resources existing the network has no fuel.

Peercoin mitigates this concern by using both PoW and PoS in combination to create new blocks. Over time PoW blocks become less frequent and PoS blocks become more frequent, so it should eventually lead to an energy efficient network (or at least more so than the Bitcoin network). Whether this will pan out or not is difficult to say; the reward for attacking Peercoin is far lower than a well executed attack on Bitcoin, and without an increase in Peercoin’s popularity and/or accessibility we might never discover how easy an attack really is.

## Where to from here?

The possibility of a zero energy currency is not something that should go without research, but should also be approached with a degree of scepticism. It has been argued that monetary monocultures [contribute to financial instability](http://www.lietaer.com/images/Journal_Future_Studies_final.pdf) due to the lower resilience of a homogeneous system (compared to one of high diversity). Is it possible that a reliance on internal states causes instability more generally, even in a currency that has no resistance to opt in to or out of? If it is still the case, can we build several different sorts of these systems together to help provide that resilience? Can one network’s security rely on actions in one or several other distinct currencies? These are important economic questions that may have profound consequences for the future of finance; they are novel because systems of this precision have been impossible under legal frameworks, and never before has any person been able to create a truly global currency in their garage. Experimentation is the future of currency, and I am excited to watch it happen.
