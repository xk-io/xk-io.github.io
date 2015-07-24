---
#title: Decentralizing Bitcoin Development Forever with Git, GitTorrent, Lighthouse, and BlocVoting
title: Decentralizing Bitcoin Development Forever
date: 2015-07-23
comments: true
layout: post
author: Max Kaye
description: Using Git, GitTorrent, Lighthouse, and BlocVoting, I provide a framework for beginning the decentralization process around Bitcoin source code. This solves the 'tyrannical developer' problem.
---

The recent block size debate in the Bitcoin community highlights a key flaw of the 'benevolent dictator' or oligarchical/technocratic models of open source software development.
The core development community has become dysfunctional and is unable to work cooperatively due to the current arrangement. However, some of the community seems
stead fast in finding a solution and moving forward in particular directions against the advice of some core developers.
Unfortunately, we currently lack the ability to determine who truly
has the most support in the public debate, or even if it is one sided. Herein I propose a way to:

* Fund core development, and
* Determine the source code used for compilation in a decentralized manner

All of this occurs on-blockchain where needed, and there are no trusted entities besides the compiler-maintainers, which can again be chosen in a similar decentralized manner. In the future perhaps we can use zero knowledge proofs to decentralize the compiling stage, but for the moment this is not considered.

The key ingredients are:

* Git: source code graphs referenced via hash.
* [GitTorrent](https://github.com/cjb/GitTorrent): essentially a git repository hosted in a DHT, indexed by git hashes in a similar way to bittorrent magnet links.
* [Lighthouse (with some modifications)](https://github.com/vinumeris/lighthouse): Decentralized crowd funding used to pay Bitcoin developers and weight votes.
* [BlocVoting](): Decentralized voting on the blockchain implementing delegative democracy; each voter is empowered in proportion to their monetary contributions via Lighthouse.

Git is fairly self explanatory: that's how we pass code between ourselves and make sure we have the right code. GitTorrent allows us to host this on a DHT to remove central authors as exists on GitHub, for example.

Lighthouse provides our method of decentralized fundraising, for the most part, but some modifications are necessary in order to decide *which* fundraisers should be used for vote weighting. Continuous funding will be required to build the funding-chain, which can be added to with bounty-esq funding rounds too. This funding-chain will -- similar to PoW -- help funding converge into a chain-like graph. The funding-chain can be built using metadata through OP_RETURN outputs. By pointing to past elements of the funding-chain (which is really a directed acyclic graph so we can have multiple parents) we are able to build a core chain of regular funding, and then tack on other improvements (that may or may not be controversial) to add features or alter the protocol. Currently some sort of irreversible resource consumption is required to avoid bad actors falsely funding themselves (again, similar to PoW). Destroying coins is a naïve way to achieve this, though perhaps in the future this can be somewhat integrated into Bitcoin (or an AuxPoW chain) to avoid the destruction of coins.

BlocVoting is a protocol of my own design to facilitate [liquid democracy](https://www.youtube.com/watch?v=fg0_Vhldz-8) / [delegative democracy](https://en.wikipedia.org/wiki/Delegative_democracy) on the blockchain. By reading the various identities and funding amounts from the funding-chain we can establish a weighted voting network where decision power is vested in those individuals who have contributed. This decision power can be held by delegates most of the time: I imagine that trusted community members would make most (boring) decisions, but when something like the block size debate emerges users can take their vote back from their delegate to ensure their funding commitment is well vested. The result is an elegant tree-like structure that morphs in response to community concerns.

By using this voting protocol we can, on a regular basis, decide on the exact source code to use for official binaries and codebase. We can additionally vote on which community members to trust to maintain a gitian build bot that produces deterministic binaries based on the current head (which is determined through the voting network). Since these builds are deterministic any funny business can be immediately detected. Although decentralizing this step would be nice, I don't think it is necessary (yet), *and* it provides the nice benefit of allowing them to act as veto-ers in the case of an attack.
