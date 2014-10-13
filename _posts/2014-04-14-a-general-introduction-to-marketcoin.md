---
layout: post
title:  A General Introduction to Marketcoin
author: Max Kaye
date:   2014-04-14 00:00:00
categories: marketcoin grachten
---

Originally published at [eudemonia.io](http://eudemonia.io/2014/04/a-general-introduction-to-marketcoin.html).

Eleven months ago I started planning Marketcoin and since then I've not described the updated design.
It has changed significantly since I first described it, and is far superior in many aspects.

Herein I'll describe what Marketcoin is designed to do, sometimes with little or no justification to how it is achieved.
The implementation is highly technical and does not belong in a general introduction.

Marketcoin is an idea that manifests in a novel fashion.
It's a bit like Bitcoin, and a bit like Mastercoin, and a bit like Ethereum, but also like none of them in many ways.
It's not any one single network, but many that are able to communicate and transfer value from chain to chain.
They're able to share a common unit of a consistent value across all chains supporting the correct standard.
It is self pruning and selects on the most efficient markets, while still enabling diversity and innovation.
It is a parallel cryptonet designed to span the Internet and enable trustless trade between both old and new chains.

Markets can be hosted anywhere, on any chain, but there will be a central hash rate source where most market-chains live by default, known as the Grachten.
A market-chain may host many markets but the central unit is always common.
This communal living is an important design decision for market-chains because it provides an environment where high quality markets can grow that have some level of mutual quality assurance due to their competitive environment.
A high quality neighbourhood is important as chains will have to communicate to move the central unit between them; remember that confidence in the chain is inversely proportional to required confirmations, so less secure chains will naturally be slower to interact with their peers.
Just as Namecoin is merge-mined with Bitcoin, market-chains can be merge-mined with the Grachten.
Unlike the Namecoin / Bitcoin relationship, though, the Grachten has limited space, and it becomes more and more difficult to produce blocks as a miner attempts to include more data.
For this reason cryptographic authentication is deferred to the Grachten, providing a competitive environment where market-chains can prove their efficiency.
The more coins stored on that chain the higher the block reward is, increasing the incentive for a miner to mine that chain.
Two chains competing for the same currency pair will each hinder the efforts of the other, so once one gains a majority the weaker will atrophy until it is discarded.

The main idea of Marketcoin is to provide a fair and unbiased market on which to trade various cryptocurrency and other smart properties.
In the same way a human watches the Bitcoin blockchain to wait for payment, Marketcoin watches the Bitcoin blockchain to confirm trades.
Since there is some internal unit and an external unit, it is conceptually easy to see that an exchange can take place.

The actual market design used in a market-chain can be of the community's choosing, however, a blockchain provides unique challenges that traditional market structures do not neatly fit.
The proof of concept (PoC) due out in the near future will demonstrate a design based on a modified call market.
Since orders must be inserted into the order book whether they are executed immediately or not, no distinction is made between orders waiting in the order book and orders made immediately.
Due to the near perfect-information state of cryptonets, it's likely a market will react to an order before it is executed - helping to create liquidity and competition around every trade.

A typical market-chain will experience the following phenomena:

* Every minute or two a market update will be produced, solidifying orders still floating around the network and helping to prevent manipulation on the part of miners - orders are added to the order-book but not executed.
* Every 15 minutes or so the market will execute, clearing all overlapping trades.
This aspect is similar to a call market.
Part of the design requires that this cannot be predicted.
* Orders will be prioritised in terms of how good a 'deal' they are.
A user wishing to sell the central unit for very little, or buy at a high price will be preferenced over a user who is less generous in their offer.
* The highest bid is matched with the lowest ask, and the price of the trade is decided to be the average of the two offers.
One or both of the trades is consumed fully and the remainder is added to the top of the respective order-book.
* This continues until there is no overlap between bids and asks.
* As a consequence there is no longer a spread in the market, but an uncertainty in the price appears instead.
(During simulations this was ~0.3% at a maximum, and usually less; since this is less than or on par with most exchange fees it's counted as negligible.
As liquidity rises this error will fall, except in times of volatility.)
* Furthermore, a large trade at a good price will generate a lot of interest, and the potential of profit will cause traders to actively compete for a slice of the trade.
* To compete traders must make a generous offer in the other direction, and so their competition benefits the market as a whole, both by increasing liquidity and by helping to maintain price stability.
* Due to the uncertainty of the market, it is possible to have two opposing trades in the same execution and make a profit (it is also possible to make a loss).
Whether this is an advantage or disadvantage is relative to the user in question.

There is a possibility of miners using their power to manipulate the orderbook slightly in their favour before offering a block, however, execution is always at the beginning of a block ensuring only existing orders are executed, preventing too much manipulation on the part of a miner.
They can, however, manipulate the orderbook very slightly with every block they produce, so that if the next block happens to invoke an execution they will be slightly advantaged.
By analogy, this is the high frequency trading of Marketcoin - both are simply having a say when it most counts.

It should be evident at this point that novel market structures are easily implemented under Marketcoin, allowing the most efficient and desired market structure to emerge.
This is an excellent example of the neutrality of Marketcoin's design.

While one market-chain may only support a few currency pairs (more may prove too cumbersome), other market-chains are easy to create and can maintain a two-way peg with the central unit provided a standard is followed.
This standard dictates a few aspects important to the network.
For example, the rate of central unit generation as a block reward should be proportional to the number of central units stored on that chain and inversely proportional to the block frequency of that chain.
Since market-chains are designed to coexist on shared hashing power they have a natural resilience to changes in block production times, and the reward adjusts accordingly.

Creating a new market-chain will be extremely accessible (we're going to provide a library) but maintaining one is very costly (you have to convince people to mine it in a competitive environment).
Because of this combination, I anticipate there will be a great evolutionary synergy, whereby there is no central Marketcoin chain and the central unit exists between many chains, abandoning them as they become insignificant and jumping on those that prove useful, novel, or advantageous.
The unit of value will be extricated from the confines of just one blockchain, allowing for innovation not just in market structure but blockchain technology - all without needing hard-forks.

Marketcoin is designed to be *the* solution to distributed exchange: from an ethical launch to evolutionary agility, we want to cover every base to ensure the longevity of such an ambitious project.
