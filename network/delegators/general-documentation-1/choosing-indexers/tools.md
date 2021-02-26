# Tools

Tools to evaluate Indexers and to compare their performance with each other.

### Graphlets.io

[Graphlets.io](http://graphlets.io/) gives Delegators an overview at the Indexers with the highest historic ROI. By sorting indexers according to their past returns, Delegators can quickly gain a feeling about how profitable delegating to a particular Indexer could be.

#### Historic ROI

Let’s assume Delegators did their due diligence on the `networks page` of the Graph protocol and think that the following indexer could be interesting:

> **legiojuve.eth**  
> 0xcb22a8ce581d04fef99b81ec5a60725070a3e8c4

![](../../../../.gitbook/assets/image%20%282%29.png)

By coping this indexers ETH address and pasting it into graphlets.io, you can quickly see, that this particular indexer hasn’t made a profit for it’s delegators despite running for 18 days. It’s historic ROI is 0.00%.

![](../../../../.gitbook/assets/image%20%286%29.png)

That is curious because more than 1.5 million GRT have been delegated to this indexer despite a fee and rewards cuts percentage of 100%. This means that all Delegators that have delegated with this Indexer are not earning any returns on their delegation at the time of writing this documentation. It could be, that this Indexer has lured delegators in by offering a low rewards cut percentage and changed it or that this Indexer simply does not want to attract delegators. Whatever may be the case, it’s important to stay away from Indexers like this.

#### Delegation Ratio

As was already mentioned earlier on, it is also important to evaluate whether or not an Indexer is overdelegated.  the next column on the graphlets.io website called `Indexers`. Here you can find a variety of other statistics about all the available indexers. One particularly helpful statistic is the `delegation ratio`. The higher the ratio, the more likely that an Indexer is running risk of becoming overdelegated or is already overdelegated. A value of 16 and higher means that the Indexer is overdelegated.

Let’s assume a Delegator went back to the networks page of Graph protocol and came to the conclusion that the following Indexer could be interesting because of the low fee/reward cut of 15.25%:

> 0xc94a2669f719f792f166800fb6ef00fb3a7f5bec

![](../../../../.gitbook/assets/image%20%284%29.png)

By referencing the graphlets.io website, Delegators can have a close look at the delegation ratio of this Indexer. One may have already noticed that the owned/delegated ratio of 2.0M GRT to 33.9M GRT was a little odd and the Graphlets website just confirmed the suspicion! This indexer has a delegation ratio of **17.14**, the highest on the entire network at the time of writing. If Delegators choose to delegate to this Indexer, the staking rewards will be diluted because there are already many other Delegators that have chosen this Indexer.

### Oracleminer.com <a id="814e"></a>

[Oracleminer.com](https://oracleminer.com/graph/indexer/0x7ab4cf25330ed7277ac7ab59380b68eea68abb0e) allows Delegators to gain useful insights on the Indexer of their choice. Simply insert the ETH address of the Indexer of your choice. For example, let’s have a look at Staking Facilities that is presently ranked on the third-place on the network page of the Graph protocol. When visiting Oracleminer, Delegators will see the following stats:

![](../../../../.gitbook/assets/image%20%283%29.png)

This website is useful for learning more about how much of the available stake is presently allocated by the indexer. In the example above, more than 100% of the available stake is allocated. This is positive as it means that this indexer is using the entirety of the available stake to earn rewards.

Delegators should avoid Indexers that are not allocating their available stake like this Indexer:

![](../../../../.gitbook/assets/image%20%287%29.png)

### Stake-machine.com

[Thegraph.stake-machine.com](https://thegraph.stake-machine.com/d/-3BUUtbMz/thegraph-overview?orgId=1&refresh=5m) offers great analytics on the network but also on Indexers and Delegators.

#### Historical changes of reward and fee cuts

A helpful feature of the website is that it allows Delegators to see if an Indexer has made changes to the reward and fee cut percentages.

![](../../../../.gitbook/assets/2.jpg)

It can also be used to see how often an Indexer closes allocations.

![](../../../../.gitbook/assets/3%20%281%29.jpg)

### Graphscan.io

[Graphscan.io](https://graphscan.io/) is another website for detailed statistics about Indexers, Curators and Delegators.

![](../../../../.gitbook/assets/4.jpg)

It can also be used to calculate estimated delegation rewards based on the amount of GRT you wish to delegate.

![](../../../../.gitbook/assets/5.jpg)



### Reward Calculators

#### Indexer comparison and [reward calculator](https://docs.google.com/spreadsheets/d/1Zg39W_TJANNiYY-HrgAlrgolrTt7aFvVF1swzngjH5o/edit#gid=893976495) by Protofire.io

{% embed url="https://docs.google.com/spreadsheets/d/1Zg39W\_TJANNiYY-HrgAlrgolrTt7aFvVF1swzngjH5o/edit\#gid=893976495" %}

#### Simplified reward calculator by me \(Space Traveler\)

The available calculators were lacking the functionality of comparing ndexers with each other. This is why [this simplified calculator](https://docs.google.com/spreadsheets/d/1NYSCxmJFgrX4YINyg5c-jBWBa4UR5aTTi5xhhjTIEuk/edit#gid=1291056551) was created.

All you need to do is insert the amount of GRT you want to delegate, the spreadsheet does the rest:

![](../../../../.gitbook/assets/image.png)

By switching to the reward calculator tab, You can now see an in-depth comparison of all the available indexers. The spreadsheet shows you if an indexer is overdelegated and how many days it will take you to break even \(because of the delegation tax of 0.5%\).

![](../../../../.gitbook/assets/image%20%2811%29%20%281%29.png)

#### Reward Calculator by SunTzu

{% embed url="http://reward.suntzu.me/" %}

### Other tools and resources

{% embed url="https://dappquery.com/dapp/graph-mainnet-delegator-10053" %}

{% embed url="https://thegraph.live/" %}

{% embed url="https://thegraph.live/" %}

