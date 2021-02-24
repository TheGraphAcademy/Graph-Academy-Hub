graphprotocol-infrastructure
========

A monitoring solution for hosting a graph node on a single Docker host with [Prometheus](https://prometheus.io/), [Grafana](http://grafana.org/), [cAdvisor](https://github.com/google/cadvisor),
[NodeExporter](https://github.com/prometheus/node_exporter) and alerting with [AlertManager](https://github.com/prometheus/alertmanager).

The monitoring configuration adapted the template by the graph team in the [mission control repository](https://github.com/graphprotocol/mission-control-indexer).


## Get a domain 

To enable SSL on your host you should get a domain.

You can use any domain and any regsitrar that allowes you to edit DNS records to point subdomains to your IP address.

For a free option go to [dotTK](http://www.dot.tk) and find a free domain name. Create a account and complete the registration. 

Hint: the shop is a bit broken. On the first try to checkout the shopping cart was empty for me, but there is a link to go back to the search results. Click this to go back, put the domain in the shopping cart again, next time it worked.

In the last step choose "use dns" and enter the IP address of your server for 2 subdomains like in the picture. You can choose up to 12 months for free.

Under "Service > My Domains > Manage Domain > Manage Freenom DNS" you can add more subdomains later for e.g. the Grafana dashboard.

## Install

Prerequisites:

* Docker Engine >= 1.13
* Docker Compose >= 1.11

On a fresh Ubuntu server login via ssh and execute the following commands:

```bash
apt update -y
apt install docker.io docker-compose httpie
```

Clone this repository on your Docker host, cd into graphprotocol-infrastructure directory and run compose up:

```bash
git clone https://github.com/trader-payne/graphprotocol-infrastructure.git
cd graphprotocol-infrastructure

EMAIL=my@email GRAFANA_HOST=grafana.mydomain.tk GRAPH_NODE=graph.mydomain.tk ADMIN_USER=admin ADMIN_PASSWORD=change_me ETHEREUM="mainnet:<ETH_RPC_URL>"  ETHEREUM_START_BLOCK=7710671 docker-compose up -d
```
-----------
You can skip the SSL/Nginx part by simply spinning the infra up via:
```
ADMIN_USER=admin ADMIN_PASSWORD=change_me ETHEREUM="mainnet:<ETH_RPC_URL>"  ETHEREUM_START_BLOCK=7710671 docker-compose up -d
```
-------------------

The ADMIN_USER and ADMIN_PASSWORD will be used by Grafana, Prometheus and AlertManager.
GRAPH_NODE and GRAFANA_HOST should point to the subdomains created earlier.

Containers:

* Graph Node (indexer / query node) `http://<host-ip>:8000`
* Postgres Database
* Prometheus (metrics database) `http://<host-ip>:9090`
* Prometheus-Pushgateway (push acceptor for ephemeral and batch jobs) `http://<host-ip>:9091`
* AlertManager (alerts management) `http://<host-ip>:9093`
* Grafana (visualize metrics) `http://<host-ip>:3000`
* NodeExporter (host metrics collector)
* cAdvisor (containers metrics collector)
* Caddy (reverse proxy and basic auth provider for prometheus and alertmanager)

## Indexing Subgraphs

Connect via ssh to the server and issue the following commands to index the subraphs required for phase 0 of the testnet challenge.

```bash
http post 127.0.0.1:8020 jsonrpc="2.0" method="subgraph_create" id="2" params:='{"name": "synthetixio-team/synthetix"}'
http post 127.0.0.1:8020 jsonrpc="2.0" id="2" method="subgraph_deploy" params:='{"name": "synthetixio-team/synthetix", "ipfs_hash": "Qme2hDXrkBpuXAYEuwGPAjr6zwiMZV4FHLLBa3BHzatBWx"}'

http post 127.0.0.1:8020 jsonrpc="2.0" method="subgraph_create" id="2" params:='{"name": "uniswap/uniswap-v2"}'
http post 127.0.0.1:8020 jsonrpc="2.0" id="2" method="subgraph_deploy" params:='{"name": "uniswap/uniswap-v2", "ipfs_hash": "QmXKwSEMirgWVn41nRzkT3hpUBw29cp619Gx58XW6mPhZP"}'

http post 127.0.0.1:8020 jsonrpc="2.0" method="subgraph_create" id="1" params:='{"name": "molochventures/moloch"}'
http post 127.0.0.1:8020 jsonrpc="2.0" id="1" method="subgraph_deploy" params:='{"name": "molochventures/moloch", "ipfs_hash": "QmTXzATwNfgGVukV1fX2T6xw9f6LAYRVWpsdXyRWzUR2H9"}'

http post 127.0.0.1:8020 jsonrpc="2.0" method="subgraph_create" id="4" params:='{"name": "jannis/gravity"}'
http post 127.0.0.1:8020 jsonrpc="2.0" id="4" method="subgraph_deploy" params:='{"name": "jannis/gravity", "ipfs_hash": "QmbeDC4G8iPAUJ6tRBu99vwyYkaSiFwtXWKwwYkoNphV4X"}'
```

## Debugging

In case of problems you can access the log output of each container (e.g. graph-node) with the command

```bash
docker logs <container> --follow --tail 100
