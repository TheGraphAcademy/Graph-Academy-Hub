# Vulnerabilities

### **Sandwich Attack**

_As described by_ [_Jim / Cryptovestor_](https://forum.thegraph.com/t/this-month-in-graph-indexing-january-edition/1041)_:_ By monitoring changes in Indexer cuts using [Stakemachine's dashboard](https://thegraph.stake-machine.com/?orgId=1&refresh=5m) a delegator, with the assistance of Indexer\_payne, picked up on a potential **Sandwich Attack**, first described and named by Indexer Nuviba. A genuine Sandwich Attack is a malicious attempt by an Indexer to pretend they will share the majority of rewards with their Delegators, but then take all the rewards for themselves and hide the fact that they did so. 

{% hint style="info" %}
This variant of a **Sandwich Attack** was explained by nuviba.eth \| 0x62a0—fc8c4a
{% endhint %}

So what does this look like in the real world?

1. Indexer has a low reward cut e.g. 20% \(Indexer takes ~20% of rewards, Delegators get ~80% of rewards\) which attracts new delegations
2. At some point the Indexer changes the rewards cut to 100% 
3. Minutes later the Indexer settles on-chain and takes all pending rewards for themselves, Delegators get nothing 
4. Indexer quickly sets reward cut back to 20% to look appealing to new Delegators 
5. Delegators are either totally unaware they are being deceived, or are left wondering where their projected yield has gone 

In a truly malicious Sandwich Attack, the above actions are performed in a short period of time in an attempt to hide the malicious activity from Delegators, and 100% of the rewards are taken. In the case that was seen on mainnet, the Indexer moved their cut from 20% to 80%, settled, then set their cut back to 20%. In explaining why, when confronted by their Delegators, the Indexer explained that they use this strategy in order to provide a fixed return to their Delegators. Does this seem like honest Indexing? The answer is up to you.

