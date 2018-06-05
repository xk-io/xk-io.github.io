---
title: A secure guessing game
author: Max Kaye
date: 2018-06-05
postlet: true
---

Here's a guessing game that I believe is secure.

## Setup

You want people to guess the answer to some question. The answer is in ASCII, and all lowercase.

Additionally, you want automatic (though not instant) payout for correct answers. Fully trustless, though.

That question could be anything with a certain answer. Example: "Who wrote Macbeth? (canonical full name)".

To do it, this is what's required of the winning guesser. _(this example is written in the context of a trustless host network like Ethereum)_.

## Winning Players Actions:

### Step 1

Come up with the answer. Got it? Great.

### Step 2

Publish to the contract:

`commit(bytes32 commitHash)`

Where `commitHash = keccak256(string answer, address yourAddress, bytes32 powOnAnswer)`

(Keep these details private for the moment)

#### Aside

Why should we commit _this_ collection of things, and why do we have `powOnAnswer`?
Does `pow` mean proof of work?

### Step 3

After some time (set by the contract), publish this transaction:

`reveal(string answer)`

Wait some more time (set by the contract) and publish:

`claim()`

Done!

## How and why you're safe

The most significant feature in this whole enterprise is automatic payouts.
There are significant design constraints when we want _automatic payouts_ to coexist
with a _completely public and trustless_ information.

The relationships we need are straight forward, though.

You need to be able to publicly reveal an answer with a near-certain guarentee that
a correct answer can't be stolen from you.

That means that everyone has to _know_ you have _a specific_ answer (and agree on that) before
you reveal it.

Collecting your winnings reveals the answer. But you also had to _commit_ to your answer
some time before-hand. That means (with a well written contract) the only people you have
to worry about swooping in and taking your winnings are those people who _had already made
commitment_ prior to yours. (And logically the winnings should be theirs, anyway)

There are two important time delays to make this happen:

1. Allow enough time for commitment to occur without risk of interception
2. Allow a significant enough time after the first answer is revealed to allow other
contestants to reveal their answers (say, 24 hrs).

If the minimum time for (1) is, say, an hour, then it's incredibly difficult for an individual
to censor a single transaction, which means many confirmations are near-certain.

Additionally, including your address in the outside hash renders replay attacks ineffective.

After such time you're free to publish your answer.

However, you don't publish _just_ the answer and your address.
You publish _additional information_. This is the `powOnAnswer` parameter above.

The exact means of calcualting it aren't important, for reasons that we'll see.
Let's presume you're doing something like a password hashing algorithm (e.g. PBKDF2).
Your task is to recursively apply a hashing function 500 million times.
(if you think this is a bit weak, you'll see shortly the parameters are freely adjustable.)

Why on earth would you recursively apply a hash like that? You could _never_ possibly prove
something like the correctness of such a hash on Etherem!

Well, let's think about how you'd _attack_ such a scheme.

First off, the contract needs to store something to check if an answer is correct or not.
The usual way is to publish a hash, or something similar. But whatever is publish needs to be
verifiable (and cheaply). If you publish just `keccak256(answer)` then you're liable to be
brute forced (especially if the answer is something like a name). So that won't work.

What if you could publish something _derivied_ from the answer that was work-intensive,
but quickly verifiable?

Not only is that the core idea _behind_ proof of work (hard to generate, easy to verify), but
we can also use it in a totally different way: to introduce entropy.

The reason brute forcing a name is easy is that there just aren't that many combinations.

We can make it much harder to brute force by salting the answer with a time-intenstive
hash of the answer. It's not that we care about verifying that proof, it's that generating
it is energy intensive and requires knowledge of the answer in advance to be efficient.

So if you're guessing wildly, then you will have to hash each guess (in this case) 500
million times before you can compare it to the answer! (And, of course, there's no way to
guess the many-times-hashed guess in advance, since it's 32 bytes and psuedorandom.)

When you add all this together, I think you end up with a guessing game secure enough to
resist any attack that isn't attacking the blockchain itself (e.g. censoring transactions).

(Note: to be properly secure we want to include a nonce (which is public) in at least the
first hash in our recursive chain. This is to make sure that the work (hashing) being done
is unique enough that it likely hasn't been done before.)

### Algorithm drafts

``` purescript
-- psudocode haskell
findAnswer :: TargetHash -> Nonce -> String
findAnswer target = allPossibleAnswers
                  |> dropWhile (failsProofOfWorkCritera target)
                  |> head
                  |> extractAnswer

generatePublicHash :: Answer -> Nonce -> TargetHash
generatePublicHash answer = performProofOfWorkCriteria target answer
```

What `findAnswer` says is:

First: find a function that will tell you if some input fails the proof of work criteria.
(`failsProofOfWorkCritera target`) - let's call that `F`.

Then, do the following in order:

One at a time, take a possible answer. Then, check if `F` returns true or false.

    allPossibleAnswers |> dropWhile (failsProofOfWorkCritera target)

_(Note: you don't have to generate all the possible answers ahead of time, you can
make a new one up each time you need one)_

If it returns false, discard the possible answer and move on to the next.
If it returns true, then take all remaining possible answer (with the most recent guess
in the first position) and take the first one (i.e. the answer).

Finally, run the answer through whatever function you need to give you the right
data to commit to smart contract above. (Which would need to know about your
address in this case.)
