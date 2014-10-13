---
title: Microchains
author: Max Kaye
date: 2014-08-27
layout: post
summary: Microchains are developing proposal for generic merged mining.
---


The [Ethereum devs](https://www.youtube.com/watch?feature=player_detailpage&v=o6D8Up411dI#t=1756) have been mentioning microchains lately so I figured it was time to write up what my thoughts on this sort of thing have condensed into; they might differ from Gav Wood's thoughts.

As a note, I didn't coin the term microchain, though I've heard Gavin Wood use it (and Stephan Tual). I didn't have a term and I think this is perfect.

The point of a microchain is to provide a shared scalable PoW 'container' - a chain meant for nothing else but wrapping data in a PoW. Typically this has been done in a roundabout way (see AuxPoW or Mastercoin/Counterparty) that requires a lot of data, and is not efficient for any 'piggy-backing' chains hanging off the main chain. This isn't a huge issue; insofar as - in the case of AuxPoW - proofs just go from 80 bytes to ~500 bytes (unless you're using P2Pool or Eligius then it's a bunch more). This is because the whole chain from block hash to PoW must be included, which is `Hash(Header(MerkleTree(Coinbase(ScriptSig(BlockHash)))))`. Ugh!

Additionally AuxPoW has a number of design flaws: using 'chain-ids' to dictate positions in merkle trees is just ugly. The point is to ensure uniqueness in the proof - that you can't secretly include *two* different block hashes (since data in a merkle tree can be hidden) and later launch a doublespend attack. It's trivial to see that a merkle patricia tree (MPT) is the better solution here as key-uniqueness is guaranteed.

Another flaw is the indirect and bulky nature of the proofs as described above.

A further flaw is the reliance on a central chain: Namecoin will never exist without Bitcoin (or at least requires a hardfork) and necessitates the use of the Bitcoin chain. It would be nice to have a system of merged mining that is coin-agnostic (doesn't favour Bitcoin, basically). Hardforks are bad, lets avoid them.

A related flaw is the dictation of data structure which favours bitcoin-forks. It introduces needless complexity for a ground-up chain to implement AuxPoW.

All in all, using AuxPoW has a lot of side effects, and it'd be nice to be able to avoid them.

## Basic microchains

These are minimum structures to fairly support merged mining and general data-inclusion.

(The code is written to be roughly compatible with [Encodium](http://github.com/eudemonia-research/encodium).

### Intra-chain view

{% highlight python %}
class Block:
  branch       = MerklePatriciaBranch.Definition()
  header       = BlockHeader.Definition()
  transactions = Transactions.Definition()
 
  def valid_proof(self):
    root = branch.calculate_root(genesis_hash, header_hash)
    return root < header.target
{% endhighlight %}
    
### Inter-chain view

{% highlight python %}
class MicrochainBlock:
  tree = 
    MerklePatriciaTree.Definition(
      List.Definition(
        KeyValuePair.Definition(
          GenesisHash.Definition(), Hash.Definition()
          )
        )
      )
      
  def proof_of_work(self):
    return self.tree.root
{% endhighlight %}

## Optimisations

* Ensure genesis keys diverge as quickly as possible; Put a cap on proof length to avoid bloat for fun - putting two very similar keys can create a worst-case proof.

* Change MicrochainBlock's proof of work to: `def pow(self): return hash(self.tree.root + nonce)` - this means we have O(1) updates to PoW whereas without this a k,v pair in the MPT must be altered, which is an O(log n) complexity update.

## More complex forms

There are a few more alterations I've been thinking of, especially:

* Making microchains into a blockchain of their own (and the metadata is included in the tree like everything else - this metadata governs targets, difficulty, etc) which will aggregate mining power in a more formal manner. Additonally it means that a chain can just not worry about PoW, and simply take an authenticated list of hashes from the parent chain (for better or worse). And...

* Deregulating block frequency on merged chains and allowing the microchain to govern update frequency. Which ties into...

* Competition within the tree. By this I mean merged mining an additional chain incurs some cost, this drastically alters the incentive structures around attacking networks and merged mining (haven't done the math yet to figure out if it even *can* be benefcial).

Those three points mean the microchain could support many merged chains, and their block frequencies would be governed by how often they are mined in the microchain (and lower frequency means higher reward per block), and with added competition that means they will reach an equilibrium which allows a direct measurement of percieved economic value. More detail another day.
