---
layout: post
title:  Efficient Reorgs on Cryptonets
author: Max Kaye
date:   2014-04-02
categories: state reorg cryptonet marketcoin
summary: Thoughts on how to reorganize a blockchain under certain non-bitcoin conditions.
---

Every [PoW](https://xk.io/glos/pow) driven cryptonet has a state. The state of Bitcoin (and forks) is the particular
set of Unspent Transaction Outputs (UTXOs) at the time - essentially the set of all Bitcoin
able to be spent.

When a new block arrives, the usual process to update the state is simple:

{% highlight text %}
Start with S[n,0] (state at block n)
Apply the first transaction from the new block (B[0]) to S

S[n,k] + B[k] -> S[n,k+1] for all k in B

S[n+1,0] = S[n,max(k)+1]
{% endhighlight %}

However, what happens when a new block arrives causing a [reorganisation](https://xk.io/glos/reorg) of the main chain?

{% highlight text %}
.       3a← 4a    <-- 3a and 4a are not in the main chain currently
      ↙
1 ← 2 ← 3 ← 4     <-- 3 and 4 are in the main chain

> 5a arrives, causing the reorg:

1 ← 2 ← 3a← 4a← 5a   <-- New main chain
      ↖
        3 ← 4        <-- Old main chain, 3 and 4 no longer in the main chain

In this case block #2 was the lowest common ancestor (a pivot point)
of the two competing chains 3a->5a and 3->4.
{% endhighlight %}

## The problem of reorgs

Let's presume the distance from the [lowest common ancestor](https://xk.io/glos/lca) (LCA) and the new head is `n`.

Bitcoin et al solve the issue by stepping backwards through time.

Since Bitcoin transactions spend outputs, and outputs may be spent only once, playing the
blockchain backwards is trivial:

{% highlight text %}
for each transaction:
	remove it's outputs from the list of UTXOs.
	add the outputs it spends to the list of UTXOs.
{% endhighlight %}

And bam! You can then play time forward from the LCA to calculate the new state. How nice.

What happens, though, when we move to a cryptonet that only operates on balances and doesn't
use the input/output system of Bitcoin?

Well, provided we're recording every transaction it's quite simple. A transaction moving
`X` coins from `A` to `B` results in `A-=X` and `B+=X`. That is trivial to reverse. However, the
caveat is that we must record every transaction. Once we start including complex mechanisms
within the protocol that produce transactions that are not recorded but simply implied, we
can no longer play time 'backwards' as `S[m]` depends on `S[m-1]` and without knowing `S[m-1]` to
calculate the implied transactions, we can't play time backwards. Of course, if we know `S[m-1]`
we don't need to do any of this anyway, so we're sort of stuck.
Examples of this sort of mechanism can be found in the way contracts create
transactions in Ethereum and the market evaluation in Marketcoin.

Remembering `S[m-1]` is easy but what if the reorg is of length 2, or 3, or 10? We can't just
remember *all* the states.

So, we can see that we have a problem.

## Efficiently remembering states

The intuitive solution (to me, at least) is to know *some* but not all states at strategic
intervals between the genesis block and the current head. When a reorg of length `n`
occurs, the network has already committed to evaluating `n` new states. I define 'efficient'
here to mean evaluating no more than `2n` new states (in the worst case). Unfortunately,
this means we'll need to remember about `2*log(2,h)` states, where `h` is the height of the
chain head. All the UTXOs in Bitcoin take up a few hundred meg of RAM, so for 500,000 blocks
we're looking at no more than 40 states, but that's still ~10 GB of space (by Bitcoin's
standards) which isn't ideal. It's unlikely that we'll see long reorganisations, but we'd still
be storing half of the figures mentioned above, which, while better, isn't perfect.

One solution may be to record the net implied change of state as the last transaction,
but that solution might be more painful than the cure, and requires introducing extra
complexity into the network architecture, which I'm against, so we won't consider
this option here.

In addition to the above constraint on 'efficient', we also require that for each block
building on the main chain we should only have to calculate one new state (the updated
current state). This implies that when we step through the blockchain, we only ever
forget cached states, with the exception of the new state produced by the next block.

Somewhat-formally:

{% highlight text %}
Current head is of height n.

A[n] = {cached states at height n}

Block n+1 arrives:

assert A[n] is a superset of {all a in A[n+1] s.t. a is not of height n+1}
{% endhighlight %}

Thus `A[n+1]` can be described as the set of some or all of the states in `A[n]` and
the state at `n+1`, and therefore our collection of states does
not requrie regeneration on each new block.

I propose a solution below that has a number of desired properties:

* A reorg of length `n` requires computing no more than `2n` states
* Space efficient: `k` states saved where `ld(h) <= k <= 2*ld(h)`
* Incremental: only one new state has to be calculated for each new block


{% highlight text %}
Initial conditions:
- Reorg length: n
- Current height: h >= 3
- i = 0; i < h

2^k < h - i <= 2^(k+1) is always the case for some k
if h-i == 2: set k to 1. (it would otherwise be 0)

After finding k, and while h-i > 1:
1. Cache states at height i + 2^k and i + 2^(k-1).
2. i += 2^(k-1)
{% endhighlight %}

and in python: (testing all combinations up to 2^13)

{% highlight python %}
import math

h = 3
states = set([1,2])

while h <= 2**13:
	newStates = set()
	# find largest k s.t. 2^k < h
	i = 0
	while h-i >= 2:
		k = math.log(h-i)//math.log(2)
		newStates.add(int(2**k)+i)
		newStates.add(int(2**(k-1))+i)
		i += int(2**(k-1))
	ts1 = set(states) # temp set for testing superset requirement
	ts1.add(h) # add the current state (instead of removing it from newStates)
	assert ts1 >= newStates # ts1 is a superset of newStates
	l = list(newStates) # temp list just to print
	l.sort()
	print(h, math.log(h)//math.log(2)+1, len(l), l)
	states = newStates
	h += 1
{% endhighlight %}

Because of the ~log(n) space requirement a very fast block time is not a major concern.
A chain with a target time of 1 minute requires about 1.5x the storage capacity of an
equivelant chain with a target time of 10 minutes in the first year, and this ratio
rapidly approaches 1 in the following years.

That said, after the first year with a 1 minute block time, we'd be storing around 30 states.
If we ignored all states more than 2000 blocks deep (a day and a bit) we're still storing more
than 15, which isn't a particularly great optimisation. (When we have events like the
[Fork of March 2013](https://bitcoin.org/en/alert/2013-03-11-chain-fork) we would like clients
to adjust quickly and efficiently).

I have some ideas about state-deltas to try and solve this issue (which is
ungood, but not doubleplusungood) but that can wait for a future post.
