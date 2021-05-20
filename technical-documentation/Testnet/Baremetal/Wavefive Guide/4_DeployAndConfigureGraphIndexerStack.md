# Summary
This guide provides instructions for:
* Installing indexer-agent, graph-cli, indexer-cli, indexer-service
* Where relevant, configuring a systemd unitfile for each component, so they auto-restart on failure.

## Acknowledgements and Disclaimer
The contents of this guide has been pulled together from a variety of sources. It has been tested on Ubuntu Server 18.04 and 20.04. Your mileage may vary. The exact versions of Graph components needed for mainnet/testnet are documented [here](https://github.com/graphprotocol/indexer/blob/main/docs/networks.md#testnet-httpstestnetthegraphcom-rinkeby) - many of the commands include specific versions of the Graph software and you will need to crosscheck and use the latest versions approved for the network you are deploying on. 

## Prerequisites
First and foremost, it is assumed that you have decided on your architecture per the earlier part of this guide series - VMs or containers, storage sizing and redundancy, Eth node choice. At all times, this guide will use the reference architecture from the first page for all instructions. This guide is not intended for absolute beginners. It assumes some knowledge of using a linux terminal. Before you get started you will need to have your Ubuntu server instance up and running and up to date. Your server will require an internet connection. This guide assumes that you are logged into the server using a non-root account with SUDO access. Security will not be covered in this guide.

Note: If you are using Linux containers and being economical with the resources you assign to them, you need to be sure that you supply them with enough memory and compute power to install packages, or you will see strange, un-diagnosable behavior from npm. 4 vcpu and 2GB of memory should be sufficient in most cases.

Specific versions of graph software will be used in this guide, but you should always install the latest builds for the network you are deploying to (mainnet or testnet). You can find the approved versions [here](https://github.com/graphprotocol/indexer/blob/main/docs/networks.md)

## Testnet prerequisites
You will need two Ethereum addresses in order to run your Indexer. One Indexer address and one Operator address. Indexer = your main address with all privileges. Operator = the address used by the indexer, only has specific privileges to run the indexer software.

If you are deploying to testnet you will need testnet GRT in order to register your Indexing operation on-chain. Check the discord for info on how to register and receive testnet GRT.

## Software prerequisites

Additional packages that need to be installed: 

**Important:** Due to the inclusion of a Rust build process in the NPM install for many graph indexer components, it is necessary to complete the install process logged in as root. Using `sudo` is not sufficient. Once the indexer software is installed, you are free to run it with any user account you like. If somebody knows how to overcome this need to use a root account and has tested their solution, please submit a PR.

Install curl:
```
apt install curl
```

Latest version of node and npm:
```
curl -sL https://deb.nodesource.com/setup_14.x | \sudo -E bash - && \
sudo apt install -y nodejs && sudo npm install -g npm@latest
```

Rust and related packages for building with Rust:

Rust - `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh` 
Git - `sudo apt install git` 
To support Rust compiles - `sudo apt-get install -y clang libpq-dev libssl-dev pkg-config build-essential`

#### Install indexer-agent
Per the reference architecture, one indexer-agent should be deployed. Reminder: this must be completed signed into the root account, not using `sudo`

```
npm install -g @graphprotocol/indexer-agent@0.12.0
```

Now that you have installed the agent, you can check that it is working by logging out of the root account and into another user account and running:
```
graph-indexer-agent --version
```
And if it's working you should get a version response.

#### Configure the indexer-agent
Now we will create a startup script for the indexer agent:

Notes: You need two separate Ethereum addresses.

--mnemonic correct horse battery staple... - This is the mnemonic for your Indexer Operator address. It has limited ability to only operate the agent and nothing more.

--indexer-address 0x... This is the top level Indexer address, the address with all the privileges. You will use this address to set the Indexer Operator address as a valid operator for your Indexer address later.

```
tee ~/graph-indexer-agent-startup.sh<<EOF

#!/bin/bash
export INDEXER_AGENT_NETWORK_SUBGRAPH_ENDPOINT="https://gateway.network.thegraph.com/network"

graph-indexer-agent start \\
    --network-subgraph-endpoint https://gateway.testnet.thegraph.com/network \\
    --graph-node-query-endpoint http://graph-test-qnode-0:8000/ \\
    --graph-node-admin-endpoint http://graph-test-node-0:8020/ \\
    --graph-node-status-endpoint graph-test-node-0:8030/graphql \\
    --metrics-port 7300 \\
    --inject-dai true \\
    --index-node-ids graphtestnode0,graphtestnode1 \\
    --public-indexer-url http://your-indexer-url:7600/ \\
    --indexer-management-port 18000 \\
    --indexer-geo-coordinates '52.606052' '-2.011507' \\
    --postgres-host graph-test-postgres-0 \\
    --postgres-port 5432 \\
    --postgres-username postgres \\
    --postgres-password yourpassword123 \\
    --postgres-database graph-agent-0 \\
    --ethereum-network mainnet \\
    --ethereum https://graph-test-eth-0:8545 \\
    --mnemonic 'correct horse battery staple...' \\
    --indexer-address 0x... \\
    --no-restake-rewards \\
    --allocation-claim-threshold 50

EOF
```
Make your startup script executable `chmod +x graph-indexer-agent-startup.sh`

Create a service unit file for the agent, so it can auto start on reboot and process failures. Note, in the example below the user `user` is used; you can choose to run the agent under your own choice of username.

```
sudo tee /etc/systemd/system/graph-indexer-agent.service<<EOF

[Unit]
Description=Graph Indexer Agent
After=network.target
Wants=network.target
[Service]
User=user
Group=user
WorkingDirectory=/home/user/
StandardOutput=journal
StandardError=journal
Type=simple
Restart=always
RestartSec=5
ExecStart= /home/user/graph-indexer-agent-startup.sh

[Install]
WantedBy=default.target

EOF
```

Now install the new service using `sudo systemctl daemon-reload`

At this point it is a good idea to manually run your `graph-indexer-agent-startup.sh` and check that it runs correctly. Keep in mind that in order to do this your testnet addresses will need to have Rinkeby eth in order to perform on-chain actions such as registering as an indexer and setting operators. You can follow the official guide to registering on-chain [https://github.com/graphprotocol/indexer/blob/main/docs/networks.md#testnet-httpstestnetthegraphcom-rinkeby](here)

Once you are confident it works correctly, you can enable the service for auto-restart using `sudo systemctl enable graph-indexer-agent.service`

#### Install indexer-service

Install the additional packages described earlier, just as you did for indexer-agent. Remember to install them as root per the above notes, at which point you can then move to a dedicated user for the indexer-service.

Now you can install the service (again, do this as root)

```
npm install -g @graphprotocol/indexer-service@0.12.0
```

#### Configure the indexer-service
Now we will create a startup script for the indexer service:

```
tee ~/graph-indexer-service-startup.sh<<EOF

graph-indexer-service start \\
    --network-subgraph-endpoint https://gateway.testnet.thegraph.com/network \\
    --port 7600 \\
    --graph-node-query-endpoint http://graph-test-qnode-0:8000/ \\
    --graph-node-status-endpoint http://graph-test-node-0:8030/graphql \\
    --ethereum-network rinkeby\\
    --ethereum http://graph-test-eth-0:8545/ \\
    --mnemonic 'impose spin trophy spread sing pyramid adult solution ask theory strong army' \\
    --indexer-address 0x70E77e6b48D8241fAc901Fbd60F43612f77D8088 \\
    --postgres-host graph-test-postgres-0 \\
    --postgres-port 5432 \\
    --postgres-username postgres \\
    --postgres-password super87b \\
    --postgres-database graph-agent \\
    --wallet-worker-threads 4 \\
    --wallet-skip-evm-validation true

EOF
```

Make your startup script executable `chmod +x graph-indexer-service-startup.sh`

Create a service unit file for the agent, so it can auto start on reboot and process failures. Note, in the example below the user `user` is used; you can choose to run the agent under your own choice of username.

```
sudo tee /etc/systemd/system/graph-indexer-service.service<<EOF

[Unit]
Description=Graph Indexer Service
After=network.target
Wants=network.target
[Service]
User=user
Group=user
WorkingDirectory=/home/user/
StandardOutput=journal
StandardError=journal
Type=simple
Restart=always
RestartSec=5
ExecStart= /home/user/graph-indexer-service-startup.sh

[Install]
WantedBy=default.target

EOF
```

#### Install indexer-cli
The indexer-cli is the command line interface tool for interacting with an indexing operation. In this example we deploy a small container specifically for using the CLI however you can deploy this wherever you want within your infrastructure. Deploying a dedicated container for the CLI is quite useful as a starting point for building a Bastion server for your operation - the single point in the network that can access all servers in whatever fashion is required - SSH, Graph CLI or otherwise.

As per other Indexer components, install as root and install all the pre-req software first.

`npm install -g @graphprotocol graph-cli`

`npm install -g @graphprotocol indexer-cli@0.12.0`

You can check the software is installed correctly with `graph --help` and `graph indexer --help`

You are now ready to connect to your indexer-agent using `graph indexer connect http://graph-test-agent-0:18000` once your agent is up and running. Assuming you are deploying to testnet, you need to follow [this](https://github.com/graphprotocol/indexer/blob/main/docs/networks.md#testnet-httpstestnetthegraphcom-rinkeby) guide for getting set up on chain before you start any graph components.

**Quick final note:** If you have issues with `npm install` when following the testnet instructions for getting set up on chain linked above, make sure you have all the pre-req software from this guide installed where your client is installed, and failing that, you can use `yarn install` and `yarn run compile` as an alternative and that should work for your environment.