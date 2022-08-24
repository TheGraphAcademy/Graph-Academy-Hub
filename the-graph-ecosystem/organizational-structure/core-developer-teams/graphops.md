# GraphOps

[GraphOps](https://graphops.xyz/) is a blockchain data infrastructure company. They extract, transform and serve blockchain data. They’re driven by the mission to build an uncensorable, equitable and self-sovereign web. Public data is at the heart of that mission, and they thrive on building open data standards and protocols to empower the next great wave of institutions and applications for the world.

GraphOps contributes to The Graph ecosystem in key areas: Protocol Economics & Network Operations, Core Development of a Gossip Client and network, and Indexer Experience.

The GraphOps team brings together a wealth of experience inside and outside of The Graph ecosystem, spanning across protocol design, economics, infrastructure and systems orchestration. They are proven indexing experts, having been active members of the community since the testnet. Their work will expand the quality of service and capacity of The Graph Network and the capabilities of Indexers as the decentralized network scales.

Chris Wessels is joined by Juan Manuel Rodriguez Defango, Ana Maria Calin, Abel Tedros, and Petko Pavlovski. Their years of contribution to The Graph ecosystem gives them the depth of experience and firsthand knowledge of the protocol to provide best-in-class resources and tooling to optimize Indexer experience.

### Expanding impact across the ecosystem in three main areas

GraphOps has long contributed to The Graph ecosystem, making a significant push to expand resources, information, and education. GraphOps provides a range of support, education, and the development of technology and tooling for Indexers in The Graph ecosystem. As a core developer, GraphOps is scaling their impact across three critical areas:

#### 1. R\&D: Protocol Economics and Network Operations

Protocol Economics and Network Operations are both active areas of research in The Graph ecosystem. Protocol Economics is a focus area that relates to the design of incentives of the protocol, while Network Operations is a focus area that advances the instantiation, maintenance, and optimization of the different subsystems of the protocol.

These areas of research are being advanced by a multidisciplinary group with expertise spanning across engineering, product, user experience, economics and AI. GraphOps’ research and development work contributes to evolving the mechanisms by which the protocol drives behavior and coordinates participants. Those active areas of research are:

**Improvements to Subgraph Curation**

At a high level, Curators signal their belief in the quality of a particular subgraph and its ability to attract future query fees from data consumers in the network by depositing $GRT in return for curation shares.

Dapp developers rely on subgraphs to serve data to their end-users. Curators are economically incentivized to play the vital role of signaling which subgraphs are worth indexing. The more a subgraph is indexed by a diverse set of Indexers, the more reliable a subgraph becomes, making it easier for dapp developers to expand their use of subgraphs in their application. Curators influence the process of allocating indexing resources on the network.

Main characteristics of Curation V2:

* **Reducing complexity:** The bonding curves used in the current design add some cognitive overhead for the user, the next set of Curator improvements are also aimed at simplifying the user experience.
* **Improving Curation Economics:** Curation V2 proposals will focus on reducing or removing the risks for late market entrants, as well as potentially adding “initialization periods” to those markets, to ensure proper curation can be done.
* **Reducing Risk & Increasing the Value of Signals:** These upgrades will target increased market safety to reduce the risk of principal loss in bonding curves.

**Epoch Block Oracle**

The Epoch Block Oracle (EBO) is a crucial tool for The Graph’s decentralized network expansion to indexing additional chains.

The (EBO) unlocks POIs (Proof of Indexing) for other chains. It provides a canonical reference on Ethereum mainnet for all Indexers to agree which block hash on a foreign chain they should use when constructing a POI. This brings the same economic data integrity guarantees that exist on Ethereum mainnet to other chains. With that security in place, Indexing Rewards for other chains can also be enabled, which creates incentives for Indexers to bootstrap supply-side capacity of the query market, ensuring that there is a good quality of service for EBO subgraphs.

GraphOps is working closely with Edge & Node to deliver the Epoch Block Oracle, with a particular focus on the associated subgraph, which provides the read interface for the Oracle. Under the hood, the subgraph indexes the compressed and encoded binary payloads submitted to the EBO’s [Data Edge contract](https://forum.thegraph.com/t/gip-0025-dataedge/3161).

#### 2. Core Development

GraphOps will lead and support several core development initiatives. This scope includes development and maintenance of core network subgraphs, smart contract development, and support and building out a Gossip Network for Indexers.

**Core Network Subgraphs**

The GraphOps team develops and maintains the core network subgraphs. These subgraphs index and describe the state of The Graph Network contracts on Ethereum mainnet. They are systemically important to the functioning of the network, being depended on by key components such as the gateways and Indexer software stack.

These subgraphs include:

* The **network subgraph**, which holds all of the relevant data for the protocol, which would include the state of all participants, as well as subgraphs, global parameters and more.
* The **network analytics subgraph**, which is a smaller version of the network subgraph, but with added daily data points for relevant entities, such as Indexers, Delegators, Subgraph Deployments and global metrics.
* The **billing subgraph**, which keeps track of billing related data (currently on Polygon)
* The **activity feed subgraph**, which keeps track of all events that happen within the protocol, for easier accessibility.

GraphOps will continue these efforts as well as create and contribute to other core subgraphs, refactor out technical debt, and add test coverage to subgraphs via [Matchstick](https://thegraph.com/docs/en/developer/matchstick/) to meet the needs of the growing network.

**Gossip Network**

GraphOps is also working on a Gossip Network—a decentralized, distributed peer-to-peer (P2P) communication tool that allows Indexers across the network to exchange information in real-time. Today, network participants coordinate with one another using the protocol by submitting on-chain transactions. These transactions cost gas on the Ethereum network. This means sending signals to other participants in the network has a relatively high cost that is determined by the cost of transacting on the Ethereum blockchain.

The purpose of the Gossip Network is to unlock a new design space for coordination as a complementary resource to the protocol. If Indexers run the additional Gossip Client component alongside their existing indexing software stack, they can communicate with each other over a P2P network, sending cryptographically signed messages to one another.

There are a number of promising use cases for this technology, including but not limited to:

* **Realtime cross-checking of POIs:** Realtime cross-checking of POIs with all other participating Indexers, constructing a stake weighted view of POI consensus. This would allow an Indexer to rapidly opt out of serving erroneous data to a consumer in the event of diverging from the consensus POI.
* **Reporting of query and indexing analytics:** Indexers could self-report query analytics (request volume, fees, top query shapes, etc) and indexing analytics (handler gas consumption, total sync time, indexing errors, etc) for aggregation and analysis.
* **Facilitating rapid sync negotiations:** Indexers could coordinate and negotiate with other Indexers to bootstrap their initial dataset, across subgraphs, Substreams flat files and Firehose flat files.

Each of these use cases can be built as a pluggable module. These modules will have no dependency on any sort of centralized reporting or aggregation server, and all participants will have free and permissionless access to the data passing through the Gossip Network.

#### 3. Indexer experience

As more subgraphs move to the decentralized network, multi-chain support expands and [Firehose rolls out](https://thegraph.com/blog/substreams-parallel-processing), Kubernetes will be an essential tool for Indexers of all sizes. GraphOps will provide the resources and tools for all indexers to use Kubernetes, preparing them to support the growth of the decentralized network as it scales regardless of their infrastructure setup.

GraphOps will release open source tooling to orchestrate, monitor and scale the Indexing stack and its dependencies on top of Kubernetes, as well as documentation and workshops to support an excellent ease of use for Indexers following this approach.

**Making Kubernetes more accessible to Indexers**

Many Indexers on the decentralized network use their own hardware, or simply don’t wish to depend on a large managed infrastructure provider such as AWS or GCP. This rules out managed Kubernetes offerings, and increases the barrier to entry for Indexers wanting to take advantage of Kubernetes on their own terms.

GraphOps is developing tooling to deploy and manage Kubernetes across any hosts that an Indexer has at their disposal, joining them into a cluster. Alongside documentation and workshops, this paves the way for more Indexers to reap the benefits of adopting Kubernetes.

**Improving the UX of indexing inside Kubernetes**

GraphOps is creating tooling to deploy the different components that make up The Graph stack, in a fully configurable, scalable and highly available way. This will enable indexers to easily deploy the indexing stack into their own Kubernetes cluster.

This work offers a strong alternative to the existing [docker compose graph-node](https://github.com/graphprotocol/graph-node/blob/master/docker/docker-compose.yml) configuration that many Indexers rely upon. Whilst this setup has its benefits and has provided operators a standardized way to deploy the different application components that make up graph-node, its use is limited to running multiple containers on the same host. Moving from Docker Compose to Kubernetes will enable indexers to effortlessly scale up their infrastructure to add more hosts, regardless of provider - cloud, bare-metal or on-prem - to meet demand as needed.

As Firehose and Substreams mature to become core components of the Indexing stack, GraphOps will also ensure that there is a smooth, well documented path for operating these systems and their dependencies in Kubernetes.

#### Additional ecosystem support

Using the depth and breadth of their experience, GraphOps will continue to offer a range of information and documentation to lower the barriers and provide support at all levels of the ecosystem, from novices to veterans.

GraphOps already plays a key role engaging with the community, now adding a particular focus on bringing more Indexers into the ecosystem while educating and raising the bar for indexing, enabling greater heights of network quality of service. They are also maximizing the value of the feedback loop between Indexers and core contributing teams.

**Indexer Office Hours**

GraphOps has been active in the ecosystem since 2020, operating resources like Indexer Office Hours (IOH), a weekly hour-long discussion on Discord to support Indexers. IOH is the go-to resource for Indexers to share knowledge, build relationships and keep up to date on all the relevant developments in The Graph ecosystem. GraphOps have already participated in 66 IOH sessions and the team now orchestrates all the sessions, all of which are available on [YouTube](https://www.youtube.com/channel/UCQ7G\_cCufIVUdUUUf-jdoVA/videos).

All Indexers are advised to follow IOHs to stay on top of the latest protocol updates, repos, and to [join the discussion](https://forum.thegraph.com/t/indexer-office-hours/1270).

**Follow all the contributions and developments from GraphOps:**

To stay current on GraphOps contributions to The Graph ecosystem, follow [GraphOps on Twitter](https://twitter.com/graphopsxyz), [The Graph on Twitter](https://twitter.com/graphprotocol), and join the conversation on The Graph Forum: [forum.thegraph.com](https://forum.thegraph.com/)

Follow all the latest ecosystem news, updates, and discussions in [The Graph Discord](http://discord.gg/vtvv7FP).

###
