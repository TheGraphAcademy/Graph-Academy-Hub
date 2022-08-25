# Mastering Subgraphs

## Resources

### Documentation

* [https://thegraph.com/docs/quick-start#local-development](https://thegraph.com/docs/quick-start#local-development)
* [https://thegraph.academy/developers/defining-a-subgraph/](https://thegraph.academy/developers/defining-a-subgraph/)
* [https://discord.com/channels/438038660412342282/438070183794573313/839516110473658398](https://discord.com/channels/438038660412342282/438070183794573313/839516110473658398)

## Some Links

* [https://github.com/graphprotocol/rfcs/blob/master/engineering-plans/0004-subgraph-grafting.md](https://github.com/graphprotocol/rfcs/blob/master/engineering-plans/0004-subgraph-grafting.md)
* [https://docs.google.com/spreadsheets/d/1J2s-FE5n1XOZJra1WSjKrTpUYiV1lYORVD32IxotJM8/edit#gid=0](https://docs.google.com/spreadsheets/d/1J2s-FE5n1XOZJra1WSjKrTpUYiV1lYORVD32IxotJM8/edit#gid=0)
* [https://thegraph.com/docs/define-a-subgraph#ipfs-pinning](https://thegraph.com/docs/define-a-subgraph#ipfs-pinning)
* [https://github.com/graphprotocol/graph-node/blob/master/docs/getting-started.md#5-example-subgraphs](https://github.com/graphprotocol/graph-node/blob/master/docs/getting-started.md#5-example-subgraphs)
* [https://medium.com/protofire-blog/subgraph-development-part-1-understanding-and-aggregating-data-ef0c9a61063d](https://medium.com/protofire-blog/subgraph-development-part-1-understanding-and-aggregating-data-ef0c9a61063d)
* [https://medium.com/protofire-blog/subgraph-development-part-2-handling-arrays-and-identifying-entities-30d63d4b1dc6](https://medium.com/protofire-blog/subgraph-development-part-2-handling-arrays-and-identifying-entities-30d63d4b1dc6)
* [https://forum.thegraph.com/t/unit-testing-in-assembly-script/845](https://forum.thegraph.com/t/unit-testing-in-assembly-script/845)

```
#1 Tools:
Protofire Subgraph Toolkit:
-<https://github.com/protofire/subgraph-toolkit>
Gnosis Subgraphs Monitor:
-<https://github.com/gnosis/thegraph-subgraphs-monitor>
Synthetix Subgraph-results-pager:
-<https://github.com/justinjmoses/graph-results-pager>
Utility to get paged results from The Graph endpoints
GraphProtocol-utils:
-<https://github.com/Amxx/graphprotocol-utils>
mStable Subgraph Utilities:
-<https://github.com/mstable/mStable-subgraphs-monorepo/tree/master/packages/utils>
Dennison's Subgraph Health Check:
-~~https://subgraphtools.com/~~- Community videos:
	- Wildcards:<https://www.youtube.com/watch?v=_4iipzOwq-U>
	- Aragon:<https://www.youtube.com/watch?v=JNqN3fek6FY>
	- PoolTogether workshop @ETHDenver:<https://www.youtube.com/watch?v=GqU_-ffyz0Q&t=21143s-> Community Articles:
    -<https://medium.com/protofire-blog/subgraph-development-part-1-understanding-and-aggregating-data-ef0c9a61063d>
    -<https://medium.com/protofire-blog/subgraph-development-part-2-handling-arrays-and-identifying-entities-30d63d4b1dc6>
	- How to create an Ethereum DeFi realtime Dashboard using Google Data Studio:<https://towardsdatascience.com/how-to-create-a-ethereum-defi-realtime-dashboard-a60c23b527f7>
		- Result:<https://datastudio.google.com/reporting/c7806832-8ba6-4250-9c27-8dab1238247b/page/6zXD>
	- Creating subgraphs:
		-<https://theethernaut.substack.com/p/creating-a-dark-side-subgraph>
	-<https://theethernaut.substack.com/p/developer-superpowers-with-thegraph>
- Time travel queries:<https://blocklytics.org/blog/ethereum-blocks-subgraph-made-for-time-travel/>
- Date strings in AssemblyScript:<https://medium.com/blockrocket/how-to-create-date-strings-using-assemblyscript-in-the-graph-f7871f48e92d-> Scaffold-eth:<https://github.com/austintgriffith/scaffold-eth/tree/graph-dev>
- Create-eth-app:<https://github.com/PaulRBerg/create-eth-app>
```

### Examples

* [https://github.com/enzymefinance/enzyme-subgraph](https://github.com/enzymefinance/enzyme-subgraph)
* [https://github.com/graphprotocol/everest](https://github.com/graphprotocol/everest)
* [https://github.com/graphprotocol/graph-network-subgraph](https://github.com/graphprotocol/graph-network-subgraph)
* [https://github.com/schmidsi/generic-erc721-subgraph](https://github.com/schmidsi/generic-erc721-subgraph) (Quite simple)

### Videos

[https://www.youtube.com/watch?v=4V2o5YJooOM](https://www.youtube.com/watch?v=4V2o5YJooOM)

[https://www.youtube.com/watch?v=SNmzhwlQqgU\&list=PLTqyKgxaGF3QTJv0JC7jHl6BenQ6yZEOG](https://www.youtube.com/watch?v=SNmzhwlQqgU\&list=PLTqyKgxaGF3QTJv0JC7jHl6BenQ6yZEOG)

## Patterns

### Do

### Don't

* Entity names should be singular: `type UserClaimedReward @entity` instead of `type UserClaimedRewards @entity`

### Common Queries

#### **Q1. If one can index events from two different chains under the same subgraph ?**

A1. SubGraph composability is still something we are looking into. Till then u will not be able to query to Blockchains that is xDai as well as MainNet using one Graph. However, u can create two subgraphs for two chains and display them on a single front-end so in that case, no end-user is affected. For that u can use -[https://www.graphql-tools.com/docs/schema-stitching/](https://www.graphql-tools.com/docs/schema-stitching/)

#### **Q2. Is there a Subgraph Unit Testing Framework**

A2.[https://forum.thegraph.com/t/unit-testing-in-assembly-script/845/18](https://forum.thegraph.com/t/unit-testing-in-assembly-script/845/18)

**Q3. Deploying Subgraph with HardHat**

A3.[https://forum.thegraph.com/t/testing-best-practices/903/4?u=pranav](https://forum.thegraph.com/t/testing-best-practices/903/4?u=pranav)

Testing file example -[https://github.com/withtally/Generic-Subgraph-Testing](https://github.com/withtally/Generic-Subgraph-Testing)

**Q4. Error- Handler skipped due to execution failure, error: wasm trap: unreachable wasm backtrace**

A4. array access out of bounds

**Q5. Deployed my Subgraph on BSC chain but it's not Syncing**

A5. There is a problem with the BSC nodes, tracking on our status page:[https://status.thegraph.com/](https://status.thegraph.com/)

**Q6. Is there a Block-Ethereum Network subgraph**

A6.[https://thegraph.com/explorer/subgraph/blocklytics/ethereum-blocks](https://thegraph.com/explorer/subgraph/blocklytics/ethereum-blocks)

**Q7. Any idea how to add multiple sources?**

A7. Yes it is possible-

dataSources:

* kind: ethereum/contract name: ContractOne network: xdai mapping: kind: ethereum/events ....
* kind: ethereum/contract name: ContractTwo network: xdai mapping: kind: ethereum/events

**Q8. Subgraph is too slow indexing. How can I optimise:**

A8.

Ways to optimise your subgraph:

a) Only use event handlers

b) Start by optimising the smart contracts so that everything you need for indexing is included in the event parameters

c) Avoid contract calls in the handlers - possible if you have everything or nearly everything in the event payloads, see b)

f) Avoid ipfs calls

d) Avoid unnecessary `.loads`of entity - possible when no data from the entity needs to be read first to do the update

e) Avoid large / boundless arrays in entity properties

Also consider splitting the subgraph up into separate subgraphs which can sync in parallel

To go more in-depth, I recommend

[https://medium.com/protofire-blog/subgraph-development-part-1-understanding-and-aggregating-data-ef0c9a61063d…](https://medium.com/protofire-blog/subgraph-development-part-1-understanding-and-aggregating-data-ef0c9a61063d%E2%80%A6)

,

[https://medium.com/protofire-blog/subgraph-development-part-2-handling-arrays-and-identifying-entities-30d63d4b1dc6…](https://medium.com/protofire-blog/subgraph-development-part-2-handling-arrays-and-identifying-entities-30d63d4b1dc6%E2%80%A6)

and

[https://youtube.com/watch?v=4V2o5YJooOM…](https://youtube.com/watch?v=4V2o5YJooOM%E2%80%A6)

In general, as other degens already pointed out: Avoid eth-calls, focus on event-handlers, avoid unnecessary data loading.

**Q9. How can I index ether transaction in the subgraph?**

A9. Transactions can not be indexed. You can currently only index on the basis of contract events, contract calls and blocks

Q10. How Create an Entity to be saved in store

```
 let transfer = new Transfer(id) // Transfer is a schema

  // Set properties on the entity, using the event parameters
  transfer.from = event.params.from
  transfer.to = event.params.to
  transfer.amount = event.params.amount

  // Save the entity to the store
  transfer.save()
```

Q11. Load and update Entity from the store

```
let id = event.transaction.hash.toHex() // or however the ID is constructed
let transfer = Transfer.load(id)
if (transfer == null) {
  transfer = new Transfer(id)
}
transfer.from = events.params.from
transfer.to = ...
transfer.amount = ...
transfer.save()
```

Q12. Delete an Entity

```
import { store } from '@graphprotocol/graph-ts'
...
let id = event.transaction.hash.toHex()
store.remove('Transfer', id)
```

Q13. How to query logs locally

You can query the index-node endpoint to fetch fatal Error information:

If it's the current version of your subgraph:

```
curl --location --request POST '<https://api.thegraph.com/index-node/graphql>'  --data-raw '{"query":"{ indexingStatusForCurrentVersion(subgraphName: \\"<SUBGRAPH-NAME>\\") { subgraph synced fatalError { message } nonFatalErrors {message } } }"}'
```

If it's the pending version of your subgraph:

```
curl --location --request POST '<https://api.thegraph.com/index-node/graphql>'  --data-raw '{"query":"{ indexingStatusForPendingVersion(subgraphName: \\"<SUBGRAPH-NAME>\\") { subgraph fatalError { message } nonFatalErrors {message } } }"}'
```

Q14. Delegation FAQ

[https://forum.thegraph.com/t/delegators-protocol-actions-faq/89](https://forum.thegraph.com/t/delegators-protocol-actions-faq/89)

[https://thegraph.academy/delegators/how-to-delegate-grt-tokens/](https://thegraph.academy/delegators/how-to-delegate-grt-tokens/)

Q15. Deploying subgraphs from contract address

```
graph init --from-contract 0xabEFBc9fD2F806065b4f3C237d4b59D9A97Bcac7 --network mainnet  \\
--contract-name Token --index-events
```

Q16. How to connect locally deployed graph node to ganache

Archive node of [docker file](https://github.com/graphprotocol/graph-node/blob/master/docker/docker-compose.yml#L20) pointing to - ethereum: 'mainnet:[http://127.0.0.1:7545](http://127.0.0.1:7545)'

change the docker network to use the host

or use the docker links to the host

run a dockerized ganache

[https://github.com/moby/moby/pull/40007](https://github.com/moby/moby/pull/40007)

Use `mainnet:http://host.docker.internal:7545`

If that works, all good.

Otherwise put in the IP address following these instructions: `CONTAINER_ID=$(docker container ls | grep graph-node | cut -d' ' -f1) docker exec $CONTAINER_ID /bin/bash -c 'apt install -y iproute2 && ip route' | awk '/^default via /{print $3}'`

[https://discord.com/channels/438038660412342282/438070183794573313/844302091530797106](https://discord.com/channels/438038660412342282/438070183794573313/844302091530797106)

Q17. Is there a way to move new subgraph we deploy to a different endpoint ?

If you deploy under a different name, but with the exact same hash, the underlining deployment will be reused so there will be no sync time

Q18. Steps for deployment

Step1: npm install -g @graphprotocol/graph-cli

Step2: yarn global add @graphprotocol/graph-cli

Step3: graph auth[https://api.thegraph.com/deploy/](https://api.thegraph.com/deploy/) \<ACCESS\_TOKEN>

Step4:

graph deploy \ --debug \ --node [https://api.thegraph.com/deploy/](https://api.thegraph.com/deploy/) \ --ipfs [https://api.thegraph.com/ipfs/](https://api.thegraph.com/ipfs/) \ \<SUBGRAPH\_NAME>

Q19. TimeTravel queries might fail if A19.

1.Block not Onchain

1. ReOrg

[https://github.com/graphprotocol/graph-node/issues/1405](https://github.com/graphprotocol/graph-node/issues/1405)

Q20. How to debug when deploying graph-node locally A.20 RUST\_LOG : debug in docker-compose file

For newer graph-node versions (>0.22.0): GRAPH\_LOG: info

Q21. Data source within a block are ordered using the following process:

1. Event and call triggers are first ordered by transaction index(as per the sequence of trx in dapp) within the block.
2. Event and call triggers with in the same transaction are ordered using a convention: event triggers first then call triggers
3. Block triggers are run after event and call triggers, in the order they are defined in the manifest.

Q22: Arweave support

There is basic Arweave support:[https://github.com/graphprotocol/graph-node/blob/a4315a33652391f453031a5412b6c51ba4ce084c/NEWS.md#feature-arweave-transaction-data-1574](https://github.com/graphprotocol/graph-node/blob/a4315a33652391f453031a5412b6c51ba4ce084c/NEWS.md#feature-arweave-transaction-data-1574)

Q23: HTTP error creating the subgraph: ECONNREFUSED

Are you trying to deploy to the hosted service? There, you need to create your subgraph through the UI first:[https://thegraph.com/explorer/dashboard](https://thegraph.com/explorer/dashboard)

Q24: IndexingStatus local graph-node

[http://localhost:8030/graphql](http://localhost:8030/graphql)

Run these query:

```graphql
 
{
  indexingStatusForCurrentVersion(subgraphName: "aave/protocol") {
    node
    synced
    health
    fatalError {
      message
    }
    chains {
      network
      chainHeadBlock {
        number
      }
      earliestBlock {
        number
      }
      latestBlock { 
        number 
      }
      lastHealthyBlock { 
        number
      }
    }
    entityCount
  }
  
}
```

Q25. Command to track RPC and rectify the block it is in

curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth\_getBlockByNumber","params":\["latest", false],"id":1}'[https://rpc-graph-mainnet.maticvigil.com/v1/7d25a9c3aca826c9d24fed0c273f686b28f4b0e5](https://rpc-graph-mainnet.maticvigil.com/v1/7d25a9c3aca826c9d24fed0c273f686b28f4b0e5)

Q26: "message": "Store error: store error: type Subscription already exists in the input schema"

The `schema.graphql` probably contains a type `Subscription`. [Example](https://github.com/iamsahu/idatest/blob/33c400406a65db5dcebbe5162f770f46d8f516c8/schema.graphql#L11). This is a reserved word. Find another word.

Q27 How to deprecate a subgraph from the network

Assume this is one of the ones they want to deprecate:

[https://thegraph.com/explorer/subgraph?id=0xacfe4511ce883c14c4ea40563f176c3c09b4c47\[…\]n=0xacfe4511ce883c14c4ea40563f176c3c09b4c47c-1-0\&view=Overview](https://thegraph.com/explorer/subgraph?id=0xacfe4511ce883c14c4ea40563f176c3c09b4c47%5B%E2%80%A6%5Dn=0xacfe4511ce883c14c4ea40563f176c3c09b4c47c-1-0\&view=Overview)

they should go here

[https://etherscan.io/address/0xadca0dd4729c8ba3acf3e99f3a9f471ef37b6825#writeProxyContract](https://etherscan.io/address/0xadca0dd4729c8ba3acf3e99f3a9f471ef37b6825#writeProxyContract)

and call \`deprecateSubgraph with their own address as the first param, and the subgraph number as 1 . and it should work!

Q28. Recover Subgraph from depreciated subgraphs

!! YOU CAN RECOVER YOUR GRT !! Step 1: Go to the GraphProxy[https://etherscan.io/address/0xadca0dd4729c8ba3acf3e99f3a9f471ef37b6825#writeProxyContract](https://etherscan.io/address/0xadca0dd4729c8ba3acf3e99f3a9f471ef37b6825#writeProxyContract) Step 2:Find the "withdraw" function Step 3: Put the graph account as 0xacfe4511ce883c14c4ea40563f176c3c09b4c47c with subgraphNumber = 1 Step 4: Write the txn (you can connect Etherscan to your metamask wallet)

Q29: API Key security

if my dapp frontend uses the graph for query, do I want to write my query key into the frontend directly? If we pay query fees for users, will malicious users cause our query fees to be very high?

→

This is actually a very frequently asked question and the answer has different dimensions:

* Currently yes, the recommended approach for a dapp is to add the key to the front-end and actually expose it. That said, you can limit that key to a host-name, like [yourdapp.io](http://yourdapp.io/), and subgraphs.
* The gateway is currently run by Edge and Node and we monitor the queries. If we detect abuses or you report an abuse, we can block IPs, etc.
* This system is actually not that different of running a server/API by yourself: It is also open to the public and one can try to attack it.
* Long term we envision that users will pay for their queries directly.

1. Is there a limit to graph results? because i can see max upto 100 results, nothing after that?

I think it displays only the first 100 by default, but try to query with first: 1000, skip: 1000 to view the next ones

Q31. Check for EIP\_1898 compatibility for an rpc curl -X POST --data '{"jsonrpc":"2.0","method":"eth\_call","params":\[{"data":"0x0902f1ac","gas":"0x2faf080","to":"0x58f876857a02d6762e0101bb5c46a8c1ed44dc16"},{"blockHash":"0xab9316c3461cb0377666b2d442d7a5fb3d327eeb6934d17263fa42ef5cc385c6"}],"id":1033989}'[https://bsc-dataseed-archive-graph.nariox.org/](https://bsc-dataseed-archive-graph.nariox.org/)

Q32 Getting CORS error on graph API Ans) The CORS errors are intermittent, we are narrowing them down but basically it is a problem with the router. Could happen when we deploy new releases or if we see an unexpected load spikes. Usually, it resolves by itself after a while like it did for you. Feel free to ping us here if you see any other problems anytime.

## Sub-Topics

[Scaler](https://www.notion.so/Scaler-be9d9a2067864fc8919fffe270c2a6df)

How to deploy on Staging

1. LogIN to -[https://staging.thegraph.com/legacy-explorer/](https://staging.thegraph.com/legacy-explorer/)
2. graph auth --product hosted-service-staging e8986681830b4ebcb0c236749f40b101 --ipfs[https://api.staging.thegraph.com/ipfs/](https://api.staging.thegraph.com/ipfs/) --node[https://api.staging.thegraph.com/deploy/](https://api.staging.thegraph.com/deploy/)
3. graph deploy pranavdaa/openzappelinsubgraph --access-token \<Token> --ipfs[https://api.staging.thegraph.com/ipfs/](https://api.staging.thegraph.com/ipfs/) --node[https://api.staging.thegraph.com/deploy/](https://api.staging.thegraph.com/deploy/)

Grafana Log commands -[https://grafana.com/docs/loki/latest/logql/](https://grafana.com/docs/loki/latest/logql/)

1. {app="index-node",cluster="hosted-service-production",pod="index-node-community-0"} |= "QmNtawNYjWwUzcrnCjV87jvtjQWtvezKe5PnyFq46JfMuP"
2. {app="index-node",cluster="hosted-service-production",pod=\~"index-node-community-.\*"}
3. {app="index-node",cluster="hosted-service-production",pod="index-node-community-0"} != "QmNtawNYjWwUzcrnCjV87jvtjQWtvezKe5PnyFq46JfMuP" |= "handleBlock" |\~ "total.\*"
4. {cluster="hosted-service-production",app\_kubernetes\_io\_name="ingress-nginx"} |= "/subgraphs/name/uniswap/uniswap-v2"
5. {cluster="hosted-service-production",app=\~"query-node.\*"

For Subgraphs deployed on the network serving any issues

1. {cluster=\~"mainnet-indexer-01-us-central|mainnet-indexer-02-europe-west|mainnet-indexer-03-us-west|mainnet-indexer-04-us-east|mainnet-indexer-05-eu-central|mainnet-indexer-07-asia-northeast",deployment="QmWK7Phe4L6H3dzXHh48G1TrYDugeAVaFroUke3y2c7Kai"}

## Random Notes

graphman is a command line tool that is part of graph-node (when you build graph-node, graphman is also built) It's available in all the graph-node docker images, and on all our index-node-\* and query-node-\* pods. It uses the normal graph-node code to expose some useful admin functionality in a CLI.

You can get more insight into how a query performs by running `GRAPH_LOG_QUERY_TIMING=sql,gql GRAPH_LOG=debug graphman query Qm... 'query { .. }'` for example in `index-node-community-quarantine-0`

[**lutter**](https://app.slack.com/team/UF6EQHC15)

That will print timing information about each SQL query that gets run for a GraphQL query, and you can then throw that SQL into `psql` and do an `explain` on it

[**lutter**](https://app.slack.com/team/UF6EQHC15)

For quickswap, I looked into some of the slow queries a while ago, and tried created some indexes. For that order by query, often creating an index on `token(trade_volume_usd, id)` helps with those (or a gist index on `token(block_range, trade_volume_usd, id)`, but for quickswap neither of these brought a significant improvement

***

The easiest way to play with it is if you log into a pod in staging:

```
> kubectl --context=staging exec index-node-community-quarantine-0 -ti -- /bin/bash
# unset GRAPH_LOG
# graphman help
# graphman info -s lutter/dice2win
```

[17:40](https://graphprotocol.slack.com/archives/C01P2DS1Z17/p1621006806200500)

You can also run it against your local `graph-node`; it requires a [config file](https://github.com/graphprotocol/graph-node/blob/master/docs/sharding.md), a simple example for one is [here](https://github.com/graphprotocol/graph-node/tree/master/store/test-store) in `config.simple.toml`

`curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest", false],"id":1}' -H "Content-Type: application/json" [<https://rpc.testnet.moonbeam.network>](<https://rpc.testnet.moonbeam.network/>)`

GraphQL interface to query node status:[http://127.0.0.1:8030/graphql/playground](http://127.0.0.1:8030/graphql/playground)

[https://api.thegraph.com/index-node/graphql](https://api.thegraph.com/index-node/graphql) (In a GraphQL Client like Altair)

[https://graphiql-online.com](https://graphiql-online.com)

### Install `graphman` locally

* Have postgres installed: `brew install postgresql`
* `cargo build`
* `cargo install --bin graphman --path node --locked`

curl --location --request POST '[https://api.thegraph.com/index-node/graphql](https://api.thegraph.com/index-node/graphql)' --data-raw '{"query":"{ indexingStatusForPendingVersion(subgraphName: \\"bigwin-official/bunny\_v2\\") { subgraph fatalError { message } nonFatalErrors {message } } }"}'

IPFS issue info

curl -X POST "[https://api.thegraph.com/ipfs/api/v0/cat?arg=QmdddHxo4aAXu5b7dJaWQpLiLsaWs16JubHg71ZGbKgHqT](https://api.thegraph.com/ipfs/api/v0/cat?arg=QmdddHxo4aAXu5b7dJaWQpLiLsaWs16JubHg71ZGbKgHqT)"

Making graphman run with indexer login

[https://cloud.google.com/kubernetes-engine/docs/quickstart](https://cloud.google.com/kubernetes-engine/docs/quickstart)

Hosted service

[https://www.notion.so/edgeandnode/Maintenance-tasks-f11930c057f14870922822aaacd70b70](https://www.notion.so/edgeandnode/Maintenance-tasks-f11930c057f14870922822aaacd70b70)
