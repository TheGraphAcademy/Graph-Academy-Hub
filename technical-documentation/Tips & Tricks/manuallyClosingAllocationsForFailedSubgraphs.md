{% hint style="info" %}
## Contributor Details
This documentation was contributed by **Gary Morris** at [0xFury](https://www.0xfury.com/). 0xFury is a blockchain infrastructure provider with a focus on decentralization and projects that push for Web3 enablement. 0xFury has been running Graph Indexer services actively since the original testnet phase.
{% endhint %}

Manually Closing Allocations for a Failed Subgraph
========
## Summary
You can use this guide to close allocations for any situation, but if the allocation is healthy i.e. the subgraph has not failed, you are better served by using the agent to close the allocation. This will avoid causing any confusion in the agent's process. This is not an issue when an allocation is for a failed subgraph that is past its last good Epoch, because the agent will be unable to close that allocation anyway because the PoI will be invalid (and the agent logs will say as much).

Warning: This guide does not currently settle the queryFees for you. If this is possible, it will be added to the guide at a later date. Be warned that your queryFees for any manually closed allocation will not be claimed automatically.

### Retrieve the last good PoI
You can query your PoIs for an allocation in two ways.

**1. Using GraphQL against your own query node graphql endpoint (http://query-node:8030/graphql)**

```bash
query {
    proofOfIndexing(
        subgraph: "**XXXXXXXXXX**"
        blockHash: "**XXXXXXXXXX**"
        blockNumber: **XXXXXXXXXX**
        indexer: "**XXXXXXXXXX**"
        )
}
```

**2. Via CLI:**

```bash
http -b post http://localhost:8030/graphql \
query='query poi($blockNumber: Int!) { proofOfIndexing(\
subgraph: "**XXXXXXXXXX**", blockNumber: $blockNumber, \
blockHash: "**XXXXXXXXXX**", \
indexer: "**XXXXXXXXXX**") }' variables:='{ "\
blockNumber": **XXXXXXXXXX** }'
```

- subgraph : ID of the subgraph your allocation is on.
- blockNumber : First block of the Epoch you're querying for (this should be the last Epoch in which the failed subgraph was working correctly).
    - You can find the first block of the Epoch in question using the following graphql query against the network subgraph:

        ```graphql
        {
          graphNetwork(id:1){
            currentEpoch
          }
          epoch(id: XXX){
            startBlock
          }
        }
        ```

- blockHash: : Hash of the block `blockNumber`.
    - You have some options to get the blockHash of the first block in the Epoch
        - Geth - if you have a geth node you can query for the blockhash like so:
            - `geth --exec 'eth.getBlock(eth.blockNumber).hash' attach`
            - Search for the block on Etherscan
- indexer : Your Indexer ID.

---

**Note:**

To maximize your rewards in the case of a failed subgraph, you should check each Epoch to see which is the latest one you have a (valid) PoI for.

This guide only covers how to obtain the PoI held by your own Indexer. However, or whether, you decide to further validate it beyond that, is another topic.

**Considerations around the indexer-agent before manually closing an allocation**

It is recommended that before submitting a manual allocation close, you `never` the failed allocation in your agent e.g.:

- `graph indexer rules set <subgraphHash> never`

When you do this, your agent will try and settle the allocation but will find that it cannot retrieve a valid POI per the agent logs:

- `ERROR (IndexerAgent/13217 on agenttesting): Received a null or zero POI for deployment`

---

### Submit the last good PoI manually

Once you have obtained your POI. You can submit it via Etherscan on this Proxy contract:

[https://etherscan.io/address/0xf55041e37e12cd407ad00ce2910b8269b01263b9#writeProxyContract](https://www.notion.so/7e12cd407ad00ce2910b8269b01263b9)

1. Connect your wallet via MetaMask or WalletConnect, and click the "Connect to Web3" button near the top-left of the page.
2. Click on `7. closeAllocation`.
3. Get your allocation ID(s) that relate to this POI.
    - You can see your allocation IDs per subgraph on your Indexer page of [https://graphscan.io](https://graphscan.io/)
    - Scroll to the right-side under the Allocations tab.
4. Enter the allocation IDs for the subgraph in question in to the `_allocationID (address)` field.
5. Enter the POI you queried from your node in the above steps in the `_poi (bytes32)` field.
6. Click "Write" and send the TX with your wallet.
7. Do this for each allocation for the subgraph/POI you want to manually close on.
