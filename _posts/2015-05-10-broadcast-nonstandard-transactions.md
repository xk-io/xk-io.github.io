---
title: Broadcast Nonstandard Txs Quickly [Bitcoin]
author: Max Kaye
date: 2015-05-10
layout: post
summary: How to edit the Bitcoin Core source code to allow sending nonstandard transactions quickly.
---

NB: This document is [better read from github](https://github.com/xk-io/xk-io.github.io/blob/master/_posts/2015-05-10-broadcast-nonstandard-transactions.md), due to fomatting issues with the code.

So, I recently wanted to [broadcast a nonstandard tx](https://blockchain.info/tx/c058286d078f059eab4231475ad6fc23c4cd1520d603128b900c13582728a961?show_adv=true) and didn't want to wait for full blockchain sync on my dev machine.

I knew that Eligius supports the [Free Tx Relay Policy](https://en.bitcoin.it/wiki/Free_transaction_relay_policy), and that I'd sent them nonstandard txs before, but all the IPs I could find weren't accepting connections. Finally I found `68.168.105.168` and was able to connect and broadcast the message. Later I realised you can [search getaddr.bitnodes.io for 'eligius' to find nodes](https://getaddr.bitnodes.io/nodes/leaderboard/?q=eligius).

This is a great start, but we still need to send the transaction. By default Bitcoin Core does not relay transactions that:

* Are nonstandard
* Contain outputs not in the **current** UTXO set

At this point we are going to need to compile a version of Bitcoin Core. We will need to address the above two problems to broadcast a transaction. The second problem is included so we don't have to download the whole blockchain, allowing us to relay pretty much anything.

The first section of code to change is `IsStandard()` in `script\standard.cpp`. [Source Link](https://github.com/bitcoin/bitcoin/blob/23254131a3fdaeae9c50dafca6d0addbbf235820/src/script/standard.cpp#L183). The quickest way to fix this is add a `return true;` at the top of the function like so:

```
bool IsStandard(const CScript& scriptPubKey, txnouttype& whichType)
{
    return true;
    vector<valtype> vSolutions;
    if (!Solver(scriptPubKey, whichType, vSolutions))
    <snip>
```

Sweet, now all transactions are standard for our node. The next part is to relay transactions even when we can't validate the outputs they spend. When troubleshooting before I ran into [this error message](https://github.com/bitcoin/bitcoin/blob/23254131a3fdaeae9c50dafca6d0addbbf235820/src/rpcrawtransaction.cpp#L796) being thrown. To avoid more debugging I figured the best thing to do was just rip the whole block of code out. That is to say this:

```
<snip>
    bool fHaveChain = existingCoins && existingCoins->nHeight < 1000000000;
    if (!fHaveMempool && !fHaveChain) {
        // push to local node and sync with wallets
        CValidationState state;
        bool fMissingInputs;
        if (!AcceptToMemoryPool(mempool, state, tx, false, &fMissingInputs, !fOverrideFees)) {
            if (state.IsInvalid()) {
                throw JSONRPCError(RPC_TRANSACTION_REJECTED, strprintf("%i: %s", state.GetRejectCode(), state.GetRejectReason()));
            } else {
                if (fMissingInputs) {
                    throw JSONRPCError(RPC_TRANSACTION_ERROR, "Missing inputs");
                }
                throw JSONRPCError(RPC_TRANSACTION_ERROR, state.GetRejectReason());
            }
        }
    } else if (fHaveChain) {
        throw JSONRPCError(RPC_TRANSACTION_ALREADY_IN_CHAIN, "transaction already in block chain");
    }
    RelayTransaction(tx);
<snip>
```

Becomes this:

```
<snip>
    bool fHaveChain = existingCoins && existingCoins->nHeight < 1000000000;
    RelayTransaction(tx);
<snip>
```

So, all that's left to do is compile bitcoind, run it with `-connect=68.168.105.168`, wait for the connection to initialize (which can be checked with `bitcoin-cli getpeerinfo`) and then `sendrawtransaction` when you've confirmed the connection. If all goes well the tx will appear in the next eligius block! 
