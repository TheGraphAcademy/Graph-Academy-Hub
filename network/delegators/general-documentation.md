# General Documentation

DRAFT



Everything delegators need to know





**What is query fee cut and indexing reward cut?**

The `queryFeeCut` and `indexingRewardCut` values are delegation parameters that the Indexer may set along with cooldownBlocks to control the distribution of GRT between the indexer and their delegators. See the last steps in [Staking in the Protocol](https://thegraph.com/docs/network#indexing_network_stake-in-protocol) for instructions on setting the delegation parameters.

* **queryFeeCut** - the % of query fee rebates accumulated on a subgraph that will be distributed to the indexer. If this is set to 95%, the indexer will receive 95% of the query fee rebate pool when an allocation is claimed with the other 5% going to the delegators.
* **indexingRewardCut** - the % of indexing rewards accumulated on a subgraph that will be distributed to the indexer. If this is set to 95%, the indexer will receive 95% of the indexing rewards pool when an allocation is closed and the delegators will split the other 5%.

