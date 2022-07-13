# Building Subgraphs on NEAR



> NEAR support in Graph Node and on the Hosted Service is in beta: please contact [near@thegraph.com](mailto:near@thegraph.com) with any questions about building NEAR subgraphs!

This guide is an introduction to building subgraphs indexing smart contracts on the [NEAR blockchain](https://docs.near.org/).

### What is NEAR? <a href="#what-is-near" id="what-is-near"></a>

[NEAR](https://near.org/) is a smart contract platform for building decentralized applications. Visit the [official documentation](https://docs.near.org/docs/concepts/new-to-near) for more information.

### What are NEAR subgraphs? <a href="#what-are-near-subgraphs" id="what-are-near-subgraphs"></a>

The Graph gives developers tools to process blockchain events and make the resulting data easily available via a GraphQL API, known individually as a subgraph. [Graph Node](https://github.com/graphprotocol/graph-node) is now able to process NEAR events, which means that NEAR developers can now build subgraphs to index their smart contracts.

Subgraphs are event-based, which means that they listen for and then process on-chain events. There are currently two types of handlers supported for NEAR subgraphs:

* Block handlers: these are run on every new block
* Receipt handlers: run every time a message is executed at a specified account

[From the NEAR documentation](https://docs.near.org/docs/concepts/transaction#receipt):

> A Receipt is the only actionable object in the system. When we talk about "processing a transaction" on the NEAR platform, this eventually means "applying receipts" at some point.

### Building a NEAR Subgraph <a href="#building-a-near-subgraph" id="building-a-near-subgraph"></a>

`@graphprotocol/graph-cli` is a command-line tool for building and deploying subgraphs.

`@graphprotocol/graph-ts` is a library of subgraph-specific types.

NEAR subgraph development requires `graph-cli` above version `0.23.0`, and `graph-ts` above version `0.23.0`.

> Building a NEAR subgraph is very similar to building a subgraph that indexes Ethereum.

There are three aspects of subgraph definition:

**subgraph.yaml:** the subgraph manifest, defining the data sources of interest, and how they should be processed. NEAR is a new `kind` of data source.

**schema.graphql:** a schema file that defines what data is stored for your subgraph, and how to query it via GraphQL. The requirements for NEAR subgraphs are covered by [the existing documentation](https://thegraph.com/docs/en/developer/create-subgraph-hosted/#the-graphql-schema).

**AssemblyScript Mappings:** [AssemblyScript code](https://thegraph.com/docs/en/developer/assemblyscript-api/) that translates from the event data to the entities defined in your schema. NEAR support introduces NEAR-specific data types and new JSON parsing functionality.

During subgraph development there are two key commands:

```
$ graph codegen # generates types from the schema file identified in the manifest$ graph build # generates Web Assembly from the AssemblyScript files, and prepares all the subgraph files in a /build folder
```

#### Subgraph Manifest Definition <a href="#subgraph-manifest-definition" id="subgraph-manifest-definition"></a>

The subgraph manifest (`subgraph.yaml`) identifies the data sources for the subgraph, the triggers of interest, and the functions that should be run in response to those triggers. See below for an example subgraph manifest for a NEAR subgraph::

```
specVersion: 0.0.2schema:  file: ./src/schema.graphql # link to the schema filedataSources:  - kind: near    network: near-mainnet    source:      account: app.good-morning.near # This data source will monitor this account      startBlock: 10662188 # Required for NEAR    mapping:      apiVersion: 0.0.5      language: wasm/assemblyscript      blockHandlers:        - handler: handleNewBlock # the function name in the mapping file      receiptHandlers:        - handler: handleReceipt # the function name in the mapping file      file: ./src/mapping.ts # link to the file with the Assemblyscript mappings
```

* NEAR subgraphs introduce a new `kind` of data source (`near`)
* The `network` should correspond to a network on the hosting Graph Node. On the Hosted Service, NEAR's mainnet is `near-mainnet`, and NEAR's testnet is `near-testnet`
* NEAR data sources introduce an optional `source.account` field, which is a human-readable ID corresponding to a [NEAR account](https://docs.near.org/docs/concepts/account). This can be an account or a sub-account.

NEAR data sources support two types of handlers:

* `blockHandlers`: run on every new NEAR block. No `source.account` is required.
* `receiptHandlers`: run on every receipt where the data source's `source.account` is the recipient. Note that only exact matches are processed ([subaccounts](https://docs.near.org/docs/concepts/account#subaccounts) must be added as independent data sources).

#### Schema Definition <a href="#schema-definition" id="schema-definition"></a>

Schema definition describes the structure of the resulting subgraph database and the relationships between entities. This is agnostic of the original data source. There are more details on subgraph schema definition [here](https://thegraph.com/docs/en/developer/create-subgraph-hosted/#the-graphql-schema).

#### AssemblyScript Mappings <a href="#assembly-script-mappings" id="assembly-script-mappings"></a>

The handlers for processing events are written in [AssemblyScript](https://www.assemblyscript.org/).

NEAR indexing introduces NEAR-specific data types to the [AssemblyScript API](https://thegraph.com/docs/en/developer/assemblyscript-api/).

```
class ExecutionOutcome {      gasBurnt: u64,      blockHash: Bytes,      id: Bytes,      logs: Array<string>,      receiptIds: Array<Bytes>,      tokensBurnt: BigInt,      executorId: string,  }
class ActionReceipt {      predecessorId: string,      receiverId: string,      id: CryptoHash,      signerId: string,      gasPrice: BigInt,      outputDataReceivers: Array<DataReceiver>,      inputDataIds: Array<CryptoHash>,      actions: Array<ActionValue>,  }
class BlockHeader {      height: u64,      prevHeight: u64,// Always zero when version < V3      epochId: Bytes,      nextEpochId: Bytes,      chunksIncluded: u64,      hash: Bytes,      prevHash: Bytes,      timestampNanosec: u64,      randomValue: Bytes,      gasPrice: BigInt,      totalSupply: BigInt,      latestProtocolVersion: u32,  }
class ChunkHeader {      gasUsed: u64,      gasLimit: u64,      shardId: u64,      chunkHash: Bytes,      prevBlockHash: Bytes,      balanceBurnt: BigInt,  }
class Block {      author: string,      header: BlockHeader,      chunks: Array<ChunkHeader>,  }
class ReceiptWithOutcome {      outcome: ExecutionOutcome,      receipt: ActionReceipt,      block: Block,  }
```

These types are passed to block & receipt handlers:

* Block handlers will receive a `Block`
* Receipt handlers will receive a `ReceiptWithOutcome`

Otherwise, the rest of the [AssemblyScript API](https://thegraph.com/docs/en/developer/assemblyscript-api/) is available to NEAR subgraph developers during mapping execution.

This includes a new JSON parsing function - logs on NEAR are frequently emitted as stringified JSONs. A new `json.fromString(...)` function is available as part of the [JSON API](https://thegraph.com/docs/en/developer/assemblyscript-api/#json-api) to allow developers to easily process these logs.

### Deploying a NEAR Subgraph <a href="#deploying-a-near-subgraph" id="deploying-a-near-subgraph"></a>

Once you have a built subgraph, it is time to deploy it to Graph Node for indexing. NEAR subgraphs can be deployed to any Graph Node `>=v0.26.x` (this version has not yet been tagged & released).

The Graph's Hosted Service currently supports indexing NEAR mainnet and testnet in beta, with the following network names:

* `near-mainnet`
* `near-testnet`

More information on creating and deploying subgraphs on the Hosted Service can be found [here](https://thegraph.com/docs/en/hosted-service/deploy-subgraph-hosted/).

As a quick primer - the first step is to "create" your subgraph - this only needs to be done once. On the Hosted Service, this can be done from [your Dashboard](https://thegraph.com/hosted-service/dashboard): "Add Subgraph".

Once your subgraph has been created, you can deploy your subgraph by using the `graph deploy` CLI command:

```
$ graph create --node <graph-node-url> subgraph/name # creates a subgraph on a local Graph Node (on the Hosted Service, this is done via the UI)$ graph deploy --node <graph-node-url> --ipfs https://api.thegraph.com/ipfs/ # uploads the build files to a specified IPFS endpoint, and then deploys the subgraph to a specified Graph Node based on the manifest IPFS hash
```

The node configuration will depend on where the subgraph is being deployed.

**Hosted Service:**

```
graph deploy --node https://api.thegraph.com/deploy/ --ipfs https://api.thegraph.com/ipfs/ --access-token <your-access-token>
```

**Local Graph Node (based on default configuration):**

```
graph deploy --node http://localhost:8020/ --ipfs http://localhost:5001
```

Once your subgraph has been deployed, it will be indexed by Graph Node. You can check its progress by querying the subgraph itself:

```
{  _meta {    block { number }  }}
```

#### Indexing NEAR with a Local Graph Node <a href="#indexing-near-with-a-local-graph-node" id="indexing-near-with-a-local-graph-node"></a>

Running a Graph Node that indexes NEAR has the following operational requirements:

* NEAR Indexer Framework with Firehose instrumentation
* NEAR Firehose Component(s)
* Graph Node with Firehose endpoint configured

We will provide more information on running the above components soon.

### Querying a NEAR Subgraph <a href="#querying-a-near-subgraph" id="querying-a-near-subgraph"></a>

The GraphQL endpoint for NEAR subgraphs is determined by the schema definition, with the existing API interface. Please visit the [GraphQL API documentation](https://thegraph.com/docs/en/developer/graphql-api/) for more information.

### Example Subgraphs <a href="#example-subgraphs" id="example-subgraphs"></a>

Here are some example subgraphs for reference:

[NEAR Blocks](https://github.com/graphprotocol/example-subgraph/tree/near-blocks-example)

[NEAR Receipts](https://github.com/graphprotocol/example-subgraph/tree/near-receipts-example)

### FAQ <a href="#faq" id="faq"></a>

#### How does the beta work? <a href="#how-does-the-beta-work" id="how-does-the-beta-work"></a>

NEAR support is in beta, which means that there may be changes to the API as we continue to work on improving the integration. Please email [near@thegraph.com](mailto:near@thegraph.com) so that we can support you in building NEAR subgraphs, and keep you up to date on the latest developments!

#### Can a subgraph index both NEAR and EVM chains? <a href="#can-a-subgraph-index-both-near-and-evm-chains" id="can-a-subgraph-index-both-near-and-evm-chains"></a>

No, a subgraph can only support data sources from one chain/network.

#### Can subgraphs react to more specific triggers? <a href="#can-subgraphs-react-to-more-specific-triggers" id="can-subgraphs-react-to-more-specific-triggers"></a>

Currently, only Block and Receipt triggers are supported. We are investigating triggers for function calls to a specified account. We are also interested in supporting event triggers, once NEAR has native event support.

#### Will receipt handlers trigger for accounts and their sub-accounts? <a href="#will-receipt-handlers-trigger-for-accounts-and-their-sub-accounts" id="will-receipt-handlers-trigger-for-accounts-and-their-sub-accounts"></a>

Receipt handlers will only be triggered for the exact match of the named account. More flexibility may be added in the future.

#### Can NEAR subgraphs make view calls to NEAR accounts during mappings? <a href="#can-near-subgraphs-make-view-calls-to-near-accounts-during-mappings" id="can-near-subgraphs-make-view-calls-to-near-accounts-during-mappings"></a>

This is not supported. We are evaluating whether this functionality is required for indexing.

#### Can I use data source templates in my NEAR subgraph? <a href="#can-i-use-data-source-templates-in-my-near-subgraph" id="can-i-use-data-source-templates-in-my-near-subgraph"></a>

This is not currently supported. We are evaluating whether this functionality is required for indexing.

#### Ethereum subgraphs support "pending" and "current" versions, how can I deploy a "pending" version of a NEAR subgraph? <a href="#ethereum-subgraphs-support-pending-and-current-versions-how-can-i-deploy-a-pending-version-of-a-near" id="ethereum-subgraphs-support-pending-and-current-versions-how-can-i-deploy-a-pending-version-of-a-near"></a>

Pending functionality is not yet supported for NEAR subgraphs. In the interim, you can deploy a new version to a different "named" subgraph, and then when that is synced with the chain head, you can redeploy to your primary "named" subgraph, which will use the same underlying deployment ID, so the main subgraph will be instantly synced.

#### My question hasn't been answered, where can I get more help building NEAR subgraphs? <a href="#my-question-hasn-t-been-answered-where-can-i-get-more-help-building-near-subgraphs" id="my-question-hasn-t-been-answered-where-can-i-get-more-help-building-near-subgraphs"></a>

If it is a general question about subgraph development, there is a lot more information in the rest of the [Developer documentation](https://thegraph.com/docs/en/developer/quick-start/). Otherwise please join [The Graph Protocol Discord](https://discord.gg/vtvv7FP) and ask in the #near channel or email [near@thegraph.com](mailto:near@thegraph.com).

### References <a href="#references" id="references"></a>

* [NEAR developer documentation](https://docs.near.org/docs/develop/basics/getting-started)

\
