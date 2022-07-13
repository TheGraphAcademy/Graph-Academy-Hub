---
description: Frequently asked questions about The Graph
---

# FAQs

**This is an extensive list of frequently asked questions about The Graph ecosystem**. This community FAQ will be updated with the latest questions. Please be sure to check the [official documentation](https://thegraph.com/docs/) by The Graph team, the [Official Network FAQ](https://docs.google.com/document/d/1h48y\_hQWb3CXbwHytsP3Hli1fNMqaMsiaoJd1x31HCQ/edit?usp=sharing) and this document before posting in the official channels. This helps the team to focus on the development of the Web3 protocol. Feel free to submit questions in the comment section, they will be answered and added to this article. _Please note that this is not an official FAQ by the team but all answers are confirmed from public responses by the team._

![](.gitbook/assets/1\_euxcu\_zmwl89ls6\_lnf05q.jpeg)

## Delegator FAQs and Bugs <a href="#delegator-fa-qs-and-bugs" id="delegator-fa-qs-and-bugs"></a>

#### MetaMask "Pending Transaction" Bug <a href="#meta-mask-pending-transaction-bug" id="meta-mask-pending-transaction-bug"></a>

**When I try to delegate my transaction in MetaMask appears as "Pending" or "Queued" for longer than expected. What should I do?**

At times, attempts to delegate to indexers via MetaMask can fail and result in prolonged periods of "Pending" or "Queued" transaction attempts. For example, a user may attempt to delegate with an insufficient gas fee relative to the current prices, resulting in the transaction attempt displaying as "Pending" in their MetaMask wallet for 15+ minutes. When this occurs, subsequent transactions can be attempted by a user, but these will not be processed until the initial transaction is mined, as transactions for an address must be processed in order. In such cases, these transactions can be cancelled in MetaMask, but the transactions attempts will accrue gas fees without any guarantee that subsequent attempts will be successful. A simpler resolution to this bug is restarting the browsesr (e.g., using "abort:restart" in the address bar), which will cancel all previous attempts without gas being subtracted from the wallet. Several users that have encountered this issue and have reported successful transactions after restarting their browser and attempting to delegate.

#### Video guide for the network UI <a href="#video-guide-for-the-network-ui" id="video-guide-for-the-network-ui"></a>

This guide provides a full review of this document, and how to consider everything in this document while interacting with the UI.

{% embed url="https://youtu.be/2G7S2gdURdc" %}

## Curation FAQs <a href="#curation-fa-qs" id="curation-fa-qs"></a>

#### 1. What % of query fees do Curators earn? <a href="#1-what-of-query-fees-do-curators-earn" id="1-what-of-query-fees-do-curators-earn"></a>

By signalling on a subgraph, you will earn a share of all the query fees that this subgraph generates. 10% of all query fees goes to the Curators pro-rata to their curation shares. This 10% is subject to governance.

#### 2. How do I decide which subgraphs are high quality to signal on? <a href="#2-how-do-i-decide-which-subgraphs-are-high-quality-to-signal-on" id="2-how-do-i-decide-which-subgraphs-are-high-quality-to-signal-on"></a>

Finding high-quality subgraphs is a complex task, but it can be approached in many different ways. As a Curator, you want to look for trustworthy subgraphs that are driving query volume. A trustworthy subgraph may be valuable if it is complete, accurate, and supports a dApp’s data needs. A poorly architected subgraph might need to be revised or re-published, and can also end up failing. It is critical for Curators to review a subgraph’s architecture or code in order to assess if a subgraph is valuable. As a result:

* Curators can use their understanding of a network to try and predict how an individual subgraph may generate a higher or lower query volume in the future
* Curators should also understand the metrics that are available through The Graph Explorer. Metrics like past query volume and who the subgraph developer is can help determine whether or not a subgraph is worth signalling on.

#### 3. What’s the cost of upgrading a subgraph? <a href="#3-what-s-the-cost-of-upgrading-a-subgraph" id="3-what-s-the-cost-of-upgrading-a-subgraph"></a>

Migrating your curation shares to a new subgraph version incurs a curation tax of 1%. Curators can choose to subscribe to the newest version of a subgraph. When curator shares get auto-migrated to a new version, Curators will also pay half curation tax, ie. 0.5%, because upgrading subgraphs is an on-chain action that costs gas.

#### 4. How often can I upgrade my subgraph? <a href="#4-how-often-can-i-upgrade-my-subgraph" id="4-how-often-can-i-upgrade-my-subgraph"></a>

It’s suggested that you don’t upgrade your subgraphs too frequently. See the question above for more details.

#### 5. Can I sell my curation shares? <a href="#5-can-i-sell-my-curation-shares" id="5-can-i-sell-my-curation-shares"></a>

Curation shares cannot be "bought" or "sold" like other ERC20 tokens that you may be familiar with. They can only be minted (created) or burned (destroyed) along the bonding curve for a particular subgraph. The amount of GRT needed to mint a new signal, and the amount of GRT you receive when you burn your existing signal are determined by that bonding curve. As a Curator, you need to know that when you burn your curation shares to withdraw GRT, you can end up with more or less GRT than you initially deposited.

Still confused? Check out our Curation video guide below:

{% embed url="https://youtu.be/VytTEcf0dxQ" %}

## Indexer FAQ <a href="#faq" id="faq"></a>

#### What is the minimum stake required to be an indexer on the network? <a href="#what-is-the-minimum-stake-required-to-be-an-indexer-on-the-network" id="what-is-the-minimum-stake-required-to-be-an-indexer-on-the-network"></a>

The minimum stake for an indexer is currently set to 100K GRT.

#### What are the revenue streams for an indexer? <a href="#what-are-the-revenue-streams-for-an-indexer" id="what-are-the-revenue-streams-for-an-indexer"></a>

**Query fee rebates** - Payments for serving queries on the network. These payments are mediated via state channels between an indexer and a gateway. Each query request from a gateway contains a payment and the corresponding response a proof of query result validity.

**Indexing rewards** - Generated via a 3% annual protocol wide inflation, the indexing rewards are distributed to indexers who are indexing subgraph deployments for the network.

#### How are rewards distributed? <a href="#how-are-rewards-distributed" id="how-are-rewards-distributed"></a>

Indexing rewards come from protocol inflation which is set to 3% annual issuance. They are distributed across subgraphs based on the proportion of all curation signal on each, then distributed proportionally to indexers based on their allocated stake on that subgraph. **An allocation must be closed with a valid proof of indexing (POI) that meets the standards set by the arbitration charter in order to be eligible for rewards.**

Numerous tools have been created by the community for calculating rewards; you'll find a collection of them organized in the [Community Guides collection](https://www.notion.so/Community-Guides-abbb10f4dba040d5ba81648ca093e70c). You can also find an up to date list of tools in the #delegators and #indexers channels on the [Discord server](https://discord.gg/vtvv7FP).

#### What is a proof of indexing (POI)? <a href="#what-is-a-proof-of-indexing-poi" id="what-is-a-proof-of-indexing-poi"></a>

POIs are used in the network to verify that an indexer is indexing the subgraphs they have allocated on. A POI for the first block of the current epoch must be submitted when closing an allocation for that allocation to be eligible for indexing rewards. A POI for a block is a digest for all entity store transactions for a specific subgraph deployment up to and including that block.

#### When are indexing rewards distributed? <a href="#when-are-indexing-rewards-distributed" id="when-are-indexing-rewards-distributed"></a>

Allocations are continuously accruing rewards while they're active. Rewards are collected by the indexers, and distributed whenever their allocations are closed. That happens either manually, whenever the indexer wants to force close them, or after 28 epochs a delegator can close the allocation for the indexer, but this results in no rewards being minted. 28 epochs is the max allocation lifetime (right now, one epoch lasts for \~24h).

#### Can pending indexer rewards be monitored? <a href="#can-pending-indexer-rewards-be-monitored" id="can-pending-indexer-rewards-be-monitored"></a>

The RewardsManager contract has a read-only [getRewards](https://github.com/graphprotocol/contracts/blob/master/contracts/rewards/RewardsManager.sol#L317) function that can be used to check the pending rewards for a specific allocation.

Many of the community-made dashboards include pending rewards values and they can be easily checked manually by following these steps:

1. Query the [mainnet subgraph](https://thegraph.com/hosted-service/subgraph/graphprotocol/graph-network-mainnet) to get the IDs for all active allocations:

```
query indexerAllocations {  indexer(id: "<INDEXER_ADDRESS>") {    allocations {      activeForIndexer {        allocations {          id        }      }    }  }}
```

Use Etherscan to call `getRewards()`:

* Navigate to [Etherscan interface to Rewards contract](https://etherscan.io/address/0x9Ac758AB77733b4150A901ebd659cbF8cB93ED66#readProxyContract)
* To call `getRewards()`:
  * Expand the **10. getRewards** dropdown.
  * Enter the **allocationID** in the input.
  * Click the **Query** button.

#### What are disputes and where can I view them? <a href="#what-are-disputes-and-where-can-i-view-them" id="what-are-disputes-and-where-can-i-view-them"></a>

Indexer's queries and allocations can both be disputed on The Graph during the dispute period. The dispute period varies, depending on the type of dispute. Queries/attestations have 7 epochs dispute window, whereas allocations have 56 epochs. After these periods pass, disputes cannot be opened against either of allocations or queries. When a dispute is opened, a deposit of a minimum of 10,000 GRT is required by the Fishermen, which will be locked until the dispute is finalized and a resolution has been given. Fisherman are any network participants that open disputes.

Disputes have **three** possible outcomes, so does the deposit of the Fishermen.

* If the dispute is rejected, the GRT deposited by the Fishermen will be burned, and the disputed Indexer will not be slashed.
* If the dispute is settled as a draw, the Fishermen's deposit will be returned, and the disputed Indexer will not be slashed.
* If the dispute is accepted, the GRT deposited by the Fishermen will be returned, the disputed Indexer will be slashed and the Fishermen will earn 50% of the slashed GRT.

Disputes can be viewed in the UI in an Indexer's profile page under the `Disputes` tab.

#### What are query fee rebates and when are they distributed? <a href="#what-are-query-fee-rebates-and-when-are-they-distributed" id="what-are-query-fee-rebates-and-when-are-they-distributed"></a>

Query fees are collected by the gateway whenever an allocation is closed and accumulated in the subgraph's query fee rebate pool. The rebate pool is designed to encourage Indexers to allocate stake in rough proportion to the amount of query fees they earn for the network. The portion of query fees in the pool that are allocated to a particular indexer is calculated using the Cobbs-Douglas Production Function; the distributed amount per indexer is a function of their contributions to the pool and their allocation of stake on the subgraph.

Once an allocation has been closed and the dispute period has passed the rebates are available to be claimed by the indexer. Upon claiming, the query fee rebates are distributed to the indexer and their delegators based on the query fee cut and the delegation pool proportions.

#### What is query fee cut and indexing reward cut? <a href="#what-is-query-fee-cut-and-indexing-reward-cut" id="what-is-query-fee-cut-and-indexing-reward-cut"></a>

The `queryFeeCut` and `indexingRewardCut` values are delegation parameters that the Indexer may set along with cooldownBlocks to control the distribution of GRT between the indexer and their delegators. See the last steps in [Staking in the Protocol](https://thegraph.com/docs/en/indexing/#stake-in-the-protocol) for instructions on setting the delegation parameters.

* **queryFeeCut** - the % of query fee rebates accumulated on a subgraph that will be distributed to the indexer. If this is set to 95%, the indexer will receive 95% of the query fee rebate pool when an allocation is claimed with the other 5% going to the delegators.
* **indexingRewardCut** - the % of indexing rewards accumulated on a subgraph that will be distributed to the indexer. If this is set to 95%, the indexer will receive 95% of the indexing rewards pool when an allocation is closed and the delegators will split the other 5%.

#### How do indexers know which subgraphs to index? <a href="#how-do-indexers-know-which-subgraphs-to-index" id="how-do-indexers-know-which-subgraphs-to-index"></a>

Indexers may differentiate themselves by applying advanced techniques for making subgraph indexing decisions but to give a general idea we'll discuss several key metrics used to evaluate subgraphs in the network:

* **Curation signal** - The proportion of network curation signal applied to a particular subgraph is a good indicator of the interest in that subgraph, especially during the bootstrap phase when query voluming is ramping up.
* **Query fees collected** - The historical data for volume of query fees collected for a specific subgraph is a good indicator of future demand.
* **Amount staked** - Monitoring the behavior of other indexers or looking at proportions of total stake allocated towards specific subgraphs can allow an indexer to monitor the supply side for subgraph queries to identify subgraphs that the network is showing confidence in or subgraphs that may show a need for more supply.
* **Subgraphs with no indexing rewards** - Some subgraphs do not generate indexing rewards mainly because they are using unsupported features like IPFS or because they are querying another network outside of mainnet. You will see a message on a subgraph if it is not generating indexing rewards.

#### What are the hardware requirements? <a href="#what-are-the-hardware-requirements" id="what-are-the-hardware-requirements"></a>

* **Small** - Enough to get started indexing several subgraphs, will likely need to be expanded.
* **Standard** - Default setup, this is what is used in the example k8s/terraform deployment manifests.
* **Medium** - Production indexer supporting 100 subgraphs and 200-500 requests per second.
* **Large** - Prepared to index all currently used subgraphs and serve requests for the related traffic.

| Setup    | <p>Postgres<br>(CPUs)</p> | <p>Postgres<br>(memory in GBs)</p> | <p>Postgres<br>(disk in TBs)</p> | <p>VMs<br>(CPUs)</p> | <p>VMs<br>(memory in GBs)</p> |
| -------- | :-----------------------: | :--------------------------------: | :------------------------------: | :------------------: | :---------------------------: |
| Small    |             4             |                  8                 |                 1                |           4          |               16              |
| Standard |             8             |                 30                 |                 1                |          12          |               48              |
| Medium   |             16            |                 64                 |                 2                |          32          |               64              |
| Large    |             72            |                 468                |                3.5               |          48          |              184              |

#### What are some basic security precautions an indexer should take? <a href="#what-are-some-basic-security-precautions-an-indexer-should-take" id="what-are-some-basic-security-precautions-an-indexer-should-take"></a>

* **Operator wallet** - Setting up an operator wallet is an important precaution because it allows an indexer to maintain separation between their keys that control stake and those that are in control of day-to-day operations. See [Stake in Protocol](https://thegraph.com/docs/en/indexing/#stake-in-the-protocol) for instructions.
* **Firewall** - Only the indexer service needs to be exposed publicly and particular attention should be paid to locking down admin ports and database access: the Graph Node JSON-RPC endpoint (default port: 8030), the indexer management API endpoint (default port: 18000), and the Postgres database endpoint (default port: 5432) should not be exposed.

#### Indexer Infrastructure <a href="#infrastructure" id="infrastructure"></a>

At the center of an indexer's infrastructure is the Graph Node which monitors Ethereum, extracts and loads data per a subgraph definition and serves it as a [GraphQL API](https://thegraph.com/docs/en/about/introduction/#how-the-graph-works). The Graph Node needs to be connected to Ethereum EVM node endpoints, and IPFS node for sourcing data; a PostgreSQL database for its store; and indexer components which facilitate its interactions with the network.

* **PostgreSQL database** - The main store for the Graph Node, this is where subgraph data is stored. The indexer service and agent also use the database to store state channel data, cost models, and indexing rules.
* **Ethereum endpoint** - An endpoint that exposes an Ethereum JSON-RPC API. This may take the form of a single Ethereum client or it could be a more complex setup that load balances across multiple. It's important to be aware that certain subgraphs will require particular Ethereum client capabilities such as archive mode and the tracing API.
* **IPFS node (version less than 5)** - Subgraph deployment metadata is stored on the IPFS network. The Graph Node primarily accesses the IPFS node during subgraph deployment to fetch the subgraph manifest and all linked files. Network indexers do not need to host their own IPFS node, an IPFS node for the network is hosted at [https://ipfs.network.thegraph.com](https://ipfs.network.thegraph.com/).
* **Indexer service** - Handles all required external communications with the network. Shares cost models and indexing statuses, passes query requests from gateways on to a Graph Node, and manages the query payments via state channels with the gateway.
* **Indexer agent** - Facilitates the indexers interactions on chain including registering on the network, managing subgraph deployments to its Graph Node/s, and managing allocations.
* **Prometheus metrics server** - The Graph Node and Indexer components log their metrics to the metrics server.

Note: To support agile scaling, it is recommended that query and indexing concerns are separated between different sets of nodes: query nodes and index nodes.

#### Ports overview <a href="#ports-overview" id="ports-overview"></a>

> **Important**: Be careful about exposing ports publicly - **administration ports** should be kept locked down. This includes the the Graph Node JSON-RPC and the indexer management endpoints detailed below.

**Graph Node**

| Port | Purpose                                              | Routes                                              | CLI Argument      | Environment Variable |
| ---- | ---------------------------------------------------- | --------------------------------------------------- | ----------------- | -------------------- |
| 8000 | <p>GraphQL HTTP server<br>(for subgraph queries)</p> | <p>/subgraphs/id/...<br>/subgraphs/name/.../...</p> | --http-port       | -                    |
| 8001 | <p>GraphQL WS<br>(for subgraph subscriptions)</p>    | <p>/subgraphs/id/...<br>/subgraphs/name/.../...</p> | --ws-port         | -                    |
| 8020 | <p>JSON-RPC<br>(for managing deployments)</p>        | /                                                   | --admin-port      | -                    |
| 8030 | Subgraph indexing status API                         | /graphql                                            | --index-node-port | -                    |
| 8040 | Prometheus metrics                                   | /metrics                                            | --metrics-port    | -                    |

**Indexer Service**

| Port | Purpose                                                   | Routes                                                         | CLI Argument   | Environment Variable   |
| ---- | --------------------------------------------------------- | -------------------------------------------------------------- | -------------- | ---------------------- |
| 7600 | <p>GraphQL HTTP server<br>(for paid subgraph queries)</p> | <p>/subgraphs/id/...<br>/status<br>/channel-messages-inbox</p> | --port         | `INDEXER_SERVICE_PORT` |
| 7300 | Prometheus metrics                                        | /metrics                                                       | --metrics-port | -                      |

**Indexer Agent**

| Port | Purpose                | Routes | CLI Argument              | Environment Variable                    |
| ---- | ---------------------- | ------ | ------------------------- | --------------------------------------- |
| 8000 | Indexer management API | /      | --indexer-management-port | `INDEXER_AGENT_INDEXER_MANAGEMENT_PORT` |

#### Setup server infrastructure using Terraform on Google Cloud <a href="#setup-server-infrastructure-using-terraform-on-google-cloud" id="setup-server-infrastructure-using-terraform-on-google-cloud"></a>

**Install prerequisites**

* Google Cloud SDK
* Kubectl command line tool
* Terraform

**Create a Google Cloud Project**

* Clone or navigate to the indexer repository.
* Navigate to the ./terraform directory, this is where all commands should be executed.

```
cd terraform
```

* Authenticate with Google Cloud and create a new project.

```
gcloud auth loginproject=<PROJECT_NAME>gcloud projects create --enable-cloud-apis $project
```

* Use the Google Cloud Console's billing page to enable billing for the new project.
* Create a Google Cloud configuration.

```
proj_id=$(gcloud projects list --format='get(project_id)' --filter="name=$project")gcloud config configurations create $projectgcloud config set project "$proj_id"gcloud config set compute/region us-central1gcloud config set compute/zone us-central1-a
```

* Enable required Google Cloud APIs.

```
gcloud services enable compute.googleapis.comgcloud services enable container.googleapis.comgcloud services enable servicenetworking.googleapis.comgcloud services enable sqladmin.googleapis.com
```

* Create a service account.

```
svc_name=<SERVICE_ACCOUNT_NAME>gcloud iam service-accounts create $svc_name \  --description="Service account for Terraform" \  --display-name="$svc_name"gcloud iam service-accounts list# Get the email of the service account from the listsvc=$(gcloud iam service-accounts list --format='get(email)'--filter="displayName=$svc_name")gcloud iam service-accounts keys create .gcloud-credentials.json \  --iam-account="$svc"gcloud projects add-iam-policy-binding $proj_id \  --member serviceAccount:$svc \  --role roles/editor
```

* Enable peering between database and Kubernetes cluster that will be created in the next step.

```
gcloud compute addresses create google-managed-services-default \  --prefix-length=20 \  --purpose=VPC_PEERING \  --network default \  --global \  --description 'IP Range for peer networks.'gcloud services vpc-peerings connect \  --network=default \  --ranges=google-managed-services-default
```

* Create minimal terraform configuration file (update as needed).

```
indexer=<INDEXER_NAME>cat > terraform.tfvars <<EOFproject = "$proj_id"indexer = "$indexer"database_password = "<database passowrd>"EOF
```

**Use Terraform to create infrastructure**

Before running any commands, read through [variables.tf](https://github.com/graphprotocol/indexer/blob/main/terraform/variables.tf) and create a file `terraform.tfvars` in this directory (or modify the one we created in the last step). For each variable where you want to override the default, or where you need to set a value, enter a setting into `terraform.tfvars`.

* Run the following commands to create the infrastructure.

```
# Install required pluginsterraform init
# View plan for resources to be createdterraform plan
# Create the resources (expect it to take up to 30 minutes)terraform apply
```

Download credentials for the new cluster into `~/.kube/config` and set it as your default context.

```
gcloud container clusters get-credentials $indexerkubectl config use-context $(kubectl config get-contexts --output='name'| grep $indexer)
```

**Creating the Kubernetes components for the indexer**

* Copy the directory `k8s/overlays` to a new directory `$dir,` and adjust the `bases` entry in `$dir/kustomization.yaml` so that it points to the directory `k8s/base`.
* Read through all the files in `$dir` and adjust any values as indicated in the comments.

Deploy all resources with `kubectl apply -k $dir`.

#### Graph Node <a href="#graph-node-2" id="graph-node-2"></a>

[Graph Node](https://github.com/graphprotocol/graph-node) is an open source Rust implementation that event sources the Ethereum blockchain to deterministically update a data store that can be queried via the GraphQL endpoint. Developers use subgraphs to define their schema, and a set of mappings for transforming the data sourced from the block chain and the Graph Node handles syncing the entire chain, monitoring for new blocks, and serving it via a GraphQL endpoint.

**Getting started from source**

**Install prerequisites**

* **Rust**
* **PostgreSQL**
* **IPFS**
* **Additional Requirements for Ubuntu users** - To run a Graph Node on Ubuntu a few additional packages may be needed.

```
sudo apt-get install -y clang libpg-dev libssl-dev pkg-config
```

**Setup**

1. Start a PostgreSQL database server

```
initdb -D .postgrespg_ctl -D .postgres -l logfile startcreatedb graph-node
```

1. Clone [Graph Node](https://github.com/graphprotocol/graph-node) repo and build the source by running `cargo build`
2. Now that all the dependencies are setup, start the Graph Node:

```
cargo run -p graph-node --release -- \  --postgres-url postgresql://[USERNAME]:[PASSWORD]@localhost:5432/graph-node \  --ethereum-rpc [NETWORK_NAME]:[URL] \  --ipfs https://ipfs.network.thegraph.com
```

**Getting started using Docker**

**Prerequisites**

* **Ethereum node** - By default, the docker compose setup will use mainnet: [http://host.docker.internal:8545](http://host.docker.internal:8545/) to connect to the Ethereum node on your host machine. You can replace this network name and url by updating `docker-compose.yaml`.

**Setup**

1. Clone Graph Node and navigate to the Docker directory:

```
git clone http://github.com/graphprotocol/graph-nodecd graph-node/docker
```

1. For linux users only - Use the host IP address instead of `host.docker.internal` in the `docker-compose.yaml` using the included script:

```
./setup.sh
```

1. Start a local Graph Node that will connect to your Ethereum endpoint:

```
docker-compose up
```

#### Indexer components <a href="#indexer-components" id="indexer-components"></a>

To successfully participate in the network requires almost constant monitoring and interaction, so we've built a suite of Typescript applications for facilitating an Indexers network participation. There are three indexer components:

* **Indexer agent** - The agent monitors the network and the indexer's own infrastructure and manages which subgraph deployments are indexed and allocated towards on chain and how much is allocated towards each.
* **Indexer service** - The only component that needs to be exposed externally, the service passes on subgraph queries to the graph node, manages state channels for query payments, shares important decision making information to clients like the gateways.
* **Indexer CLI** - The command line interface for managing the indexer agent. It allows indexers to manage cost models and indexing rules.

**Getting started**

The indexer agent and indexer service should be co-located with your Graph Node infrastructure. There are many ways to setup virtual execution environments for you indexer components; here we'll explain how to run them on baremetal using NPM packages or source, or via kubernetes and docker on the Google Cloud Kubernetes Engine. If these setup examples do not translate well to your infrastructure there will likely be a community guide to reference, come say hi on [Discord](https://thegraph.com/discord)! Remember to [stake in the protocol](https://thegraph.com/docs/en/indexing/#stake-in-the-protocol) before starting up your indexer components!

**From NPM packages**

```
npm install -g @graphprotocol/indexer-servicenpm install -g @graphprotocol/indexer-agent
# Indexer CLI is a plugin for Graph CLI, so both need to be installed:npm install -g @graphprotocol/graph-clinpm install -g @graphprotocol/indexer-cli
# Indexer servicegraph-indexer-service start ...
# Indexer agentgraph-indexer-agent start ...
# Indexer CLI#Forward the port of your agent pod if using Kuberneteskubectl port-forward pod/POD_ID 18000:8000graph indexer connect http://localhost:18000/graph indexer ...
```

**From source**

```
# From Repo root directoryyarn
# Indexer Servicecd packages/indexer-service./bin/graph-indexer-service start ...
# Indexer agentcd packages/indexer-agent./bin/graph-indexer-service start ...
# Indexer CLIcd packages/indexer-cli./bin/graph-indexer-cli indexer connect http://localhost:18000/./bin/graph-indexer-cli indexer ...
```

**Using docker**

* Pull images from the registry

```
docker pull ghcr.io/graphprotocol/indexer-service:latestdocker pull ghcr.io/graphprotocol/indexer-agent:latest
```

Or build images locally from source

```
# Indexer servicedocker build \  --build-arg NPM_TOKEN=<npm-token> \  -f Dockerfile.indexer-service \  -t indexer-service:latest \# Indexer agentdocker build \  --build-arg NPM_TOKEN=<npm-token> \  -f Dockerfile.indexer-agent \  -t indexer-agent:latest \
```

* Run the components

```
docker run -p 7600:7600 -it indexer-service:latest ...docker run -p 18000:8000 -it indexer-agent:latest ...
```

**NOTE**: After starting the containers, the indexer service should be accessible at [http://localhost:7600](http://localhost:7600/) and the indexer agent should be exposing the indexer management API at [http://localhost:18000/](http://localhost:18000/).

**Using K8s and Terraform**

See the [Setup Server Infrastructure Using Terraform on Google Cloud](https://thegraph.com/docs/en/indexing/#setup-server-infrastructure-using-terraform-on-google-cloud) section

**Usage**

> **NOTE**: All runtime configuration variables may be applied either as parameters to the command on startup or using environment variables of the format `COMPONENT_NAME_VARIABLE_NAME`(ex. `INDEXER_AGENT_ETHEREUM`).

**Indexer agent**

```
graph-indexer-agent start \  --ethereum <MAINNET_ETH_ENDPOINT> \  --ethereum-network mainnet \  --mnemonic <MNEMONIC> \  --indexer-address <INDEXER_ADDRESS> \  --graph-node-query-endpoint http://localhost:8000/ \  --graph-node-status-endpoint http://localhost:8030/graphql \  --graph-node-admin-endpoint http://localhost:8020/ \  --public-indexer-url http://localhost:7600/ \  --indexer-geo-coordinates <YOUR_COORDINATES> \  --index-node-ids default \  --indexer-management-port 18000 \  --metrics-port 7040 \  --network-subgraph-endpoint https://gateway.network.thegraph.com/network \  --default-allocation-amount 100 \  --register true \  --inject-dai true \  --postgres-host localhost \  --postgres-port 5432 \  --postgres-username <DB_USERNAME> \  --postgres-password <DB_PASSWORD> \  --postgres-database indexer \  | pino-pretty
```

**Indexer service**

```
SERVER_HOST=localhost \SERVER_PORT=5432 \SERVER_DB_NAME=is_staging \SERVER_DB_USER=<DB_USERNAME> \SERVER_DB_PASSWORD=<DB_PASSWORD> \graph-indexer-service start \  --ethereum <MAINNET_ETH_ENDPOINT> \  --ethereum-network mainnet \  --mnemonic <MNEMONIC> \  --indexer-address <INDEXER_ADDRESS> \  --port 7600 \  --metrics-port 7300 \  --graph-node-query-endpoint http://localhost:8000/ \  --graph-node-status-endpoint http://localhost:8030/graphql \  --postgres-host localhost \  --postgres-port 5432 \  --postgres-username <DB_USERNAME> \  --postgres-password <DB_PASSWORD> \  --postgres-database is_staging \  --network-subgraph-endpoint https://gateway.network.thegraph.com/network \  | pino-pretty
```

**Indexer CLI**

The Indexer CLI is a plugin for [`@graphprotocol/graph-cli`](https://www.npmjs.com/package/@graphprotocol/graph-cli) accessible in the terminal at `graph indexer`.

```
graph indexer connect http://localhost:18000graph indexer status
```

**Indexer management using indexer CLI**

The indexer agent needs input from an indexer in order to autonomously interact with the network on the behalf of the indexer. The mechanism for defining indexer agent behavior are the **indexing rules**. Using **indexing rules** an indexer can apply their specific strategy for picking subgraphs to index and serve queries for. Rules are managed via a GraphQL API served by the agent and known as the Indexer Management API. The suggested tool for interacting with the **Indexer Management API** is the **Indexer CLI**, an extension to the **Graph CLI**.

**Usage**

The **Indexer CLI** connects to the indexer agent, typically through port-forwarding, so the CLI does not need to run on the same server or cluster. To help you get started, and to provide some context, the CLI will briefly be described here.

* `graph indexer connect <url>` - Connect to the indexer management API. Typically the connection to the server is opened via port forwarding, so the CLI can be easily operated remotely. (Example: `kubectl port-forward pod/<indexer-agent-pod> 8000:8000`)
* `graph indexer rules get [options] <deployment-id< [<key1> ...]` - Get one or more indexing rules using `all` as the `<deployment-id>` to get all rules, or `global` to get the global defaults. An additional argument `--merged` can be used to specify that deployment specific rules are merged with the global rule. This is how they are applied in the indexer agent.
* `graph indexer rules set [options] <deployment-id> <key1> <value1> ...` - Set one or more indexing rules.
* `graph indexer rules start [options] <deployment-id>` - Start indexing a subgraph deployment if available and set its `decisionBasis` to `always`, so the indexer agent will always choose to index it. If the global rule is set to always then all available subgraphs on the network will be indexed.
* `graph indexer rules stop [options] <deployment-id>` - Stop indexing a deployment and set its `decisionBasis` to never, so it will skip this deployment when deciding on deployments to index.
* `graph indexer rules maybe [options] <deployment-id>` — Set `thedecisionBasis` for a deployment to `rules`, so that the indexer agent will use indexing rules to decide whether to index this deployment.

All commands which display rules in the output can choose between the supported output formats (`table`, `yaml`, and `json`) using the `-output` argument.

**Indexing rules**

Indexing rules can either be applied as global defaults or for specific subgraph deployments using their IDs. The `deployment` and `decisionBasis` fields are mandatory, while all other fields are optional. When an indexing rule has `rules` as the `decisionBasis`, then the indexer agent will compare non-null threshold values on that rule with values fetched from the network for the corresponding deployment. If the subgraph deployment has values above (or below) any of the thresholds it will be chosen for indexing.

For example, if the global rule has a `minStake` of **5** (GRT), any subgraph deployment which has more than 5 (GRT) of stake allocated to it will be indexed. Threshold rules include `maxAllocationPercentage`, `minSignal`, `maxSignal`, `minStake`, and `minAverageQueryFees`.

Data model:

```
type IndexingRule {  deployment: string  allocationAmount: string | null  parallelAllocations: number | null  decisionBasis: IndexingDecisionBasis  maxAllocationPercentage: number | null  minSignal: string | null  maxSignal: string | null  minStake: string | null  minAverageQueryFees: string | null  custom: string | null}
IndexingDecisionBasis {  rules  never  always}
```

**Cost models**

Cost models provide dynamic pricing for queries based on market and query attributes. The Indexer Service shares a cost model with the gateways for each subgraph for which they intend to respond to queries. The gateways, in turn, use the cost model to make indexer selection decisions per query and to negotiate payment with chosen indexers.

**Agora**

The Agora language provides a flexible format for declaring cost models for queries. An Agora price model is a sequence of statements that execute in order for each top-level query in a GraphQL query. For each top-level query, the first statement which matches it determines the price for that query.

A statement is comprised of a predicate, which is used for matching GraphQL queries, and a cost expression which when evaluated outputs a cost in decimal GRT. Values in the named argument position of a query may be captured in the predicate and used in the expression. Globals may also be set and substituted in for placeholders in an expression.

Example cost model:

```
# This statement captures the skip value,# uses a boolean expression in the predicate to match specific queries that use `skip`# and a cost expression to calculate the cost based on the `skip` value and the SYSTEM_LOAD globalquery { pairs(skip: $skip) { id } } when $skip > 2000 => 0.0001 * $skip * $SYSTEM_LOAD;
# This default will match any GraphQL expression.# It uses a Global substituted into the expression to calculate costdefault => 0.1 * $SYSTEM_LOAD;
```

Example query costing using the above model:

| Query                                          | Price   |
| ---------------------------------------------- | ------- |
| { pairs(skip: 5000) { id } }                   | 0.5 GRT |
| { tokens { symbol } \&#125                     | 0.1 GRT |
| { pairs(skip: 5000) { id { tokens } symbol } } | 0.6 GRT |

**Applying the cost model**

Cost models are applied via the Indexer CLI, which passes them to the Indexer Management API of the indexer agent for storing in the database. The Indexer Service will then pick them up and serve the cost models to gateways whenever they ask for them.

```
indexer cost set variables '{ "SYSTEM_LOAD": 1.4 }'indexer cost set model my_model.agora
```

#### **Interacting with the network** <a href="#interacting-with-the-network" id="interacting-with-the-network"></a>

#### Stake in the protocol <a href="#stake-in-the-protocol" id="stake-in-the-protocol"></a>

The first steps to participating in the network as an Indexer are to approve the protocol, stake funds, and (optionally) set up an operator address for day-to-day protocol interactions. \_ **Note**: For the purposes of these instructions Remix will be used for contract interaction, but feel free to use your tool of choice ([OneClickDapp](https://oneclickdapp.com/), [ABItopic](https://abitopic.io/), and [MyCrypto](https://www.mycrypto.com/account) are a few other known tools).\_

Once an indexer has staked GRT in the protocol, the [indexer components](https://thegraph.com/docs/en/indexing/#indexer-components) can be started up and begin their interactions with the network.

**Approve tokens**[**#Link to this section**](https://thegraph.com/docs/en/indexing/#approve-tokens)

1. Open the [Remix app](https://remix.ethereum.org/) in a browser
2. In the `File Explorer` create a file named **GraphToken.abi** with the [token ABI](https://raw.githubusercontent.com/graphprotocol/contracts/mainnet-deploy-build/build/abis/GraphToken.json).
3. With `GraphToken.abi` selected and open in the editor, switch to the Deploy and `Run Transactions` section in the Remix interface.
4. Under environment select `Injected Web3` and under `Account` select your indexer address.
5. Set the GraphToken contract address - Paste the GraphToken contract address (`0xc944E90C64B2c07662A292be6244BDf05Cda44a7`) next to `At Address` and click the `At address` button to apply.
6. Call the `approve(spender, amount)` function to approve the Staking contract. Fill in `spender` with the Staking contract address (`0xF55041E37E12cD407ad00CE2910B8269B01263b9`) and `amount` with the tokens to stake (in wei).

**Stake tokens**[**#Link to this section**](https://thegraph.com/docs/en/indexing/#stake-tokens)

1. Open the [Remix app](https://remix.ethereum.org/) in a browser
2. In the `File Explorer` create a file named **Staking.abi** with the staking ABI.
3. With `Staking.abi` selected and open in the editor, switch to the `Deploy` and `Run Transactions` section in the Remix interface.
4. Under environment select `Injected Web3` and under `Account` select your indexer address.
5. Set the Staking contract address - Paste the Staking contract address (`0xF55041E37E12cD407ad00CE2910B8269B01263b9`) next to `At Address` and click the `At address` button to apply.
6. Call `stake()` to stake GRT in the protocol.
7. (Optional) Indexers may approve another address to be the operator for their indexer infrastructure in order to separate the keys that control the funds from those that are performing day to day actions such as allocating on subgraphs and serving (paid) queries. In order to set the operator call `setOperator()` with the operator address.
8. (Optional) In order to control the distribution of rewards and strategically attract delegators indexers can update their delegation parameters by updating their indexingRewardCut (parts per million), queryFeeCut (parts per million), and cooldownBlocks (number of blocks). To do so call `setDelegationParameters()`. The following example sets the queryFeeCut to distribute 95% of query rebates to the indexer and 5% to delegators, set the indexingRewardCutto distribute 60% of indexing rewards to the indexer and 40% to delegators, and set `thecooldownBlocks` period to 500 blocks.

```
setDelegationParameters(950000, 600000, 500)
```

#### The life of an allocation[#Link to this section](https://thegraph.com/docs/en/indexing/#the-life-of-an-allocation) <a href="#the-life-of-an-allocation" id="the-life-of-an-allocation"></a>

After being created by an indexer a healthy allocation goes through four states.

* **Active** - Once an allocation is created on-chain ([allocateFrom()](https://github.com/graphprotocol/contracts/blob/master/contracts/staking/Staking.sol#L873)) it is considered **active**. A portion of the indexer's own and/or delegated stake is allocated towards a subgraph deployment, which allows them to claim indexing rewards and serve queries for that subgraph deployment. The indexer agent manages creating allocations based on the indexer rules.
* **Closed** - An indexer is free to close an allocation once 1 epoch has passed ([closeAllocation()](https://github.com/graphprotocol/contracts/blob/master/contracts/staking/Staking.sol#L873)) or their indexer agent will automatically close the allocation after the **maxAllocationEpochs** (currently 28 days). When an allocation is closed with a valid proof of indexing (POI) their indexing rewards are distributed to the indexer and its delegators (see "how are rewards distributed?" below to learn more).
* **Finalized** - Once an allocation has been closed there is a dispute period after which the allocation is considered **finalized** and it's query fee rebates are available to be claimed (claim()). The indexer agent monitors the network to detect **finalized** allocations and claims them if they are above a configurable (and optional) threshold, **—-allocation-claim-threshold**.
* **Claimed** - The final state of an allocation; it has run its course as an active allocation, all eligible rewards have been distributed and its query fee rebates have been claimed.



## Developer FAQs

#### 1. Can I delete my subgraph? <a href="#1-can-i-delete-my-subgraph" id="1-can-i-delete-my-subgraph"></a>

It is not possible to delete subgraphs once they are created.

#### 2. Can I change my subgraph name? <a href="#2-can-i-change-my-subgraph-name" id="2-can-i-change-my-subgraph-name"></a>

No. Once a subgraph is created, the name cannot be changed. Make sure to think of this carefully before you create your subgraph so it is easily searchable and identifiable by other dapps.

#### 3. Can I change the GitHub account associated with my subgraph? <a href="#3-can-i-change-the-git-hub-account-associated-with-my-subgraph" id="3-can-i-change-the-git-hub-account-associated-with-my-subgraph"></a>

No. Once a subgraph is created, the associated GitHub account cannot be changed. Make sure to think of this carefully before you create your subgraph.

#### 4. Am I still able to create a subgraph if my smart contracts don't have events? <a href="#4-am-i-still-able-to-create-a-subgraph-if-my-smart-contracts-don-t-have-events" id="4-am-i-still-able-to-create-a-subgraph-if-my-smart-contracts-don-t-have-events"></a>

It is highly recommended that you structure your smart contracts to have events associated with data you are interested in querying. Event handlers in the subgraph are triggered by contract events and are by far the fastest way to retrieve useful data.

If the contracts you are working with do not contain events, your subgraph can use call and block handlers to trigger indexing. Although this is not recommended, as performance will be significantly slower.

#### 5. Is it possible to deploy one subgraph with the same name for multiple networks? <a href="#5-is-it-possible-to-deploy-one-subgraph-with-the-same-name-for-multiple-networks" id="5-is-it-possible-to-deploy-one-subgraph-with-the-same-name-for-multiple-networks"></a>

You will need separate names for multiple networks. While you can't have different subgraphs under the same name, there are convenient ways of having a single codebase for multiple networks. Find more on this in our documentation: [Redeploying a Subgraph](https://thegraph.com/docs/en/hosted-service/deploy-subgraph-hosted/#redeploying-a-subgraph)

#### 6. How are templates different from data sources? <a href="#6-how-are-templates-different-from-data-sources" id="6-how-are-templates-different-from-data-sources"></a>

Templates allow you to create data sources on the fly, while your subgraph is indexing. It might be the case that your contract will spawn new contracts as people interact with it, and since you know the shape of those contracts (ABI, events, etc) upfront you can define how you want to index them in a template and when they are spawned your subgraph will create a dynamic data source by supplying the contract address.

Check out the "Instantiating a data source template" section on: [Data Source Templates](https://thegraph.com/docs/en/developer/create-subgraph-hosted/#data-source-templates).

#### 7. How do I make sure I'm using the latest version of graph-node for my local deployments? <a href="#7-how-do-i-make-sure-i-m-using-the-latest-version-of-graph-node-for-my-local-deployments" id="7-how-do-i-make-sure-i-m-using-the-latest-version-of-graph-node-for-my-local-deployments"></a>

You can run the following command:

```
docker pull graphprotocol/graph-node:latest
```

**NOTE:** docker / docker-compose will always use whatever graph-node version was pulled the first time you ran it, so it is important to do this to make sure you are up to date with the latest version of graph-node.

#### 8. How do I call a contract function or access a public state variable from my subgraph mappings? <a href="#8-how-do-i-call-a-contract-function-or-access-a-public-state-variable-from-my-subgraph-mappings" id="8-how-do-i-call-a-contract-function-or-access-a-public-state-variable-from-my-subgraph-mappings"></a>

Take a look at `Access to smart contract` state inside the section [AssemblyScript API](https://thegraph.com/docs/en/developer/assemblyscript-api/).

#### 9. Is it possible to set up a subgraph using `graph init` from `graph-cli` with two contracts? Or should I manually add another datasource in `subgraph.yaml` after running `graph init`? <a href="#9-is-it-possible-to-set-up-a-subgraph-using-from-with-two-contracts-or-should-i-manually-add-another" id="9-is-it-possible-to-set-up-a-subgraph-using-from-with-two-contracts-or-should-i-manually-add-another"></a>

Unfortunately, this is currently not possible. `graph init` is intended as a basic starting point, from which you can then add more data sources manually.

#### 10. I want to contribute or add a GitHub issue. Where can I find the open source repositories? <a href="#10-i-want-to-contribute-or-add-a-git-hub-issue-where-can-i-find-the-open-source-repositories" id="10-i-want-to-contribute-or-add-a-git-hub-issue-where-can-i-find-the-open-source-repositories"></a>

* [graph-node](https://github.com/graphprotocol/graph-node)
* [graph-cli](https://github.com/graphprotocol/graph-cli)
* [graph-ts](https://github.com/graphprotocol/graph-ts)

#### 11. What is the recommended way to build "autogenerated" ids for an entity when handling events? <a href="#11-what-is-the-recommended-way-to-build-autogenerated-ids-for-an-entity-when-handling-events" id="11-what-is-the-recommended-way-to-build-autogenerated-ids-for-an-entity-when-handling-events"></a>

If only one entity is created during the event and if there's nothing better available, then the transaction hash + log index would be unique. You can obfuscate these by converting that to Bytes and then piping it through `crypto.keccak256` but this won't make it more unique.

#### 12. When listening to multiple contracts, is it possible to select the contract order to listen to events? <a href="#12-when-listening-to-multiple-contracts-is-it-possible-to-select-the-contract-order-to-listen-to-eve" id="12-when-listening-to-multiple-contracts-is-it-possible-to-select-the-contract-order-to-listen-to-eve"></a>

Within a subgraph, the events are always processed in the order they appear in the blocks, regardless of whether that is across multiple contracts or not.

#### 13. Is it possible to differentiate between networks (mainnet, Kovan, Ropsten, local) from within event handlers? <a href="#13-is-it-possible-to-differentiate-between-networks-mainnet-kovan-ropsten-local-from-within-event-ha" id="13-is-it-possible-to-differentiate-between-networks-mainnet-kovan-ropsten-local-from-within-event-ha"></a>

Yes. You can do this by importing `graph-ts` as per the example below:

```
import { dataSource } from '@graphprotocol/graph-ts'
dataSource.network()dataSource.address()
```

#### 14. Do you support block and call handlers on Rinkeby? <a href="#14-do-you-support-block-and-call-handlers-on-rinkeby" id="14-do-you-support-block-and-call-handlers-on-rinkeby"></a>

On Rinkeby we support block handlers, but without `filter: call`. Call handlers are not supported for the time being.

#### 15. Can I import ethers.js or other JS libraries into my subgraph mappings? <a href="#15-can-i-import-ethers-js-or-other-js-libraries-into-my-subgraph-mappings" id="15-can-i-import-ethers-js-or-other-js-libraries-into-my-subgraph-mappings"></a>

Not currently, as mappings are written in AssemblyScript. One possible alternative solution to this is to store raw data in entities and perform logic that requires JS libraries on the client.

#### 16. Is it possible to specify what block to start indexing on? <a href="#16-is-it-possible-to-specify-what-block-to-start-indexing-on" id="16-is-it-possible-to-specify-what-block-to-start-indexing-on"></a>

Yes. `dataSources.source.startBlock` in the `subgraph.yaml` file specifies the number of the block that the data source starts indexing from. In most cases, we suggest using the block in which the contract was created: Start blocks

#### 17. Are there some tips to increase the performance of indexing? My subgraph is taking a very long time to sync. <a href="#17-are-there-some-tips-to-increase-the-performance-of-indexing-my-subgraph-is-taking-a-very-long-tim" id="17-are-there-some-tips-to-increase-the-performance-of-indexing-my-subgraph-is-taking-a-very-long-tim"></a>

Yes, you should take a look at the optional start block feature to start indexing from the block that the contract was deployed: [Start blocks](https://thegraph.com/docs/en/developer/create-subgraph-hosted/#start-blocks)

#### 18. Is there a way to query the subgraph directly to determine the latest block number it has indexed? <a href="#18-is-there-a-way-to-query-the-subgraph-directly-to-determine-the-latest-block-number-it-has-indexed" id="18-is-there-a-way-to-query-the-subgraph-directly-to-determine-the-latest-block-number-it-has-indexed"></a>

Yes! Try the following command, substituting "organization/subgraphName" with the organization under it is published and the name of your subgraph:

```
curl -X POST -d '{ "query": "{indexingStatusForCurrentVersion(subgraphName: \"organization/subgraphName\") { chains { latestBlock { hash number }}}}"}' https://api.thegraph.com/index-node/graphql
```

#### 19. What networks are supported by The Graph? <a href="#19-what-networks-are-supported-by-the-graph" id="19-what-networks-are-supported-by-the-graph"></a>

The graph-node supports any EVM-compatible JSON RPC API chain.

The Graph Network supports subgraphs indexing mainnet Ethereum:

* `mainnet`

In the Hosted Service, the following networks are supported:

* Ethereum mainnet
* Kovan
* Rinkeby
* Ropsten
* Goerli
* PoA-Core
* PoA-Sokol
* xDAI
* NEAR
* NEAR testnet
* Matic
* Mumbai
* Fantom
* Binance Smart Chain
* Clover
* Avalanche
* Fuji
* Celo
* Celo-Alfajores
* Fuse
* Moonbeam
* Arbitrum One
* Arbitrum Testnet (on Rinkeby)
* Optimism
* Optimism Testnet (on Kovan)

There is work in progress towards integrating other blockchains, you can read more in our repo: [RFC-0003: Multi-Blockchain Support](https://github.com/graphprotocol/rfcs/pull/8/files).

#### 20. Is it possible to duplicate a subgraph to another account or endpoint without redeploying? <a href="#20-is-it-possible-to-duplicate-a-subgraph-to-another-account-or-endpoint-without-redeploying" id="20-is-it-possible-to-duplicate-a-subgraph-to-another-account-or-endpoint-without-redeploying"></a>

You have to redeploy the subgraph, but if the subgraph ID (IPFS hash) doesn't change, it won't have to sync from the beginning.

#### 21. Is this possible to use Apollo Federation on top of graph-node? <a href="#21-is-this-possible-to-use-apollo-federation-on-top-of-graph-node" id="21-is-this-possible-to-use-apollo-federation-on-top-of-graph-node"></a>

Federation is not supported yet, although we do want to support it in the future. At the moment, something you can do is use schema stitching, either on the client or via a proxy service.

#### 22. Is there a limit to how many objects The Graph can return per query? <a href="#22-is-there-a-limit-to-how-many-objects-the-graph-can-return-per-query" id="22-is-there-a-limit-to-how-many-objects-the-graph-can-return-per-query"></a>

By default, query responses are limited to 100 items per collection. If you want to receive more, you can go up to 1000 items per collection and beyond that, you can paginate with:

```
someCollection(first: 1000, skip: <number>) { ... }
```

#### 23. If my dapp frontend uses The Graph for querying, do I need to write my query key into the frontend directly? What if we pay query fees for users – will malicious users cause our query fees to be very high? <a href="#23-if-my-dapp-frontend-uses-the-graph-for-querying-do-i-need-to-write-my-query-key-into-the-frontend" id="23-if-my-dapp-frontend-uses-the-graph-for-querying-do-i-need-to-write-my-query-key-into-the-frontend"></a>

Currently, the recommended approach for a dapp is to add the key to the frontend and expose it to end users. That said, you can limit that key to a hostname, like _yourdapp.io_ and subgraph. The gateway is currently being run by Edge & Node. Part of the responsibility of a gateway is to monitor for abusive behavior and block traffic from malicious clients.

#### 24. Where do I go to find my current subgraph on the Hosted Service? <a href="#24-where-do-i-go-to-find-my-current-subgraph-on-the-hosted-service" id="24-where-do-i-go-to-find-my-current-subgraph-on-the-hosted-service"></a>

Head over to the Hosted Service in order to find subgraphs that you or others deployed to the Hosted Service. You can find it [here.](https://thegraph.com/hosted-service)

#### 25. Will the Hosted Service start charging query fees? <a href="#25-will-the-hosted-service-start-charging-query-fees" id="25-will-the-hosted-service-start-charging-query-fees"></a>

The Graph will never charge for the Hosted Service. The Graph is a decentralized protocol, and charging for a centralized service is not aligned with The Graph’s values. The Hosted Service was always a temporary step to help get to the decentralized network. Developers will have a sufficient amount of time to migrate to the decentralized network as they are comfortable.

#### 26. When will the Hosted Service be shut down? <a href="#26-when-will-the-hosted-service-be-shut-down" id="26-when-will-the-hosted-service-be-shut-down"></a>

If and when there are plans to do this, the community will be notified well ahead of time with considerations made for any subgraphs built on the Hosted Service.

#### 27. How do I upgrade a subgraph on mainnet? <a href="#27-how-do-i-upgrade-a-subgraph-on-mainnet" id="27-how-do-i-upgrade-a-subgraph-on-mainnet"></a>

If you’re a subgraph developer, you can upgrade a new version of your subgraph to the Studio using the CLI. It’ll be private at that point, but if you’re happy with it, you can publish to the decentralized Graph Explorer. This will create a new version of your subgraph that Curators can start signaling on.



## Subgraph Studio FAQs

#### 1. How do I create an API Key?[#Link to this section](https://thegraph.com/docs/en/studio/studio-faq/#1-how-do-i-create-an-api-key) <a href="#1-how-do-i-create-an-api-key" id="1-how-do-i-create-an-api-key"></a>

In the Subgraph Studio, you can create API Keys as needed and add security settings to each of them.

#### 2. Can I create multiple API Keys?[#Link to this section](https://thegraph.com/docs/en/studio/studio-faq/#2-can-i-create-multiple-api-keys) <a href="#2-can-i-create-multiple-api-keys" id="2-can-i-create-multiple-api-keys"></a>

A: Yes! You can create multiple API Keys to use in different projects. Check out the link [here](https://thegraph.com/studio/apikeys/).

#### 3. How do I restrict a domain for an API Key?[#Link to this section](https://thegraph.com/docs/en/studio/studio-faq/#3-how-do-i-restrict-a-domain-for-an-api-key) <a href="#3-how-do-i-restrict-a-domain-for-an-api-key" id="3-how-do-i-restrict-a-domain-for-an-api-key"></a>

After creating an API Key, in the Security section, you can define the domains that can query a specific API Key.

#### 4. Can I transfer my subgraph to another owner?[#Link to this section](https://thegraph.com/docs/en/studio/studio-faq/#4-can-i-transfer-my-subgraph-to-another-owner) <a href="#4-can-i-transfer-my-subgraph-to-another-owner" id="4-can-i-transfer-my-subgraph-to-another-owner"></a>

Yes, subgraphs that have been published to Mainnet can be transferred to a new wallet or a Multisig. You can do so by clicking the three dots next to the 'Publish' button on the subgraph's details page and selecting 'Transfer ownership'.

Note that you will no longer be able to see or edit the subgraph in Studio once it has been transferred.

#### 5. How do I find query URLs for subgraphs if I’m not the developer of the subgraph I want to use?[#Link to this section](https://thegraph.com/docs/en/studio/studio-faq/#5-how-do-i-find-query-ur-ls-for-subgraphs-if-i-m-not-the-developer-of-the-subgraph-i-want-to-use) <a href="#5-how-do-i-find-query-ur-ls-for-subgraphs-if-i-m-not-the-developer-of-the-subgraph-i-want-to-use" id="5-how-do-i-find-query-ur-ls-for-subgraphs-if-i-m-not-the-developer-of-the-subgraph-i-want-to-use"></a>

You can find the query URL of each subgraph in the Subgraph Details section of The Graph Explorer. When you click on the “Query” button, you will be directed to a pane wherein you can view the query URL of the subgraph you’re interested in. You can then replace the `<api_key>` placeholder with the API key you wish to leverage in the Subgraph Studio.

Remember that you can create an API key and query any subgraph published to the network, even if you build a subgraph yourself. These queries via the new API key, are paid queries as any other on the network.

\


