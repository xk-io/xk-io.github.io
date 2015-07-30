---
#title: Decentralizing Bitcoin Development Forever with Git, GitTorrent, Lighthouse, and BlocVoting
title: How To Decentralize Bitcoin Development Forever
date: 2015-07-23
comments: true
layout: post
author: Max Kaye
summary: Using Bitcoin, Git, GitTorrent, and BlocVoting, I propose a method to find consensus on canonical source code for the Bitcoin network. This solves the 'tyrannical developer' problem.
---

## Introduction

Development of Bitcoin has become dysfunctional. This post isn't about either side of the block size debate, though the quality of this debate is the inspiration for this post. While the correct course of action may not be apparent, the divide in the community (and corresponding lack of direction) is apparent.

However, some of the community seems stead fast in finding a solution and moving forward in particular directions against the advice of some core developers. Unfortunately, we currently lack the ability to determine who truly has the most support in the public debate, or even if it is one sided. Herein I propose a way to:

* Fund core development, and
* Determine the source code used for compilation in a decentralized manner

All of this occurs on-blockchain where needed, and there are no trusted entities besides the compiler-maintainers, which can again be chosen in a similar decentralized manner. In the future perhaps we can use zero knowledge proofs to decentralize the compiling stage, but for the moment this is not considered.

This proposal requires bitcoins to be *burnt*, or destroyed, in order to form consensus. While this may be unpalatable for some, it provides a way to secure the distributed consensus.

## Ingredients

There are four key parts to this proposal:

* Bitcoin
* Git
* [GitTorrent][2] - decentralized git hosting
* [BlocVoting][4] - delegative democracy on the blockchain

I presume the reader is familiar with the first two: Bitcoin and Git. Bitcoin provides the blockchain and Git provides our method of managing source code.

[GitTorrent][2] is a recent development that allows accessing and hosting source code via a DHT, similar to accessing torrents via magnet links.

[BlocVoting][4] is a protocol of my own design that faciliatates [delegative democracy][1] (or liquid democracy) on the blockchain.

## The Burn-Graph

Bitcoin offers us an important lesson: the irreversible conversion or destruction of resources provides a method for converging to consensus in a distributed manner. By burning coins in a way that resembles proof-of-work we can secure a blockchain like structure to manage identities.

Coins are burnt by sending them to an OP_RETURN output that contains linking information, among other things. Each burn transaction points to one or two previous burn transactions, which in turn points to previous burn transactions, etc. In this way, starting from a genesis burn tx, a graph (or list) of burnings can form. Like the blockchain has a "top block", the burn-graph will have one node with more coins *cumulativley* burnt than any other. This is the head of the graph, and used as the basis of the weighting system. In this way, an identities weighting is determined by the volume of resources destroyed (number of coins). Because a weighting will only be obtained if the burning is inside the burn-graph, there is an incentive to work off the top, in the same way that Bitcoin incentivises mining on top of the Bitcoin chain.

> Aside: exponentially increasing the weighting with respect to time may be required in order to ensure old burnings don't interfere with recent burnings.

After the burn-graph is established we can extract a map (or dictionary, or list of key, value pairs) that will continually be updated. This map is between identity (which can be a Bitcoin address) and weighting. One increases their weighting by burning more coins.

## Membership and Voting

Using this map as a membership list (open to anyone willing to participate in the burn-graph) we can then allocate the number of votes for that identity based on the weighting. Votes could be used to indicated current preference for the *hash* of the *git commit* which they prefer as the *canonical* source used for Bitcoin compilation. One option would be to implement direct democracy on the blockchain, but that would be inefficient.

Instead, I propose an implementation of [Delegative Democracy][1]. This would allow most individuals (who do not have the technical prowess needed to read and understand Bitcoin source code) to choose a delegate, which they can change at any time, who can vote on their behalf. This delegate may in turn have a delegate of their own. This allows core developers to hold the same responsibility and power as they have in the past, until they are unable to solve problems effectively amongst themselves. This inevitably happens from time to time, and so at this point the next layer of delegates can take matters into their own hands and vote directly. If this increase in participation is still unable to solve the issue, the process can continue until we reach something similar to direct democracy where *everyone* is participating.

Furthermore, when there is little controversy within the community delegative democracy is incredibly light, perhaps requiring only a few kilobytes per release cycle. During times of controversy it is natural that participation will rise, and so the space requirements will rise accordingly.

> Disclosure: I am developing an on-blockchain implementation of delegative democracy called [BlocVoting][4].

This voting network would not physically transfer tokens as some voting proposals do. Rather a weighted graph of voters would be established and evaluated for each ballot.

## Hosting Source Code

While (at this stage) we could hook up a git server to read the blockchain and publish information about the current git head, we can do better.

Using [GitTorrent][2] ([source code][3]) we can decentralize the source-code-hosting problem. Because we can decide on the latest commit with respect to the blockchain we no longer need to reference a) a hosted git repository, or b) a central authority. (These are the only two methods originally suggested, though the author does talk about using blockchain name resolution.) In this case, running a node to store and provide access to the Bitcoin source code would help the network (especially a node that tries to include as many branches as possible).

At this point we can decide what source code to use with a voting network, which is in itself managed via an open opt-in proof-of-burn based algorithm. Furthermore we can host and access this code trustlessly.

The final problem to solve is source code distribution. The same voting network is capable of voting on compiler-maintainers. These would be public key identities (probably well connected to real world identities) that would be responsible for deterministically compiling and hosting Bitcoin binaries, based on what the most recent ballot yeilded as the git head. In this way we could at least know if any funny business was going on by comparing the various compiled binaries. There is the potential to decentralize this further, but for the moment the above is considered sufficient.

## Funding Core Development

At the beginning I mentioned funding core development, though that has remained absent until now. There is no way that I know of to integrate this sort of funding in such a way that does not provide an advantage for an attacker. However, with sensible defaults we can heavily mitigate this posibiltiy.

One possibility is for the protocol to mandate each vote requires 2 outputs with some ratio between the values (such as 1:1). One is an OP_RETURN output, and one standard output. By *default* users would be encouraged to select a core developer to donate to, though they could specify any address (including their own) to direct the second output at. Whether to include this at all is a design decision perhaps best left for later, but the possibility of funding development is tantalizing.

## Summary

Using some novel technology and the immutability of the blockchain we can construct a framework to help manage decisions around what code to include in Bitcoin, including hard-forks and block-size updates. The unique combination of these technologies allows for a completely decentralized development process without the implicit trust that the Bitcoin community has endured (and now suffers from).

[1]: https://en.wikipedia.org/wiki/Delegative_democracy
[2]: http://blog.printf.net/articles/2015/05/29/announcing-gittorrent-a-decentralized-github/
[3]: https://github.com/cjb/GitTorrent
[4]: https://github.com/xertrov/blocvoting
