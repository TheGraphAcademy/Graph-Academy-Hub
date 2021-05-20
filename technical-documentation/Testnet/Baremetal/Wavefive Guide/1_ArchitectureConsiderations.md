Note to reader: Although this guide as a whole is catered towards testnet deployment, this specific document is geared towards very serious, production-ready, mainnet-ready Graph deployments.

That being said, if you are deploying just for fun on testnet, a spare PC with 16 core cpu and lots of SSD storage is a very good place to start with learning about Indexing on The Graph.

## Reference Architecture
For the purposes of this guide, the following reference architecture will be used for a very capable Graph indexing deployment that can comfortably handle many subgraphs and Ethereum chain growth for the next 6-12months or more:


|Component   |Platform   |Spec   |
|---|---|---|
|graph-test-eth-0 (OpenEthereum 3.0.1, trace enabled)   |VM   |32vcpu, 64GBram, 12TB dedicated ZFS RaidZ2   |
|graph-test-postgres-0 (graph-node, graph-agent DBs)   |VM   |32vcpu, 32GBram, Thin-provisioned 2TB shared ZFS RaidZ2   |
|graph-test-node-0   |LXC   |8vcpu, 8GBram, Thin-provisioned 16GB shared ZFS RaidZ2   |
|graph-test-node-1   |LXC   |8vcpu, 8GBram, Thin-provisioned 16GB shared ZFS RaidZ2   |
|graph-test-qnode-0   |LXC   |16vcpu, 8GBram, Thin-provisioned 16GB shared ZFS RaidZ2   |
|graph-test-agent-0   |LXC   |8vcpu, 8GBram, Thin-provisioned 8GB shared ZFS RaidZ2   |
|graph-test-service-0   |LXC   |8vcpu, 8GBram, Thin-provisioned 4GB shared ZFS RaidZ2   |
|graph-test-service-1   |LXC   |8vcpu, 8GBram, Thin-provisioned 4GB shared ZFS RaidZ2   |
|graph-test-nginx-0   |LXC   |4vcpu, 4GBram, Thin-provisioned 4GB shared ZFS RaidZ2   |
|graph-test-client-0   |LXC   |2vcpu, 1GBram, Thin-provisioned 4GB shared ZFS RaidZ2   |

## Physical servers? Hypervisors?

It is entirely possible to deploy most of a Graph infrastructure in a baremetal fashion to one very large server, however if you do intend to do that, it is recommended to deploy using Docker in order to make the job of scaling easier in the future. You can follow [this](https://github.com/StakeSquid/graphprotocol-mainnet-docker) for deploying using Docker, if that's the route you want to go. If you want to use a hypervisor, or just deploy everything to one server (again, not recommended) then read on.

For a baremetal Graph Indexing operation you will want to try and separate your most resource-intensive loads either with separate physical servers or high performance servers using a hypervisor. A reasonable strategy is to use a KVM-based hypervisor which allows an admin to run certain loads as isolated virtual machines (KVM) and other, more basic loads as Linux containers (LXC/LXD). There are pros and cons to both options, however for your more intensive loads - your Ethereum node and your Postgres Database, it is strongly recommended to use physical servers if it fits your budget, but otherwise you definitely want to use virtual machines over Linux containers for these components. Physical servers/virtual machines have a number of benefits over containers including genuine resource isolation, direct mapping to physical CPUs and access to advanced CPU features that, due to the nature of Linux containers, cannot be used by an LXC. On the other hand, containers can share spare resources so are exceptionally efficient, highly scalable and easy to automate with very small footprints, so can be useful for components that need to scale horizontally, such as your graph nodes and indexer services. Depending on your own infrastucture and the performance of individual components, you may find that specific components required migration from container to VM if they become particularly resource-intensive e.g. when you have very high query load you might need to move your query nodes to a virtual machine.


## Graph Protocol Infrastructure Specs

Excluding the Ethereum node, the recommended total compute for the infrastructure is documented in the table below:

|         | Minimum Specs   | Recommended Specs | Maxed out Specs   |
|---------|-----------------|-------------------|-------------------|
| CPU     | 16 vcore        | 64 vcore          | 128 vcore         |
| RAM     | 32 GB           | 128 GB            | 256/512 GB        |
| Storage | 300 GB SATA SSD | 2TB (usable) NVME         | 4TB (usable) NVME RAID 10 |

(Table courtesy of @trader-payne at Stakesquid, see Stakesquid's Graph Protocol on Docker guide [here](https://github.com/StakeSquid/graphprotocol-testnet-docker))

How you choose to cut up the resources is up to you. Wavefive uses a spec similar to the reference architecture at the top of this document.

## Infrastructure components

### Graph nodes (container)
For the purposes of this guide we will deploy two graph nodes. Graph nodes can be scaled horizontally as needed, two will provide ample capacity for indexing multiple subgraphs.


### Query nodes (container)
For the purposes of this guide we will deploy one query node, however you can scale them horizontally with a loadbalancer if the level of query traffic demands it.


### Indexer agent (container)
You will only ever deploy one Indexer Agent per the current architecture.


### Indexer services (container)
For the purposes of this guide we will deploy two Indexer services with 6 worker threads each, and we will sit them behind an nginx load balancer. You can continue to scale indexer services horizontally as needed (node that horizontal scaling may not be required in the future - keep an eye on the [indexer](https://github.com/graphprotocol/indexer) repo updates.)

### Graph database (virtual machine, Postgres12)
32vcpu,16GB,1TB storage - you can start smaller than this but be prepared to expand resources if you do.

### Eth archive node (virtual machine, OpenEthereum/v3.0.1-stable-8ca8089-20200601) 
For Ethereum node specs, please refer to Stakequid's guide [here](https://github.com/StakeSquid/graphprotocol-testnet-docker#ethereum-archive-node-specs).

## Storage considerations
Storage performance requirements for the total infrastructure are high (SSD/nvme for the Eth node and database as a minimum.) More importantly, you need to consider your redundancy and backup strategy - the high performance storage is generally so expensive that full mirrored redundancy is prohibitively expensive. Wavefive uses ZFS for storage in nearly all cases, so the wording around redundancy will use ZFS nomenclature. Some strategies being used in production are described below.

### Graph Database (Virtual Machine)
Fastest, most redundant storage within budget. With a single database you will be constantly reading and writing to your main graph database. New subgraphs will be writing intensively as they churn through old blocks to sync the subgraph, existing synced subgraphs will be constantly working to stay at the chainhead and the database will be serving queries to your query node and out to your customers. The more you can reduce the latency within the database on the read side, the higher the utility of your queries served to your customer. During the Mission Control Testnet, which include ~60 subgraphs, the Postgres database was closing in on 2TiB total size, so if you plan to offer data for many subgraphs you can expect your database to have significant expansion needs on the storage front.

### Ethereum Node (Virtual Machine)
In order to support all types of subgraphs an Indexer needs access to an Ethereum Archive node with tracing. Usually this is an OpenEthereum 3.0.1 node. Using the fastest storage, many cpus and a lot of memory, this will take weeks to months to sync from scratch. As of early February 2021, an OE Archive node with tracing takes up 6.23TiB of storage. There are alternative third party options such as Infura, Alchemy, Chainstack and many others, but these services are relatively expensive compared to managing your own node - well over $1000 per month. Please see [this](https://github.com/StakeSquid/graphprotocol-testnet-docker#ethereum-archive-node-specs) guide for details on server spec for the node.

### Other components - graph-node, indexer-agent, indexer-service
Basic SSD storage will do here

## Redundancy and Disaster Recovery
Disk layer redundancy can be very expensive for the database and Ethereum node, because both require very fast storage in large quantities. Indexers will often sacrifice disk redundancy for total storage capacity and IOPS/throughput simply because of the huge performance and capacity requirements of an Ethereum Archive node with tracing. My recommendation would be to find a happy medium between ultimate disk redundancy and a battle-tested backup schedule that covers both the vm,container and applications layers - how you choose to add redundancy and disaster recovery features **will** have a significant impact on your business bottom line and the speed at which you can recover from a disaster.

Example minimum viable disk redundancy strategy
* Database, graph nodes, indexer agent, indexer service - 4x 2TB Gen3 nvme in a ZFS pool, RAID-Z2 (can withstand one disk failure out of the four in the pool, you could use Raid-Z but you are significantly increasing the risk that you have a failure during resilvering if you choose that configuration - it is not recommend for production use)
* Ethereum node - 8x 2TB Gen3 nvme in a ZFS pool, RAID0 (no disk-level redundancy, maximum performance - ideally this should be RAID-Z2 minimum (can withstand two disk failures out of the eight, if budget can stretch to it, but some choose to run the node without redundancy simply due to the sheer on-disk size of the database, and instead have a backup node in case of failure)

Note: Above is **minimum viable strategy.** The ideal local disk redundancy strategy would be full mirrors on Gen4 nvme, so a full disk set failure can be tolerated. However this is prohibitively expensive for the high performance storage needed for a lot of the Graph infrastructure. There are many other potential configurations, this is just one example.

Example minimum viable backup strategy
* Database, graph nodes, indexer agent, indexer service - Daily PGDump, Daily ZFS snapshots, weekly full (live) backups to a spinner (3 weeks of backups retained per vm/container), replicated to NAS - ideally, live backups should be daily if NAS capacity is available
* Ethereum node - Eth chain database rsync'd to NAS daily - future plans to do rsync via the rsync daemon (constantly syncing)

Example single-site catastrophic failure recovery
* Run two near-identical host servers, compute loads can be migrated between the servers using the Hypervisor. Automated migration and a shared SAN would be ideal to minimise recovery time, but not mandatory. Ideally (if your budget can stretch to it) a cluster of three servers running as a high availability cluster is the most resilient single-site configuration you can run as this allows highly reliable automated migration of applications between nodes in the cluster. This is achievable via various hypervisors including ESXi, Proxmox and XCP-NG.

