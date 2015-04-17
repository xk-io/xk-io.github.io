---
title: Handeling Death in the NVB
author: Max Kaye
date: 2015-03-27
layout: post
summary: Without correlating deaths of voters to the expiration of their identity it is difficult to maintain anonymity in a decentralized voting system. A system of expiry (and revalidation) is suggested that is compatible with CoinJoin to allow the best of both worlds.
---

# Handling Death and the NVB

It occured to me that there is an unsolved problem with the NVB: death.

When a voter dies, if there is no connection between their physical death and their cryptographic identity; it continues to live on. This brings up a new-ish toxic market: dead people's ID. In short, since they don't expire they essentially become a 'vote for hire' if they can be recovered. Artificially inflating the voting pool in this way would almost certainly be to the long term detriment of the quality of governance we are obliged to accept (or is it? I presume yes for the moment).

So, one way to address this is for votes to 'time out'. Let's take a situation like the following: 

Voters are empowered once every three months, and many at once. The empowerment of their ID only lasts 1 year at a time (or w/e). During that 1 year they are free to transfer away the right to vote to other identities. Particularly, they can do so through (synchronised?) CoinJoin operations. In this way, provided they only partake with members of their own pool, they can maintain relative anonymity while still linking their identity to only one large batch of people so an expiry date is maintained. The transaction they create will maintain constant voting rights and contstant expiry date. Mismatching expiry dates cause the whole transaction to be flagged as invalid. 

That sort of situation would largely solve the problem. People who die are known and thus can't validate, so their token expires.

Aditionally you can choose your pool by timing when you register, or abstaning (by letting your token expire for a 3 month period or w/e, then revalidating for another block).

I guess people can also elect to be empowered instantly but this isn't the default and will lead to less privicy. Political active people are good candidates for going straight away, but those valuing secret ballet are encouraged to wait.





