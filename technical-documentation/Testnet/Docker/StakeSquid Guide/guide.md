# Graph Protocol Testnet Docker Compose

**Github repository**: [https://github.com/StakeSquid/graphprotocol-testnet-docker](https://github.com/StakeSquid/graphprotocol-testnet-docker)

**Setup video**: [https://www.youtube.com/watch?v=bSr8L1GPk54](https://www.youtube.com/watch?v=bSr8L1GPk54)

A monitoring solution for hosting a graph node on a single Docker host with [Prometheus](https://prometheus.io/), [Grafana](http://grafana.org/), [cAdvisor](https://github.com/google/cadvisor), [NodeExporter](https://github.com/prometheus/node\_exporter) and alerting with [AlertManager](https://github.com/prometheus/alertmanager).

The monitoring configuration adapted the K8S template by the graph team in the [mission control repository](https://github.com/graphprotocol/mission-control-indexer) during the testnet, and later adapted for the new testnet release using [this configuration](https://github.com/graphprotocol/indexer/blob/main/docs/networks.md#testnet-httpstestnetthegraphcom-rinkeby).

The advantage of using Docker, as opposed to systemd bare-metal setups, is that Docker is easy to manipulate around and scale up if needed. We personally ran the whole testnet infrastructure on the same machine, including a TurboGeth Archive Node (not included in this docker build).

For those that consider running their infras like we did, here are our observations regarding the necessary hardware specs:

> From my experience during the testnet, the heaviest load was put onto Postgres at all times, whilst the other infrastructure parts had little to no load on them at times. And Postgres loads the CPU enormously even with all the optimizations in the world. Even my 48 core EPYC was struggling to deliver a steady 100-150 queries per second for Uniswap during the testnet. I think I hit 90 system load on it before my ETH node collapsed (it wasn't related to the traffic, just a sad coincidence)

The good thing about Docker, is that the data is stored in named volumes on the docker host and can be exported / copied over to a bigger machine once more performance is needed.

Note that you **need** access to an **Ethereum Archive Node that supports EIP-1898**. The setup for the archive node is **not included** in this docker setup.

The minimum configuration should to be the CPX51 VPS at Hetzner. Feel free to sign up using our [referral link](https://thegraph.academy/recommends/hetzner/) -- you can save 20€ and we get 10€ bonus for setting up some testnet nodes to support the network growth. :)

## Ethereum Archive Node Specs

|         | Minimum Specs   | Recommended Specs | Maxed out Specs   |
| ------- | --------------- | ----------------- | ----------------- |
| CPUs    | 16 vcore        | 32 vcore          | 64 vcore          |
| RAM     | 32 GB           | 64 GB             | 128 GB            |
| Storage | 1.5 TB SATA SSD | 7 TB NVME         | 7 TB NVME RAID 10 |

_Note: The 1.5 TB requirement for storage is the absolute minimum, it needs to be at least SATA SSD as it doesn't work with spinning disks. Also, only TurboGETH has that little space required. OE, Parity and GETH all take 7 TB at the very minimum, and expanding pretty fast._

### Archive node options

| Self-hosted        | Trace API | Stable | EIP-1898 | Min Disk Size |
| ------------------ | --------- | ------ | -------- | ------------- |
| OpenEthereum 3.0.x | yes ✔️    | no ⚠️  | yes ✔️   | 7 TB          |
| OpenEthereum 3.1   | yes ✔️    | no ⚠️  | no ☠️    | 7 TB          |
| OpenEthereum 3.2   | yes ✔️    | TBD ⚠️ | yes ✔️   | 7 TB          |
| Parity 2.5.13      | yes ✔️    | yes ✔️ | no ☠️    | 7 TB          |
| GETH               | no ⚠️     | yes ✔️ | yes ✔️   | 7 TB          |
| TurboGETH          | no ⚠️     | no ⚠️  | yes ✔️   | 1.5 TB        |

| Service Providers (WIP) |
| ----------------------- |
| Infura                  |
| Alchemy                 |
| ChainStack              |
| Quiknode                |
| Ankr                    |

## Graph Protocol Infrastructure Specs

|         | Minimum Specs   | Recommended Specs | Maxed out Specs   |
| ------- | --------------- | ----------------- | ----------------- |
| CPU     | 16 vcore        | 64 vcore          | 128 vcore         |
| RAM     | 32 GB           | 128 GB            | 256/512 GB        |
| Storage | 300 GB SATA SSD | 2 TB NVME         | 4 TB NVME RAID 10 |

_The specs/requirements listed here come from our own experience during the testnet._

_Your mileage may vary, so take this with a grain of salt and be ready to upgrade._ :)

* The minimum specs will definitely get you running, but not for long, assuming you want to serve data for more than a few heavy-weight subgraphs in the future.
* The recommended specs are a good setup for those that want to dip more than their feet in the indexing waters. Can serve a decent number of subgraphs, but it's limited by the CPU if too many requests flow through.
* The maxed out specs rule of thumb is basically more is better. More CPUs, more RAM, faster disks. There is never enough. IT...NEEDS....MORE!!!!11

Closing note, regarding the specs mentioned above: ideally, they need to scale up proportional with your stake in the protocol.

## Prerequisites

* Docker Engine >= 1.10.0
* Docker Compose >= 1.6.0
* git

On a fresh Ubuntu server login via ssh and execute the following commands:

```bash
apt update -y
apt install docker.io docker-compose httpie git
```

## Install from scratch

Run the following commands to clone the repository and set everything up:

```bash
git clone git@github.com:StakeSquid/graphprotocol-testnet-docker.git
cd graphprotocol-testnet-docker
git submodule init
git submodule update
git config user.email "you@example.com"
git config user.name "Example User"
git branch --set-upstream-to=origin/master
```

## Install or Update the Agora and Qlog modules

To update those repos to the latest version just do the following command occasionally.

```bash
git submodule update
```

To use qlog or agora execute the `runqlog` or `runagora` scripts in the root of the repository.

```bash
./runagora --help
./runqlog --help
```

This will use the compiled qlog tool and extract queries since yesterday or 5 hours ago and store them to the query-logs folder.

```bash
./extract_queries_since yesterday 
./extract_queries_since "5 hours ago"
```

To make journald logs persistent across restarts you need to create a folder for the logs to store in like this:

```
mkdir -p /var/log/journal
```

That's all.

## Get a domain

To enable SSL on your host you should get a domain.

You can use any domain and any regsitrar that allowes you to edit DNS records to point subdomains to your IP address.

For a free option go to [myFreenom](https://my.freenom.com/) and find a free domain name. Create a account and complete the registration.

In the last step choose "use dns" and enter the IP address of your server. You can choose up to 12 months for free.

Under "Service > My Domains > Manage Domain > Manage Freenom DNS" you can add more subdomains later.

Create 3 subdomains, named as follows:

```
index.sld.tld
query.sld.tld
dashboard.sld.tld
```

## Create a mnemonic

You need a wallet with a seed phrase that is registered as your operator wallet. This wallet will be the one that makes transactions on behalf of your main wallet (which holds and stakes the GRT). The operator wallet has limited functionality, and it's recommended to be used for security reasons.

_You need a 12-word, or 15-word mnemonic phrase in order for it to work._

To make yourself a mnemonic eth wallet you can go to this [website](https://iancoleman.io/bip39/) and just press generate. You get a seed phrase in the input field labeled BIP39 Mnemonic. Scroll down a bit and find the select field labeled Coin. Select ETH as network in the dropdown and you find your address, public key and private key in the first row of the table if you scroll down the page in the section with the heading "Derived Addresses". You can import the wallet using the private key into Metamask.

## Run

In the root of the repo, create (or edit, it's already there) a file called `start` and insert the following lines in it:

```bash
ADMIN_TOKEN="your-vector-admin-token" \
EMAIL=email@sld.tld \
INDEX_HOST=index.sld.tld \
QUERY_HOST=query.sld.tld \
GRAFANA_HOST=dashboard.sld.tld \
ADMIN_USER=admin \
ADMIN_PASSWORD=password \
DB_USER=user \
DB_PASS=password \
AGENT_DB_NAME=indexer-agent \
GRAPH_NODE_DB_NAME=graph-node \
ETHEREUM_RPC="mainnet:url:port" \
RINKEBY_RPC="url:port" \
OPERATOR_SEED_PHRASE="12 or 15 word phrase" \
STAKING_WALLET_ADDRESS=0x... \
GEO_COORDINATES="69.420 69.420" \
JSON_STRING=$(jq -n --arg at "$ADMIN_TOKEN" --arg rr "$RINKEBY_RPC" --arg osp "$OPERATOR_SEED_PHRASE" '{"adminToken":$at,"chainProviders":{"4":$rr},"logLevel":"info","natsUrl":"nats://nats1.connext.provide.network:4222,nats://nats2.connext.provide.network:4222,nats://nats3.connext.provide.network:4222","authUrl":"https://messaging.connext.network","messagingUrl":"https://messaging.connext.network","production":true,"baseGasSubsidyPercentage":0,"allowedSwaps":[],"skipCheckIn":true,"mnemonic":$osp}') \
docker-compose up -d --remove-orphans --build $@
```

**To start the software, just do `bash start`**

`EMAIL` is only used as contact to create SSL certificates. Usually it doesn't receive any emails but is required by the certificate issuer.

`QUERY_HOST`, `INDEX_HOST` and `GRAFANA_HOST` should point to the subdomains created earlier.

`ADMIN_USER` and `ADMIN_PASSWORD` will be used by Grafana, Prometheus and AlertManager.

`DB_HOST` - do not modify this unless you're running native (non-dockerized) PostgreSQL.

`AGENT_DB_HOST` - do not modify this unless you're running native (non-dockerized) PostgreSQL.

`DB_USER` and `DB_PASS` will be used for initializing the PostgreSQL Databases (both index/query DB and indexer agent/service DB).

`AGENT_DB_NAME` is the name of the database used by the Indexer agent/service nodes.

`GRAPH_NODE_DB_NAME` is the name of the database used by the Index/Query nodes.

`MAINNET_RPC` should be your Mainnet Ethereum Archive node endpoint. This will be used by the index/query node ingestors.

`RINKEBY_RPC` should be your Rinkeby RPC - can be a fast/full node, can also be an infura account.

`OPERATOR_SEED_PHRASE` should belong to the operator wallet mnemonic phrase.

`STAKING_WALLET_ADDRESS` needs to be the address that you staked your GRT with.

To find out the `GEO_COORDINATES` you can search for an ip location website and check your server exact coordinates.

`JSON_STRING` do not modify this, leave as it is.

In case something goes wrong try to add `--force-recreate` at the end of the command, eg.: `bash start --force-recreate`.

Containers:

* Graph Node (query node) `https://query.sld.tld`
* Graph Node (index node) `https://index.sld.tld`
* Indexer Agent
* Indexer Service
* Indexer CLI
* Postgres Database for the index/query nodes
* Postgres Database for the agent/service nodes
* Prometheus (metrics database) `http://<host-ip>:9090`
* Prometheus-Pushgateway (push acceptor for ephemeral and batch jobs) `http://<host-ip>:9091`
* AlertManager (alerts management) `http://<host-ip>:9093`
* Grafana (visualize metrics) `http://<host-ip>:3000`
* NodeExporter (host metrics collector)
* cAdvisor (containers metrics collector)
* Caddy (reverse proxy and basic auth provider for prometheus and alertmanager)

## Updates and Upgrades

The general procedure is the following:

```bash
cd <project-folder>
git pull
```

This will update the scripts from the repository.

To upgrade the containers:

```bash
bash start --force-recreate <container-name>
```

To update Agora or Qlog repos to the latest version just do the following command occasionally:

```bash
git submodule update
```

To use qlog or agora execute the `runqlog` or `runagora` scripts in the root of the repository.

```bash
./runagora --help
./runqlog --help
```

## Managing Allocations

* To **control** the allocations, we will use the **indexer-cli**
* To **check** our allocations, we will use the **indexer-cli, other community-made tools, and later on, the Graph Explorer**

## How to check your allocations

Assuming you already have the graph-cli and indexer-cli installed, in the root of the directory, type:

```bash
./shell cli
graph indexer rules get all
```

You will be greeted by this table. By default, it's set to these values below: ![](https://i.imgur.com/rPwX9wL.png)

### What do the table columns mean?

* `deployment` - can be either **global**, or an **IPFS hash** of a subgraph of your choice
* `allocationAmount` - refers to the **GRT allocation** that you want to set, either **globally** or for a **specific subgraph**, depending on your preference
* `parallelAllocations` - influence how many **state channels** the gateways open with you for a deployment, and this in turn affects the max query request rate you can receive
* `minSignal` - conditional decision basis ruled by the **minimum** Subgraph **Signal**
* `maxSignal` - conditional decision basis ruled by the **maximum** Subgraph **Signal**
* `minStake` - conditional decision basis ruled by the **minimum** Subgraph **Stake**
* `minAverageQueryFees` - conditional decision basis ruled by the **minimum average** of **query fees**
* `decisionBasis` - dictates the **behavior** of your **rules**

### General caveats

* Your total stake of a specific subgraph, or globally, will be calculated as follows:

`allocationAmount` x `parallelAllocations` = `totalStake`

**Example:**

`allocationAmount 100` x `parallelAllocations 5` = 500 GRT allocated

* `decisionBasis` can be of three types: `always` , `never` and `rules`

`decisionBasis always` overrides the conditional decision basis rules that you might have set (minStake, minSignal, etc) and will ensure that your **allocation** is **always active**

`decisionBasis never` same as above, only that it will ensure that your **allocation** is **always inactive**

`decisionBasis rules` will give you the option of using the conditional decision basis

* `global` rules will have, by default, an `allocationAmount` of `0.01` GRT and `parallelAllocations` set to `2`

This means that by default, every time you set an `allocationAmount` of a specific subgraph, it will inherit `parallelAllocations 2` rule from `global`.

To see the global rules merged into the rest of your allocations table, you can use the following command:

```bash
graph indexer rules get all --merged
```

## How to set allocations?

**Examples:**

**1.**

```bash
graph indexer rules set {IPFS_HASH} allocationAmount 1000 decisionBasis always
```

Assuming the `{IPFS_HASH}` exists on-chain, this will set an `allocationAmount` of `1000 GRT` and will ensure that the subgraph will `always` be allocated, through `decisionBasis always`

**2.**

```bash
graph indexer rules set global allocationAmount 100 parallelAllocations 10 decisionBasis always
```

This command will enable you to automatically allocate `100 GRT` x `10 parallelAllocations` to **all** the subgraphs that exist on-chain, with 10 parallel allocations each

**3.**

```bash
graph indexer rules set {IPFS_HASH} allocationAmount 1337 parallelAllocations 5 minSignal 100 maxSignal 200 decisionBasis rules
```

This command will enable you to use the decision basis conditional rules of minSignal and maxSignal. The subgraph will only get allocated by the Agent IF the network participants have a minimum of 100 signal strength and a maximum of 200 signal strength.

Generally speaking, you'll be good to just use either the first command or the second one, as they're not complicated to understand. Just be aware of the parallelAllocations number.

## How to verify your allocations?

We can use the following command(s) with the indexer-cli:

**This will only display the subgraph-specific allocation rules**

```bash
graph indexer rules get {IPFS_HASH}
```

**This will display the full rules table**

```bash
graph indexer rules get all
```

**This will display the full rules table with the global values merged**

```bash
graph indexer rules get all --merged
```

## What happens after you set your allocations?

The indexer-agent will now start to allocate the amount of GRT that you specified for each subgraph that it finds to be present on-chain.

Depending on how many subgraphs you allocated towards, it will take time for this action to finish.

Keep in mind that the indexer-agent once given the instructions to allocate, it will throw everything in a queue of transactions that you will not be able to close. For example, if you set `global always` then immediately after, you decide to set `global rules` or `never` it will do a full set of transactions for `global always` then go around and deallocate from them with your second transactions. This means that you will likely be facing a lot of delay between the input time and until the actions have finalized on-chain.

A workaround for this is to restart the indexer-agent app/container, as this will reset his internal queue managing system and start with the most fresh data that it has.

Another workaround is to either delete your rules with `graph indexer rules delete {IPFS}`

## Managing cost models

### What are cost models?

Cost models are indexer tools that they can use in order to set a price for the data that they serve.

You cannot earn GRT for the queries that you serve without a cost model.

The cost models are denominated in decimal GRT.

**Cost models can have two parts:**

* The model — should contain the queries that you want to price
* The variables — should contain the variables that the queries use

You can either have a static, simple cost model, or you can dive into complicated cost models based on your database access times for different queries that you serve across different subgraphs, etc.

The decision here is totally up to you 🙂

### How does a model look like?

**The easiest cost model you can set, can look something like this:**

```bash
default => price;

or 

query {...} => price;
```

**Example — you're serving every query at 0.01 GRT / query**

```bash
default => 0.01;
```

### How do the variables look like?

```javascript
{                              
  "VALUE-1": "10.0006390502074853",
  "VALUE-2": "5",                 
  "VALUE-3": "3",                
  "VALUE-4": "1"               
}
```

## Debugging and troubleshooting

First off, I strongly recommend having either `graph-pino` or `pino-pretty` installed for this, along with `Grafana` or something else to collect the data scraped by `Prometheus` and be easily accessible at a glance.

You will need NPM installed for this.

```bash
sudo apt install npm -y
```

To install `graph-pino`, you can simply do:

```bash
npm install -g --registry <https://registry.npmjs.org/> @graphprotocol/graph-pino
```

To install `pino-pretty`, you can simply do:

```bash
npm install -g pino-pretty
```

And you're done. These two will greatly help you read through the `indexer-agent` and `indexer-service` logs to easily find errors and warning messages that might occur.

**To use them, you can use the following examples:**

**Graph-pino with Docker**

```bash
docker logs indexer-agent --tail 10 -f | graph-pino
```

**Graph-pino with Journald**

```bash
journalctl -fu indexer-agent -n 10 -f | graph-pino
```

**Pino-pretty with Docker**

```bash
docker logs indexer-agent --tail 10 -f | pino-pretty -c -t
```

**Pino-pretty with Journald**

```bash
journalctl -fu indexer-agent -n 10 -f | pino-pretty -c -t
```

## Troubleshooting scenarios

*   **Indexer-agent and Indexer-service containers are loop crashing**

    This is an indication that your index-node cannot connect to either the PostgreSQL DB or your Ethereum Archive-node

    **I mentioned this in discord, but worth mentioning it here as well:**

    If, at any given time while you're starting up your dockerized/k8s'ed infrastructure, your `INDEX-NODE` can't connect to the `ETH-ARCHIVE`, your agent and service nodes will crash in a loop saying that they can't reach the index-node, but in reality, it's your index-node that can't reach the archive-node. There is no mention in the agent/service logs saying that they crash because of that. Only a `connection refused` error. And there is no mention in the index-node either that it can't connect to the archive node, only that it stalls when connecting, with no timeout. I spent 6 hours trying to fix this, I thought it was an UFW issue blocking my docker containers, when it reality it was what I explained above.
*   **You have allocated, but can't see the subgraph indexing in Grafana?**

    Check the `indexer-agent` logs immediately, the agent is probably still about to send the allocation transaction, but who knows ¯\\\_(ツ)\_/¯
*   **You have allocated, you can see the subgraph indexing, but its blocks behind number doesnt go down**

    Check your `archive-node` logs, and if everything looks good, check your `index-node` logs after
*   **Docker - Nginx load balanced indexer-service nodes are not getting queries or only part of them are**

    When you compose-up, some of your containers, even if you set the correct order of container dependencies, will crash at start-up waiting for others to start first. By design, Nginx caches the internal Docker IPs at start-up. In order to mitigate that problem, add a script in the Nginx start sequence that executes the following command: `nginx -s reload`.

    Alternatively, you can just manually do `docker exec -it nginx-loadbalancer nginx -s reload` right from the host machine.
* **Other indexer-agent errors documentation from the logs can be found here:** [https://github.com/graphprotocol/indexer/blob/main/docs/errors.md](https://github.com/graphprotocol/indexer/blob/main/docs/errors.md)
*   **You're getting `Could not find matching rule with non-null allocation`**

    This means that one of your rules has `allocationAmount null` — usually I've seen this being the `global` rule missing a value.

    To get rid of it, set `graph indexer rules set global allocationAmount 0.01`
*   **How to see what subgraphs are available for indexing**

    All available subgraphs are located in grafana graphql dashboard.

    To convert subgraph id to ipfs hash you can use script `subgraph_convert.py`

    Before running script install python3 module called `base58`.
