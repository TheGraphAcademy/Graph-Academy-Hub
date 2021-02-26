---
description: What are Indexers in The Graph Network?
---

# Indexers

Indexers operate nodes in The Graph Network and provide indexing and query processing services to customers. By staking Graph Tokens \(GRT\), Indexers earn **indexing rewards** and **query fees** for their services. Additionally, Indexers earn from a **Rebate Pool** that is shared with all network contributors proportional to their work, following the [Cobb-Douglas Production Function](https://en.wikipedia.org/wiki/Cobb%E2%80%93Douglas_production_function). See [Revenue Streams](revenues/revenue-streams.md) for more details on Indexer incentives.

{% hint style="danger" %}
The technical level to participate in the network as an Indexer is **ADVANCED**. To get started as an Indexer, follow the [Indexer documentation](https://thegraph.com/docs/network#infrastructure).
{% endhint %}

### Requirements

Indexers need to stake at least 100k GRT tokens to run a node and participate in the network as an Indexer. Aside from the technical knowledge to run a node, Indexers also have to be able to provide the technical infrastructure for doing so.

### Function in the network

Indexers select subgraphs in The Graph Network to index. Customers \(typically end-users\) query the indexed data by paying for their metered usage based on the laws of supply and demand. Indexers are running an indexer agent that programmatically monitors their resource usage, sets prices, and decides which subgraphs to index. Indexers can set their own pricing models and strategies to gain a competitive edge in the marketplace.

The selection of subgraphs by indexers is based on subgraph’s curation signal, where [Curators ](../curators.md)stake GRT in order to indicate which subgraphs are high-quality and should be prioritized. Consumers \(eg. applications\) can also set parameters for which Indexers process queries for their subgraphs and set preferences for query fee pricing.

### Indexer staking

The Graph utilizes a [work token](https://multicoin.capital/2018/02/13/new-models-utility-tokens/) model. Based on this model, service providers to the network such as Indexers must stake Graph Tokens \(GRT\) in order to sell their services in the query market. The adoption of the work token model serves to primary functions:

* **Economic security:** GRT that is staked can be slashed \(_see below for more information on slashing_\)
* **Sybil resistance:** Only indexers who are willing to invest resources are able to participate

Indexers are incentivized to hold GRT roughly in proportion to the amount of work they seek to contribute to the network.

### Slashing risks

Indexers in The Graph Network are incentivized to provide honest and reliable indexing and query processing services. In order to safeguard that Indexer misbehavior is discouraged, Indexers have to stake GRT that is subject to a thawing period. If Indexers act maliciously, serve incorrect data to applications or index incorrectly, their staked GRT can be slashed.

Slashing is a mechanism built into The Graph protocol to discourage and punish malicious Indexer behavior. Additionally, slashing incentivizes node security, availability, and network participation. 

{% hint style="success" %}
It is important to note that [curators ](../curators.md)and [delegators ](../delegators/)are not subject to slashing or other punishments for Indexer misbehavior.
{% endhint %}

### Delegation

Indexers can also be delegated stake from Delegators, to contribute to the network. You can find further documentation about delegators here:

{% page-ref page="../delegators/" %}

### Thawing period

GRT that is staked by Indexers in the protocol is subject to a **thawing period** and can be **slashed** if Indexers act maliciously. 

### Cooldown period 

Indexers have a “cooldown” that determines how often they can change delegation parameters. Indexers are free to decide the cooldown period but are subject to reprimands by the free market. All other things being equal, Indexers who set longer cooldowns should receive more delegation from delegators.

