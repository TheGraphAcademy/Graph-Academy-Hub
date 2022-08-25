# Substreams

StreamingFast has evolved Sparkle’s capabilities and created substreams that can scale across all subgraphs on all chains.

{% embed url="https://www.youtube.com/watch?v=Nn6k7A-TjVE" %}

### How Substreams Work

RPC-based Subgraphs have a linear indexing model for processing blockchain data (i.e. they process events one at a time, in order). They do so via polling API calls to Ethereum clients. Firehose technology replaces those polling API calls with a stream of data utilizing a push model and sending data to the indexing node faster. This helps increase the speed of syncing and indexing.

Substreams take things even further by enabling massively parallelized streaming data. Substreams can be combined and aggregated in powerful new ways to feed data into subgraphs or end-user applications in a fraction of the time. With substream parallelization, some subgraphs could sync more than 100x faster.

With substreams, the data pipeline can be broken down into four stages:

* Extract (via Firehose)
* Transform (via Substreams and Subgraphs)
* Load (to the postgres database)
* Query (serving queries to users)

The first transformation via substreams allows lighter weight parallelized computation and composability that many subgraphs can benefit from.

To illustrate: in the instance of large DEXes—which need to find pairs for any given trade—a substream model enables individual small modules to work simultaneously on pairs, reserve extractors, prices, volume aggregation, and other key metrics. If a developer bases their work on existing substreams, they can take the DEX prices and create a module to average all DEX prices across an ecosystem.

Substream modules don’t go through postgresQL. Existing modules can be leveraged, which developers can adapt, allowing end users to take advantage of composability without paying a performance penalty for indexing.

After the Extraction and Transformation stages, substreams can be composed in an infinite number of ways, enabling another module to populate into a subgraph, all before Load operations.

As opposed to linear historical data processing, substream data can be processed in parallel and cached. This allows for the fastest possible insertion into the postgres database, going from days or weeks to mere hours.

This all serves as a benefit to developers. Developers need to build subgraphs and should be able to iterate on those subgraphs as fast as possible, maximizing developer productivity. Developers will be able to iterate upon existing modules, reuse the most efficient processes (such as in the DEX example), using incremental iterations to improve without needing to rebuild a new subgraph. They will be able to observe data and add to their database as required. The speed and data composability of subgraphs and substreams, pulling data through Firehose, will make The Graph the fastest and most efficient way to get data from blockchains.

This is the power of open-source data composability via The Graph: a hivemind of developers building composable data across a global ecosystem. Centralized services cannot compete.

### Current Stage in the Process

An initial implementation of substreams has been built and is being tested. The core devs are working with a small group of developers to improve the software. Keep an eye out for announcements on availability for developers.

Thanks to all the core dev teams that have worked on this (special shoutout to StreamingFast!). We can’t wait for developers to experience the radically faster indexing performance enabled by substreams.
