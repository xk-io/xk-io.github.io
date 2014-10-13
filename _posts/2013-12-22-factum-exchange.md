---
title: Introducing Factum Exchange
layout: post
author: Max
date: 2013-12-22
---

# Introducing Factum Exchange

In my [first post](FactumMoney.md) in the factum series I looked at Factum Money, a new category of money which has no non-financial use (or if there is a non-financial use, it is a distance second when ranked by utility), and has no extrinsic requirement to hold value. That is to say, the main utility of Factum Money is as money, and we can see this by looking at the properties of said money and *nothing more*.

Commodity money and commodity backed money have common non-financial uses and often this is their primary use, and it is thus trivial to see they are not factum money. Fiat money (such as common government issued monies in use today) has no substantial non-financial use, however, by looking solely at the construction of fiat money we can see that it is not guaranteed to have a non-zero value. Most (if not all) of the time fiat money will acquire value through the exercise of authority, which almost ubiquitously takes a legal form.

Bitcoin, however, satisfies both requirements; it is a purely financial instrument (though it's technical implementation leads to other uses, like storing data in the blockchain) *and* one can see that Bitcoin has a non-zero (or should we say *intrinsic*) value by a pure examination of the internal mechanism.

## Markets and Exchange

Money is a multidimensional problem. Sending value to other parties is all good and well, but there must exist a means of exchanging between monies; without One World Currency there will exist some merchants who won't accept your preferred flavour of money and some clients who don't have any of the flavours you accept.

Traditionally currencies are exchanged in an environment outside the system of money itself. They are walled off from the outside and require specific entry and exit procedures. These procedures are a method of deferring value (mentioned in the first in the factum series). Take the best known BTC/USD exchange: MtGox. The deposit process, for both USD and BTC, involves P1 (the first party) relinquishing their funds, and in return they are issued fungible tokens that operate within the MtGox environment, but are incompatible with any other payment network. These tokens have the unique property (belonging to none of their parents) of being exchangeable for other tokens (denominated in a different currency) on the market provided by MtGox. Thus tokens from P1 are swapped for tokens from P2 (the second party), and both parties direct the value back into their original forms, and the exchange is complete.

By issuing tokens for USD or BTC, MtGox are deferring the value. Put another way, the tokens only have value because of something we know about then outside of their construction: there is a legal gateway allowing value to flow into and out of the MtGox zone.

Because of the similarity in the constructions of tokens in these markets, and the construction of fiat money and commodity backed money, I feel it is appropriate to label these systems **Fiat Exchanges**. Two forms of fiat money are being traded. No real BTC is traded on the MtGox exchange, only MtGox-BTC -- a petty shadow by comparison.

There exists, however, another form of exchange. In this form the monies themselves are exchanged; not tokens in a segregated environment. When the two of us exchange gold coins for silver, the exchange takes place in an environment native to the subjects of the exchange (in this case the real world). A factum exchange that operates using Bitcoin would satisfy the same criterion; the exchange takes place in an environment native to the subjects of the exchange (the blockchain). Transactions on the Bitcoin network and transactions involved in the exchange are *one and the same* (in this hypothetical exchange system).

These exchanges, whether they involve real world objects or cryptocurrencies, will be labelled **Factum Exchanges**. In these cases, the ability for exchange to occur is built into the payment networks -- in the case of gold it is the physical transfer, in the case of Bitcoin it is a transaction on the network. When a factum exchange operates over factum money (and possible some fiat money) there should be no possibility of any particular exchange being censored, blocked, regulated, etc. There should only be two possibilities: the exchange fails (and the original money is returned) or the exchange succeeds (and both parties swap as agreed).

It is possible to host a factum exchange over fiat currencies. An exchange in person, or through banking networks, can be called a factum exchange because value is not deferred from the subjects of the exchange.

### A Note on Cryptocurrencies

Although Bitcoin is a form of factum money, not all crypto currency needs to be. One can easily imagine a crypto currency minted by a central bank, and although mining might be decentralised, supply of the money is still regulated by the bank (even with distributed wealth generation). This would count as fiat currency because there is zero assurance (excepting legal agreements) that the currency won't be inflated through the roof. If the private key were compromised this would be an inevitability.

Cryptocurrency could even be a form of commodity backed money, but we shan't explore that here.

## Exchange and Distributed Exchange

The Bitcoin community has felt the thorns of regulation for some time. Traditional methods of currency exchange are stifling growth and promoting unhealthy markets (such as we're seeing in the exchange differential between USD/BTC markets on MtGox, Bitstamp, and BTC-e). The Bitcoin community owes it to itself to build tools to better allow for this exchange, and to investigate what is going wrong currently (so we know how and to build, and the purpose of such tools).

The current system looks like this: (using MtGox as an example)

```
    TITLE: USING MTGOX TO CONVERT BETWEEN BITCOIN AND USD
    ________________________________________________________________
    BITCOIN 
     P1-->MTG-------+                                +--MTG-->P2
    ________________|________________________________|______________
    USD             |                                |
     P2==>MTG-----+ |                                | +--MTG==>P1   (insert joke here
    ______________|_|________________________________|_|____________  about never get-
                  | |                                | |              ting fiat out of
                  | |                                | |              MtGox)
    MTGOX         | |                                | |
    ______________|_|________________________________|_|____________
                  | +-M>P1(BTC)----#X->P2(BTC)-D>MTG-+ |
                  +---M>P2(USD)-#---X->P1(USD)-D>MTG---+
    ________________________________________________________________
    
    
    LEGEND
    -   : Path of Action, horizontal
    |   : Path of Action, vertical
    +   : Path of Action, corner; if two paths intersect, their direction is unchanged
    .   : Path of Funds in Escrow
    >   : Transaction to
    #   : Order Placed
    •   : Block Produced (alt 8)
    X   : Exchange Matched
    @   : Proof of Payment
    &   : Escrow Unlock
    =   : Stress on Path of Action (e.g. Regulation)
    M   : Mint coins/tokens
    D   : Destroy / Unmint
    
    Cn  : for an integer n, custom action, details provided with graph
    
    P1  : The First Party, always refers to the same people
    Pn  : for any integer n, as above
    En  : for any integer n, a special escrow account, details provided with graph
    PN  : The Nth Party, can be anyone and can be a different party every time
    ABC : Three letter abbreviation of a real world entity.
    
    RULES - The following excludes paths and transactions:
    - When two icons appear next to each other they are simultaneous. Their order 
        preserves causality.
    - When two icons are in the same column they are simultaneous.
    - If two icons are in adjacent columns but different rows they are not 
        necessarily simultaneous.
    - If two icons are adjacent and there is a third in a column shared with one of 
        these icons, all three are simultaneous.
```
    
The regulatory efforts are applied to the fiat entry and exit points, with = indicating where those stresses are felt. The MtGox infrastructure requires value to be deferred into compatible tokens, which is the choke point in this system. If direct person to person transactions in USD were used instead, the regulator pressure would fall away. Unfortunately this isn't able to be checked from within the MtGox infrastructure, and thus relies on manual verification, in turn allowing for a number of attacks that make the system too burdensome to use.

### The First Distributed Exchange: Ripple

A system such as Ripple looks like this:


```
    TITLE: USING RIPPLE TO CONVERT BETWEEN BITCOIN AND USD
    __________________________________________________________
    BITCOIN 
     P1-->BTS---+                                 +-BTS->P2
    ____________|_________________________________|___________
    USD         |                                 |
     P2==>BTS-+ |                                 | +-BTS=>P1
    __________|_|_________________________________|_|_________
              | |                                 | |
              | |                                 | |
    RIPPLE    | |                                 | |
    __________|_|_________________________________|_|_________
              | +--M>P1(BTC)-#----X>P2(BTC)-D>BTS-+ |
              +----M>P2(USD)-----#X>P1(USD)-D>BTS---+
    __________________________________________________________
    
    LEGEND
    -|+ : Path of Action, horizontal,vertical,corner
    >   : Transaction to
    #   : Order Placed
    X   : Exchange Matched
    =   : Stress on Path of Action (e.g. Regulation)
    M   : Mint coins/tokens
    D   : Destroy / Unmint
```


It is nearly identical to MtGox, and involves using a payment processor to cash in and out. Bitstamp (BTS) was chosen here as it is a 'gateway' into the Ripple system for both Bitcoin and USD. It can be replaced with any other gateway, though additional steps are required. Ultimately this provides no advantage over the traditional model (see MtGox, above) besides that there are more options to cash in and out (though you have to exchange Bitstamp-USD for OtherGateway-USD as the two aren't fungible). I guess you'd say it's better than MtGox, but not substantially.

### Cross Chain Trade

This algorithm is taken from the [Contracts](https://en.bitcoin.it/wiki/Contracts) page.


```
    TITLE: SIMPLE CROSS CHAIN TRADE BETWEEN BITCOIN AND LITECOIN
    _____________________________________
    BITCOIN 
     P1------X->E1-•-C1------C2-->P2
    _________|___________________________
    LITECOIN |
     P2------X-------->E2-•->P1
    _____________________________________
    
    LEGEND
    -|+ : Path of Action, horizontal,vertical,corner
    >   : Transaction to
    •   : Block Produced (alt 8)
    X   : Exchange Matched
    
    E1 and E2 are both transactions to the following output:
        <Pubkey> OP_CHECKSIGVERIFY OP_HASH256 <HashOfX> OP_EQUAL
    Redeemed by:
        <X> <Sig>
        
    C1 - P1 tells P2 about the transaction
    C2 - P1 tells P2 the secret (X) OR P1 spends the TX, making the secret public.
```

    
Cross chain trade looks fairly simple, but in reality there is no market built behind it, so much of the communication is manual. This might be solved with some distributed layer over the top, but there is still the issue of P1 keeping X secret, locking funds away forever. There has been a suggested solution to this that involves timeout periods. This makes things a little more difficult:


```
    TITLE: ZERO-LOSS CROSS CHAIN TRADE BETWEEN BITCOIN AND LITECOIN
    _______________________________________________
    BITCOIN 
     P1------X------C1------C3->E1--C5--•->P2
    _________|_____/__\____/__\____/__\____________
    LITECOIN |    /    \  /    \  /    \
     P2------X--C0------C2------C4->E2----•->P1
    _______________________________________________
    
    LEGEND
    -|+ : Path of Action, horizontal,vertical,corner
    >   : Transaction to
    •   : Block Produced (alt 8)
    X   : Exchange Matched
    
    E1 and E2 are both transactions to the following output:
        OP_IF 
            <PubkeyYou> OP_CHECKSIGVERIFY OP_HASH256 <HashOfX> 
            OP_EQUALVERIFY OP_HASH256 <HashOfY> OP_EQUAL 
        OP_ELSE 
            2 <PubkeyYou> <PubkeyMe> 2 OP_CHECKMULTISIG 
        OP_ENDIF
    Redeemed by:
        0 <Sig> <Sig> 
            OR
        1 <Y> <X> <Sig>
        
    The flow of information between the Cn events are shown with slashes.
    C0 - P2 tells P1 <HashOfY>
    C1 - P1 telling P2 the E1 transaction, and <HashOfX>, unsigned, and providing 
         a reversal transaction R1.
        
        * R1 is locked for 48 hours
        * Rn is a reversal transaction from En>Pn. It has a lock time far in the future, 
          and far from the time the lock time of the other reversal, if it is known.
        
    C2 - P2 verifying E1, signing and returning R1, P2 also tells P1
         about the E2 tx, unsigned, and provides R2.
    
        * R2 is locked for 24 hours
    
    C3 - P1 verifies E2, inspects R2, signs, and returns. P1 signs R1 and 
         signs and broadcasts E1.
    C4 - P2 verifies E1 has been broadcast, signs 
         and broadcasts E2. P2 tells P1 <Y>
    C5 - P1 tells P2 <X>, either explicitly or by spending the transaction
```

    
In this case the trade will never fail: after R2 becomes active it is unsafe for P1 provide the secret X. Thus, if P1 is unable to redeem E2 she can wait for R1 become active. By placing the burden of providing the secret on P2, the transaction with the first reversal is guaranteed to occur first.

However, the cost of using this method is great; many confirmations are required for individuals to be certain they are safe executing the next step and there is a great deal of time for either party to renege on the transaction after the terms of exchange are set. Furthermore a reorganisation on one chain could lead to one party with both sides of the transaction.

### Other Distributed Fiat Exchanges (Hypothetical)

None of these have been completed to my knowledge. They typically allow the creation of assets backed by some value (fiat), or offered IPO style (possibly fiat or factum).

Typically, a generic fiat exchange (GFiX) will take the following form:


```
    TITLE: GENERIC FIAT EXCHANGE (GFiX) - BITCOIN TO USD
    ___________________________________________________
    BITCOIN 
     P1-->BTS---+                         +-BRK-->P2
    ____________|_________________________|____________
    USD         |                         |
     P2==>BRK-+ |                         | +-BRK==>P1
    __________|_|_________________________|_|__________
              | |                         | |
              | |                         | |
    GFiX      | |                         | |
    __________|_|_________________________|_|____________
    BTC       | +-M>P1-#-•...•X&>P2-D>BRK-+ |
              |               |             |        
    __________|_______________|_____________|____________
    USD       |               |             |       
              +---M>P2---•-#-•X>P1--D>BRK---+
    __________________________________________________
    
    LEGEND
    -|+ : Path of Action, horizontal,vertical,corner
    .   : Path of Funds in Escrow
    >   : Transaction to
    #   : Order Placed
    •   : Block Produced (alt 8)
    X   : Exchange Matched
    &   : Escrow Unlock
    =   : Stress on Path of Action (e.g. Regulation)
    M   : Mint coins/tokens
    D   : Destroy / Unmint
    
    BRK : Broker
```


### Existing and Future Factum Exchanges

#### Mastercoin

Note: Marstercoin is a layer over Bitcoin (data stored in TXs on the Bitcoin network) and thus blocks occur at the same time.
Note: The following may be incorrect. I've scraped together some information but details of the spec are pretty thin.


```
    TITLE: EXCHANGING BITCOIN FOR MASTERCOIN
    _______________________________
    BITCOIN 
     P1----------C1#-•X-->P2 •
    __________________|____________
    MASTERCOIN        |   
     P2--------#-----•X......•&>P1
    _______________________________
    
    C1 - Buyer selects order to fill

```

    
In english:

* An order is placed on the Mastercoin network (sell)
* A buyer finds and decides to fill that order (buy)
* They publish the order, and away the next block
* When the next block arrives the orders are matched and the Mastercoin asset goes into pseudo-escrow
* Once P1 pays P2 in the required specific manner, Mastercoin unlocks the escrow and transfers the assets to P1

One issue is the buyer (of MSC) is able to renege on the trade before it is complete; this, however, is an issue with any asynchronous exchange. The process here is simpler than other asynchronous models because it is only possible to trade between Bitcoin and Mastercoin, and Mastercoin has interchain awareness to Bitcoin; when an order is filled (and paid for) the Mastercoin chain can release funds automagically. A 'pledge' system could easily be implemented to indicate one's intent to purchase. A market system could be implemented to remove the need to choose an order to fill.

#### Marketcoin

Marketcoin is a hypothetical currency/market I've begun to set out [here](https://github.com/XertroV/MarketcoinWhitepaper)


```
    TITLE: EXCHANGING BITCOIN FOR MARKETCOIN - ANNOTATED
           ASYMMETRIC EXCHANGE
                +-- P1 places an order on the MKC network to buy (with pledge)
                |    +-- Exchange matched, unacknowledged on bitcoin network
                |    |     +-- P1 sends coins to P2 as agreed
                |    |     |   +-- BTC block mined
    _____________________________________
    BITCOIN            +---------+
     P1---------+----X-+-P1>P2 • |
    ____________|____|___________|_______
    MARKETCOIN  #    |           @
     P2-----#-------•X.............•&>P1
    _____________________________________
            |        |           | +-- When an MKC block is mined,
            |        |           |     the MKC in escrow is released to P1
            |        |           +-- P1 provides proof of tx to MKC network
            |        +-- MKC Block produced, exchange matched
            |            P2's funds put in escrow     
            +-- P2 places an order on the MKC network to sell 

```

    
In english:

* P2 places bid
* P1 places ask (with pledge)
* When an MKC block is created and the orders are matched, P2's MKC is put into escrow, redeemable by P1
* P1 then transfers correct amount of BTC to P2
* A Bitcoin block is mined including this transaction
* P1 provides proof of payment to the Marketcoin network
* When an MKC block is mined, the MKC in escrow is released to P1

Currently, P1 can technically renege on the trade before transacting to P2. However, the order P1 places on the Marketcoin network (this is one of many possible implementations) require a fee to be paid (in MKC) that is proportional to the change of value in the last 24 hours (as that is the escrow length). If the trade times out the pledge is given to P2, so P2 is guaranteed to either make the trade, or receive compensation better than the best case scenario considering the last 24 hours. That is a powerful incentive to trade. This requirement of pledges is not required in symmetric exchange. Proof of payment is another issue; it may be possible to automate this process with deep scanning of the foreign blockchain, but this could easily be too intensive a task, and requires marking transactions on the foreign chain. Manual proof of payment is sufficient at this stage, and with software automation, not a burden at all.



### Methods of Operation for Distributed Cross-Chain Exchanges

#### Asymmetric Exchange

As it stands, [Marketcoin](https://github.com/XertroV/MarketcoinWhitepaper) is asymmetric.

An asymmetric exchange has different rules on both sides. In the case of Marketcoin, it hosts the order book for both currencies, and Altcoin is unaware of it. This means asymmetric exchanges are backwards compatible (they can be made to 'read' a great many forms of blockchain), so a web between all currencies can be created with only asymmetric exchanges.

As mentioned before, the Marketcoin graph:


```
    TITLE: EXCHANGING BITCOIN FOR MARKETCOIN
           ASYMMETRIC EXCHANGE
    _______________________________________
    BITCOIN              +---------+
     P1---------+------X-+-P1>P2 • |
    ____________|______|___________|_______
    MARKETCOIN  #      |           @
     P2-----#---------•X.............•&>P1
    _______________________________________

```

    
Using Marketcoin to move between currencies other than Marketcoin is a little more of a burden as the process must be repeated:


```
    TITLE: EXCHANGING BITCOIN FOR LITECOIN THROUGH MARKETCOIN
           ASYMMETRIC EXCHANGE PASSTHROUGH
    ___________________________________________________________________________
    BITCOIN              +---------+
     P1---------+------X-+-P1>P2 • |
    ____________|______|___________|___________________________________________
    MARKETCOIN  #      |           @       +--------#--•X.............•&>P3
     P2-----#---------•X.............•&>P1-+  #         |           @
    __________________________________________|_________|___________|__________
    LITECOIN                                  |         | +---------+
     P3---------------------------------------+---------X-+-P3>P1 •
    ___________________________________________________________________________
```


An ideal asymmetric exchange built into two cryptocurrencies looks like:


```
    TITLE: EXCHANGING BITCOIN FOR LITECOIN ON AN IDEAL ASYMMETRIC EXCHANGE
    ______________________________
    XCOIN 
     P1-----------#--•X>P2
    __________________|___________
    YCOIN             |  
     P2--------#-•....X..•&>P1
    ______________________________
```


What is important is this is the only way this could happen. Bitcoin hosts the exchange and Litecoin 'reads' the exchange from the Bitcoin blockchain. This is about half-way to a symmetric exchange where both coins have both functionalities. We explore this graph in more detail later on.

##### Ignorant and Knowledgable Asymmetric Exchange

There is a clear difference between Marketcoin and an ideal asymmetric exchange. This is because in an ideal case, both chains have interchain awareness and can verify transactions on the other chain. In the case of Marketcoin and an existing cryptocurrency (say Bitcoin), the foreign coin is unable to read the local market (hosted entirely by Marketcoin). I call this ignorant asymmetric exchange, because Bitcoin is ignorant of the fact it is even occurring.

In the counter-case that a foreign chain *is* aware of the local chain, we can offload buy orders to the foreign chain, which can then enable some escrow like function to guarantee trades are atomic. I call this knowledgable asymmetric exchange. However, to guarantee determinism in such an exchange, buy orders will only be matched once they are learnt about by the other chain, and can only be canceled with the permission of the other chain (they will either be cancelled or a trade will occur before the cancelation takes place).

#### Combining Fiat Exchange with Factum Asymmetric Exchange
    
Consider a distributed Generic Fiat Exchange (GFiX). Often such an exchange will have a core cryptocurrency operating beneath the user-defined assets (think Ripples, BitShares, Freicoins, etc) and so should be compatible with a distributed cryptocurrency exchange. Then presume this chain also supports ignorant asymmetric exchange. In such a case it would be possible to buy arbitrary assets on the GFiX using Bitcoin in a trustless, multistep manner. In the best case where Xcoin supports asymmetric cross-chain trade in a similar way to Marketcoin and an asset market, you would experience the following process:


```
    TITLE: EXCHANGING BITCOIN FOR XCOIN-ASSET THROUGH XCOIN
    __________________________________________________
    BITCOIN              +---------+
     P1---------+------X-+-P1>P2 • |
    ____________|______|___________|__________________
    XCOIN       #      |           @
     P2-----#---------•X.............•&>P1---#-•X>P3    }
    ____________________________________________|_____  } Walled off Market
    XCOIN-ASSET                                 |       }
     P3----------------------------------#-•...•X&>P1   }
    __________________________________________________
    
    LEGEND
    -|+ : Path of Action, horizontal,vertical,corner
    .   : Path of Funds in Escrow
    >   : Transaction to
    #   : Order Placed
    •   : Block Produced (alt 8)
    X   : Exchange Matched
    @   : Proof of Payment
    &   : Escrow Unlock
```


#### Symmetric Exchange

A symmetric exchange is one where both networks run identical rule sets. Each hosts one half of two exchanges - a 'bid' and an 'ask' order book. Consider MKC and XC, two crypto coins. In the case of MKC, the 'ask' order book is for XC/MKC (the MKC chain is authoritative) and the bid order book is for MKC/XC (the XC chain is authoritative). Likewise, the XC chain hosts an 'ask' order book for MKC/XC (XC chain authoritative), and a 'bid' order book for XC/MKC (MKC chain authoritative).

Technically this is equivalent to two knowledgable asymmetric exchanges running on both chains.

##### A 'brief' explanation of one possible symmetric exchange 

Each market's deterministic execution is decided by the authoritative chain, based on best-effort updates shared between chains. 

*Side note:* If you imagine a cryptocoin hosting 10 markets, not every market needs to be updated every block, in addition, preventing updates increases liquidity at the cost of transaction time. For fledgling, unpopular markets this may well be a positive thing, and evidence in favour of only including market updates for the markets you care about - after all, you'll need to be running those clients. In addition, a very flexible update method such as this lends itself to better compatibility with block chains progressing at different rates.

These best effort updates relay specific information about both order books.

In the case of the 'ask' order book - the market the local coin has authority over - all known but excluded bid updates (from the foreign chain) are amalgamated into a chunk and deterministically matched against the 'ask' order book. The details of the trades made are recorded and packaged into a market update, which is then relayed back to the foreign blockchain in a best-effort fashion. Market updates are recorded in the merkel root (or a similar device) and secured in a chain so one can not be omitted. These are in turn recorded under the full block chain headers of the foreign chain. The deterministic matching happens over one market update. If a local block happens to contain three foreign market updates then all three are lumped and evaluated against the local order book deterministically. This leads to the fairest exchange between all parties concerned. The corresponding market update, when relayed back to the foreign blockchain, alerts the chain which cross-chain escrow transactions may be released and in what proportions (if there is a change address, for example).

In the case of the 'bid' order book - the market the local coin has no authority over - once orders are made the coins are locked and in escrow. All new or changed bid orders are added to the market update. After this update is recorded in the blockchain, in order to maintain foreign blockchain authority, if the user wishes to cancel the order they will have to wait for the foreign chain to recognise and acknowledge the request (one must broadcast a cancel message, record this in a market update, have the foreign coin register this in a market update, and then have the local blockchain recognise that it is finally safe to release the coins from escrow). During this time it is possible the order may be filled and the cancel message will fail.

##### Overview

Let us examine an ideal distributed exchange which operates exclusively on cryptocurrencies; and the path of value (for a Bitcoin/Litecoin trade) looks like:


```
    TITLE: EXCHANGING BITCOIN FOR LITECOIN ON AN IDEAL SYMMETRIC EXCHANGE
    ______________________________
    BITCOIN 
     P1-----------#--•X>P2
    __________________|___________
    LITECOIN          |  
     P2--------#-•....X..•&>P1
    ______________________________
    
    OR:
    ______________________________
    BITCOIN 
     P1--------#-•....X..•&>P2
    __________________|___________
    LITECOIN          |  
     P2-----------#--•X>P1
    ______________________________

```

    
That is to say, in the first case, an order is placed on the Litecoin network (ask for BTC or bid LTC) and recorded in a block. At some other point an order is placed on the Bitcoin network (bid BTC or ask LTC) which overlaps with the previous order on the other blockchain. When this second order is recorded in a block, it is known to have matched with the order on the Litecoin network (deterministically) and is automatically sent (or assigned) to the receiving party. At the next block on the Litecoin network the trade is learned of and the other transaction is performed so the Litecoins are transferred to the receiving party.

Moving form Xcoin to Zcoin through Ycoin - all of which support symmetric exchange:


```
    TITLE: EXCHANGING XCOIN FOR YCOIN FOR ZCOIN
           SYMMETRIC EXCHANGE PASSTHROUGH
    ________________________________________
    XCOIN 
     P1-----------#--•X>P2
    __________________|_____________________
    YCOIN             |  
     P2--------#-•....X..•&>P1-#-•X>P3
    ______________________________|_________
    ZCOIN                         |
     P3-----------------#---•.....X..•&>P1
    ________________________________________
```


By voting on which market updates to accept (from which other cryptocurrencies) and which markets to run, it will be possible to create a dynamic mesh of markets, forming many possible paths between any cryptocurrencies. (In the worst situation, a coin can run an asymmetric market and use that to trade into and out of foreign block chains.)

### Finding Efficiency

Every novel technology developed will be hindered by regulation in a unique way. The 'directness' of transferring fiat to crypto is a worry for a number of people (the same people as are behind the steering wheel of regulation). They feel they need to remain insulated from the untested Bitcoin. Perhaps they would feel more comfortable with a bridging technology, such as a cryptocoin pegged to a parent currency, that just so happens to natively interact with a distributed market.

Lets have a look at that, shall we?


```
    TITLE: AUD -> CRYPTO-AUD -> BITCOIN
    BANKING:
    __________________________________________
    AUD 
     P1==>BRK---+                      +==>P2
    ____________|______________________|______
                |                      |
    CRYPTO:     |                      |
    ____________|______________________|______
    CRYPTO-AUD  |                      |
                +-M>P1--#-•X>P2--D>BRK-+                  
    _______________________|__________________
    BITCOIN                |         
     P2------------#-•.....X...•&>P1                  
    __________________________________________
```

    
This, however, will likely not be the first iteration. It is elegant, quick, and efficient, but there are likely to be many sticking points before that can be realised. Firstly, Bitcoin doesn't support knowledgeable asymmetric exchange, and there is a strong possibility that too much regulatory pressure will require CRYPTO-AUD to ship without an exchange. Therefore the *first* iteration might look something a little more like:


```
    TITLE: AUD -> CRYPTO-AUD -> MARKETCOIN -> BITCOIN
    BANKING:
    ______________________________________________________________________
    AUD 
     P1==>BRK---+                          +==>P2
    ____________|__________________________|______________________________
                |                          |
    CRYPTO:     |                          |
    ____________|__________________________|______________________________
    CRYPTO-AUD  |                          |
                +-M>P1--+--X-+->P2-•-D>BRK-+                 
    ____________________|__|_|____________________________________________
    MARKETCOIN          #  | +---------@       +--#-•X.............•&>P3
     P2------------#------•X.............•&>P1-+ #   |  +-------@          
    _____________________________________________|___|__|_________________
    BITCOIN                                      |   |  |
     P3------------------------------------------+---X--+->P1 •
    ______________________________________________________________________
```

    
Not as pretty. Compared to a our current fiat exchanges, this doesn't look that appealing. That said, legally CRYPTO-AUD is far more comparable to a traditional payment processing system such as PayPal. By exploring the edge cases of regulation we can help find the inconsistencies and assist its evolution. An attack on Bitcoin by a Government will necessarily involve shutting down the flow of fiat into Bitcoin as much as possible. One strategy is to create useful technologies that are too similar to existing tech (PayPal, Visa) so we can stand on some very resilient legal precedents and standards if these systems are challenged. These middle ground crypto networks, then, cannot be made illegal without negatively effecting the current corporate monopoly because they are designed to resemble them so much. Whether that's possible is another matter.

## Conclusions

We know that regulatory pressure can be applied to restrict a flow of Dollars/Yen/Euros anywhere. While this investigation into distributed exchange didn't identify how to expunge regulatory pressure, it did yield at least one other method of allowing value to move from Fiat to Bitcoin: distributed cross-chain markets for cryptocurrency. By building a PayPal-like network built on Bitcoin and minted/destroyed in the same fashion as PayPal (deposit -> mint, withdraw -> destroy). Ultimately some legal entity must be responsible for the cash-in/out process, but this can now safely be entertained without needing to worry about the regulation surrounding running an exchange - provided there is a cross-chain market out there already.

In addition to this, we've looked at the minimum ideal for a market and found that it is readily achievable with knowledgable asymmetric exchange (better yet, symmetric exchange). We've briefly looked at one way this can be achieved, providing a fast, resilient, cross-chain market that operates as a close to perfect market. We have not investigated this suggestion deeply, though (don't worry, that's coming soon). By extrapolating this across all coins (or even just a few) we can see an interconnected web of markets bridging the gaps between chains.

## Where To?

For cryptocurrency to succeed a distributed exchange must be developed linking them together. By leveraging interchain awareness we can build factum exchanges that operate in the domain of the currency itself. Atomic exchange that is intwined in cryptocurrency is a strong motivator for adoption, and by creating a web of markets the canonical boundaries between \*coins will be removed.

Efficient atomic cross chain trade is a necessity for the long term viability of cryptocurrency. Using an asymmetric exchange, any user of a \*coin can move value into an alternate chain, letting them take advantage of any new innovative features produced on other chains.
