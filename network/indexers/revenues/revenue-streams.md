---
description: What are the incentives for Indexers to participate in the network?
---

# Revenue Streams

In order to ensure the decentralization of The Graph Network, different incentives are given to [network participants](../../overview.md). These are the incentives for **Indexers**:

{% tabs %}
{% tab title="Indexing rewards" %}
### Indexing rewards

[Curators](../../curators.md) stake GRT in order to signal to Indexers which subgraphs are of a high-quality and should accordingly be indexed in the network. Based on the curation signal, Indexers select subgraphs and index their contents. The indexing rewards for doing so are generated via a **3% annual protocol wide inflation**. The rewards are distributed to all Indexers who are providing subgraphs developments for the network proportional to the amount of their indexing work.
{% endtab %}

{% tab title="Query fee rebates" %}
### Query fee rebates

Consumers of The Graph Network \(typically end-users and applications\) are able to query indexed data in The Graph Network. To do so, consumers have to pay query fees for their metered usage to the Indexer they are querying data from. Indexers can freely set their pricing models for query fees and can utilize different strategies to attract customers.

At the same time, consumers are able to set their own preferences for query fee pricing and can decide on the parameters for which Indexers process queries.

{% hint style="info" %}
Based on the mechanisms of the free market, query fees will be decided by supply and demand.
{% endhint %}
{% endtab %}

{% tab title="Rebate Pool" %}
### Rebate Pool

Following the [Cobb-Douglas Production Function](https://en.wikipedia.org/wiki/Cobb%E2%80%93Douglas_production_function), a Rebate Pool is created that rewards all network participants \(_like Indexers_\) based on their contributions to The Graph Network. The intention behind the Rebate Pool is to encourage Indexers to stake GRT in rough proportion to the amount of query fees they earn for the network. The Rebate Pool receives a fixed portion of query fees that are contributed to it.

{% hint style="success" %}
The Cobbs-Douglas Production Function calculates contributions to the reward pool and allocates the resulting stake on subgraphs where the query fees were generated. When indexers allocate stake \(in proportion to their fee contribution to the pool\) they receive 100% of their fees back as a rebate. **This is the optimal allocation.**
{% endhint %}
{% endtab %}
{% endtabs %}

See the documentation on Reward and fee distribution to learn more when and how indexing rewards and query fees are distributed:

{% page-ref page="reward-distribution.md" %}



