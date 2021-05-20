# Network Page

In order to delegate, Delegators will first have to choose an Indexer from the [network page of the Graph protocol](https://network.thegraph.com/). Let’s have a look at what you can learn from the `network page`.

First of all, the network page shows you the most important stats about the network. Such as the total token supply, the amount of GRT that is presently staked and the amount of indexing rewards that have been earned so far.

## Metrics

The metrics on the network page help Delegators to gain a quick overview of Indexers.

![Network Page of The Graph](../../../../.gitbook/assets/image%20%288%29.png)

### Fee and Reward cut Percentages

`Fee and reward cuts` refer to the percentages Indexers deduct from the indexing and querying rewards that are distributed to their Delegators.

![](../../../../.gitbook/assets/image%20%289%29.png)

An indexer with a fee cut of 20% keeps a total of 20% of earned rewards for themselves.

{% hint style="info" %}
**Example:** If the delegated stake earns a total of 100 GRT within a week of staking, an Indexer with a 20% cut will keep a total of 20 GRT for themselves.
{% endhint %}

The percentages Indexers vary to a great degree but taken alone, they are not enough to select an indexer.

{% hint style="danger" %}
As a general rule, indexers with a fee cut of 100% are not interested in taking delegations from Delegators. Consequently, these should be avoided.
{% endhint %}

### Cooldown Remaining

Indexers have a `cooldown period` that determines how often they can change delegation parameters. Indexers are free to decide the cooldown period but are subject to reprimands by the free market. All other things being equal, Indexers who set longer cooldowns should receive more delegation from Delegators because of the reduced risk of sudden changes to the the fee and reward cut percentages.

### Stake Owned and Delegated

Within the `stake owned` _\*\*_column Delegators can see how many GRT are deposited by the Indexer as collateral to prevent malicious behavior.

![](../../../../.gitbook/assets/image%20%285%29.png)

Should an indexer behave in a harmful way, a percentage of his owned stake will be deducted as punishment. This is called `slashing`. You can learn more about it here:

{% page-ref page="../../../indexers/" %}

The higher the collateral, the more is at risk for the indexer.

In the next column, `stake delegated` , Delegators can see the amount of GRT that is delegated to one particular Indexer. In the image above, Delegators can see that 238 million GRT are delegated to the very first Indexer in the list. This means that community members think that this is a highly trustworthy and profitable indexer and have subsequently delegated a large amount of GRT with this indexer.

{% hint style="warning" %}
We will see in the following why this conclusion could be superficial.
{% endhint %}

### Delegation Capacity

The section `Available` within the category `Delegation Capacity` indicates the amount of Graph Tokens Indexers can productively accept before having to deposit more of their own stake. This is an indicator to Delegators how many GRT can be delegated until the Indexer can no longer productively accept delegations.

`Max Capacity` indicates the maximum amount of delegated stake the indexer can productively accept. An excess of delegated stake cannot be used for allocations or rewards allocations.

What is important to analyze is whether or not an Indexer is `overdelegated`. If `Delegation Capacity` of an Indexer is negative \(indicated by the small glowing square\), the Indexer is overdelegated.

![](../../../../.gitbook/assets/1%20%281%29.jpg)

This implies that the amount of GRT delegated to the Indexer is higher than the available delegation capacity the Indexer can still productively accept.

{% hint style="danger" %}
If an Indexer is overdelegated, staking rewards are diluted.
{% endhint %}

This means that it could be more profitable to delegate to an Indexer that is not yet overdelegated but has similar stats.

### Query Fees and Indexer Rewards

Fourth and last, Delegators can find two columns with stats about the generated revenue of an Indexer.

![](../../../../.gitbook/assets/image%20%281%29.png)

The `query fees` and the `indexer rewards` show how many GRT an Indexer has earned so far. These two columns are important if Delegators want to evaluate the activity level of one particular Indexer. When doing so, it is important to keep in mind that there may be indexers with attractive rewards cut percentages that are not active for a variety of reasons. Having a look at the earned rewards of the Indexer in these two columns can help to assess if an Indexer has been active.

