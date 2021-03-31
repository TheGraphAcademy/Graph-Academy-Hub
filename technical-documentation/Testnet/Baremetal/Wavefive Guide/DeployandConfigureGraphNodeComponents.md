# Summary
This guide provides instructions for:
* Installing graph-node, query-node
* Where relevant, configuring a systemd unitfile for each component, so they auto-restart on failure.

## Acknowledgements and Disclaimer
The contents of this guide has been pulled together from a variety of sources. It has been tested on Ubuntu Server 18.04 and 20.04. Your mileage may vary. The exact versions of Graph components needed for mainnet/testnet are documented [here](https://github.com/graphprotocol/indexer/blob/main/docs/networks.md#testnet-httpstestnetthegraphcom-rinkeby) - many of the commands include specific versions of the Graph software and you will need to crosscheck and use the latest versions approved for the network you are deploying on. 

## Prerequisites
First and foremost, it is assumed that you have [decided on your architecture](https://github.com/cryptovestor21/GraphProtocolGuides/wiki/Decide-on-your-Architecture) before starting this guide - VMs or containers, storage sizing and redundancy, Eth node choice. At all times, this guide will use the [reference architecture](https://github.com/cryptovestor21/GraphProtocolGuides/wiki/Decide-on-your-Architecture#reference-architecture) for all instructions. This guide is not intended for absolute beginners. It assumes some knowledge of using a linux terminal. Before you get started you will need to have your Ubuntu server instance up and running and up to date. Your server will require an internet connection. This guide assumes that you are logged into the server using a non-root account with SUDO access. Security will not be covered in this guide.

Please note that in order to successfully build and compile this software you will need 4 cores and 2GB of memory as a minimum.

## graph-node installation
Per the reference architecture, two of these nodes should be deployed. To avoid repetition, the guide will only run through the first install. We will also build a query-node, which is simply a graph-node with indexing turned off and graphql query logging turned on, for use in serving queries to consumers and analyzing the performance of served queries.

Additional packages that may need to be installed: 

Rust - `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
Git - `sudo apt install git`
To support Rust compiles - `sudo apt-get install -y clang libpq-dev libssl-dev pkg-config build-essential`

Make a directory graph-node in home:
`mkdir ~/graph-node`

#### Build graph-node
Download and compile the tagged release of graph-node using the following command:

`cd ~/ && rm -rf ~/graph-node && git clone https://github.com/graphprotocol/graph-node ~/graph-node && cd ~/graph-node && git checkout v0.21.1 && cargo build --release`

In the above case we are checking out the `v0.21.1` tag. Make sure and check that you are using the right version for the network you are deploying to as per the link in the Acknowledgements section.

#### Configure graph-node startup script
Run the following to create the graph-node startup script

```
tee ~/graph-startup.sh<<EOF

#!/bin/bash
source $HOME/.cargo/env
cd $HOME/graph-node

cargo run -p graph-node --release -- \\
        --node-id graph-test-node-0 \\
        --postgres-url postgresql://postgres:changeme@graph-test-postgres-0:5432/graph-node \\
        --ethereum-rpc mainnet:http://graph-test-eth-0:8545 \\
        --ipfs https://ipfs.testnet.thegraph.com

EOF
```
Make the script executable by running `chmod +x graph-startup.sh`

As a preliminary test, you can manually execute the script `./graph-startup.sh` and should see the initial compilation process kick off (this will take some time)
```
$ ./graph-startup.sh 
   Compiling libc v0.2.80
   Compiling proc-macro2 v1.0.24
   Compiling syn v1.0.48
   Compiling log v0.4.11
   Compiling lazy_static v1.4.0
     Building [============>            ] 10/650...
```
Once compilation is complete the graph-node should start and will look something like:
```
Feb 15 17:27:04.779 INFO Graph Node version: v0.21.1 (8915fd15c 2021-01-11)
Feb 15 17:27:04.779 INFO Generating configuration from command line arguments
Feb 15 17:27:04.809 INFO Starting up
Feb 15 17:27:04.810 INFO Trying IPFS node at: https://ipfs.testnet.thegraph.com/
Feb 15 17:27:04.829 INFO Creating transport, capabilities: archive, trace, url: http://graph-test-eth-0:8545, network: mainnet
Feb 15 17:27:04.961 INFO Connecting to Postgres, weight: 1, conn_pool_size: 10, url: postgresql://postgres:HIDDEN_PASSWORD@graph-test-postgres-0:5432/graph-node, pool: main, shard: primary
Feb 15 17:27:05.070 INFO Pool successfully connected to Postgres, pool: main, shard: primary, component: Store
Feb 15 17:27:05.137 INFO Waiting for other graph-node instances to finish migrating, shard: primary, component: Store
Feb 15 17:27:05.144 INFO Running migrations, shard: primary, component: Store
Feb 15 17:27:05.160 INFO Successfully connected to IPFS node at: https://ipfs.testnet.thegraph.com/
Feb 15 17:27:07.861 INFO Migrations finished, shard: primary, component: Store
Feb 15 17:27:07.884 INFO Connecting to Ethereum..., capabilities: archive, trace, network: mainnet
Feb 15 17:27:07.900 INFO Connected to Ethereum, capabilities: archive, trace, network_version: 1, network: mainnet
Feb 15 17:27:07.918 INFO Creating LoadManager in disabled mode, component: LoadManager
Feb 15 17:27:07.921 INFO Starting block ingestors
Feb 15 17:27:07.921 INFO Starting block ingestor for network, network_name: mainnet
Feb 15 17:27:07.934 INFO Starting JSON-RPC admin server at: http://localhost:8020, component: JsonRpcServer
Feb 15 17:27:07.936 INFO Started all subgraphs, component: SubgraphRegistrar
Feb 15 17:27:07.937 INFO Starting GraphQL HTTP server at: http://localhost:8000, component: GraphQLServer
Feb 15 17:27:07.938 INFO Starting index node server at: http://localhost:8030, component: IndexNodeServer
Feb 15 17:27:07.941 INFO Starting metrics server at: http://localhost:8040, component: MetricsServer
Feb 15 17:27:07.942 INFO Starting GraphQL WebSocket server at: ws://localhost:8001, component: SubscriptionServer
Feb 15 17:27:08.027 INFO Downloading latest blocks from Ethereum. This may take a few minutes..., network_name: mainnet, component: BlockIng....
```

### graph-node systemd configuration
Once confident that your node runs correctly, it is important to configure the node to start automatically and restart itself if a failure occurs. To achieve this we can used systemd to manage the node process.

Run the following command to create your graphindexer unit file
```
sudo tee /etc/systemd/system/graphindexer.service<<EOF

[Unit]
Description=Graph Indexer Node
After=network.target 
Wants=network.target
[Service]
User=node
Group=node
WorkingDirectory=/home/node/
StandardOutput=journal
StandardError=journal
Type=simple
Restart=always
RestartSec=5
ExecStart= /home/node/graph-startup.sh

[Install]
WantedBy=default.target
EOF
```

Note how the unitfile called the script you made earlier. Keep in mind that this script contains your Postgres database password for the postgres user.

Reload the systemd daemon to include the new service unitfile

```
sudo systemctl daemon-reload
```

Start the graph-node service

```
sudo systemctl start graphindexer.service
```

Check that graph-node is running as expected

```
sudo systemctl status graphindexer.service
```

You can also tail the logs for more details

```
sudo journalctl --follow -o cat -u graphindexer.service
```

When you are satisfied that the node is running correctly, you can enable it for automatic restart on fail/system restart:

```
sudo systemctl enable graphindexer.service
```

## query-node installation

Follow the [graph-node](https://github.com/cryptovestor21/GraphProtocolGuides/wiki/Deploy-and-Configure-Graph-Components#graph-node-installation) installation steps. Stop just before you hit the `Congifure graph-node startup script` section.

### Configure query-node startup script

Run the following to create the query-node startup script

```
tee ~/graph-startup.sh<<EOF

#!/bin/bash
source $HOME/.cargo/env
cd $HOME/graph-node

export GRAPH_LOG_QUERY_TIMING="gql"
export DISABLE_BLOCK_INGESTOR="true"

cargo run -p graph-node  --release -- --debug \\
        --node-id query0 \\
        --postgres-url postgresql://postgres:changeme@graph-test-postgres-0:5432/graph-node \\
        --ethereum-rpc mainnet:http://graph-test-eth-0:8545 \\
        --ipfs https://ipfs.testnet.thegraph.com

EOF
```

Note the application of two environment variables `GRAPH_LOG_QUERY_TIMING` and `DISABLE_BLOCK_INGESTOR` these are the variables that configure the graph node to act as a query node. Adding graph log query timing allows the extraction of graphql performance data on subgraph queries. Disabling the block ingestor means this node will not be able to index subgraphs. Its only role will be to collect query performance data and serve queries to the end user.

Make the script executable by running `chmod +x graph-startup.sh`

As per your experience deploying a standard graph node, you can manually execute the script ./graph-startup.sh and should see the initial compilation process kick off (this will take some time)

Once compilation is complete the node should start running, looking something like:

```
Mar 23 16:36:21.014 INFO Graph Node version: v0.21.1 (8915fd15c 2021-01-11)
Mar 23 16:36:21.017 INFO Generating configuration from command line arguments
Mar 23 16:36:21.165 INFO Starting up
Mar 23 16:36:21.165 INFO Trying IPFS node at: https://ipfs.testnet.thegraph.com/
Mar 23 16:36:21.206 INFO Creating transport, capabilities: archive, trace, url: http://graph-test-eth-0:8545, network: mainnet
Mar 23 16:36:21.273 DEBG Cleaning up large notifications after about 300s, channel: store_events, component: NotificationListener
Mar 23 16:36:21.384 INFO Connecting to Postgres, weight: 1, conn_pool_size: 10, url: postgresql://postgres:HIDDEN_PASSWORD@graph-test-postgres-0:5432/graph-node, pool: main, shard: primary
Mar 23 16:36:21.690 INFO Successfully connected to IPFS node at: https://ipfs.testnet.thegraph.com/
Mar 23 16:36:21.808 INFO Pool successfully connected to Postgres, pool: main, shard: primary, component: Store
Mar 23 16:36:21.845 INFO Waiting for other graph-node instances to finish migrating, shard: primary, component: Store
Mar 23 16:36:21.851 INFO Running migrations, shard: primary, component: Store
Mar 23 16:36:21.917 INFO Migrations finished, shard: primary, component: Store
Mar 23 16:36:21.918 DEBG Using postgres host order [Main], shard: primary, component: Store
Mar 23 16:36:21.918 DEBG Cleaning up large notifications after about 300s, channel: chain_head_updates, component: ChainHeadUpdateListener > NotificationListener
Mar 23 16:36:21.936 INFO Connecting to Ethereum..., capabilities: archive, trace, network: mainnet
Mar 23 16:36:21.946 INFO Connected to Ethereum, capabilities: archive, trace, network_version: 1, network: mainnet
Mar 23 16:36:21.989 INFO Creating LoadManager in disabled mode, component: LoadManager
Mar 23 16:36:22.014 INFO Starting JSON-RPC admin server at: http://localhost:8020, component: JsonRpcServer
Mar 23 16:36:22.018 INFO Started all subgraphs, component: SubgraphRegistrar
Mar 23 16:36:22.021 INFO Starting GraphQL HTTP server at: http://localhost:8000, component: GraphQLServer
Mar 23 16:36:22.022 INFO Starting index node server at: http://localhost:8030, component: IndexNodeServer
Mar 23 16:36:22.023 INFO Starting metrics server at: http://localhost:8040, component: MetricsServer
Mar 23 16:36:22.023 INFO Starting GraphQL WebSocket server at: ws://localhost:8001, component: SubscriptionServer
```

You can now use the [graph-node systemd configuration](https://github.com/cryptovestor21/GraphProtocolGuides/wiki/Deploy-and-Configure-graph-node-Components/_edit#graph-node-systemd-configuration) to automate restarting of the query node.

You have successfully built two graph-nodes and one query node.

        
