# Reward Statuses

Documentation for better understanding the statuses of rewards in The Graph Network.

## Pending

The reward status `pending` refers to your rewards being accumulated in an active allocation by the indexer. It can fluctuate by an increase/decrease of total allocation size by the Indexer but also by time passing by. [Oracleminder.com](https://oracleminer.com/graph/indexers/) can be used to see total pending rewards and also pending rewards of an Indexer and of the Delegators of that Indexer.

{% hint style="danger" %}
The rewards in `pending` are subject to changes of the Indexers indexing and fee cuts. This is a vulnerability that can be exploited by malicious Indexers, see the link to Indexer Behavior below.
{% endhint %}

{% content-ref url="../../indexers/vulnerabilities.md" %}
[vulnerabilities.md](../../indexers/vulnerabilities.md)
{% endcontent-ref %}

## Unrealized

The section `unrealized` shows the final amount of GRT that has been assigned to you. The network automatically add your unrealized rewards to your existing delegation and is referred to as `automatic compounding`.

## Realized

Once you have exited your rewards (subject to a 28 day thawing period) you can withdraw your realized rewards. It is important to note that your realized rewards are no longer delegated and do no longer earn rewards.
