---
description: Documentation for Indexers on indexing and querying
---

# Indexing & Querying

## IP addresses of query traffic

Indexers should expect to receive requests from the following IP addresses:

```
34.66.143.111
35.193.209.143
35.202.175.180
34.72.59.178
34.122.80.18
34.67.243.209
35.188.137.254
35.222.115.231
34.72.172.209
```

## Evaluating subgraphs

Indexers can use the following key metrics to evaluate subgraphs. Based on this evaluation, they can decide which subgraphs they index on the network.

{% tabs %}
{% tab title="Curation Signal" %}
### Curation Signal

[Curators](../../curators.md) stake GRT in order to signal to Indexers which subgraphs are of a high-quality and should accordingly be indexed in the network. The strength of the curation signal is an indicator to Indexers about the interest in the curated subgraph.

{% hint style="success" %}
This is especially true during the bootstrapping phase during which query volume is starting to ramp up.
{% endhint %}
{% endtab %}

{% tab title="Collected query fees" %}
### Collected query fees

The future demand of a subgraph can be estimated by assessing historical data about the volume of query fees collected on the subgraph.

{% hint style="danger" %}
Past performance is no guarantee of **future** results. Therefore, the amount of collected query fees should only be taken into consideration with other factors.
{% endhint %}
{% endtab %}

{% tab title="Amount staked" %}
**Amount staked**

By having a look at the total stake allocated towards a specific subgraph, Indexers are able to gauge the network's interest in it. Doing so helps Indexers to monitor the supply side for subgraph queries.

{% hint style="info" %}
By means of evaluating the supply side, subgraphs that may need more supply or subgraphs that the network is showing confidence in are highlighted.
{% endhint %}
{% endtab %}
{% endtabs %}
