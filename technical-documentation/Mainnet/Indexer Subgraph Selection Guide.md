# Indexer Subgraph Selection Guide

{% hint style="info" %}
### Contributor Details

This documentation was contributed by [Jim Cousins](https://twitter.com/\_cryptovestor) as part of his work at The Graph Foundation. Thanks also to the following community members for peer review and other contributions to this article:

* Aderks @ Oracleminer
* Chris Wessels @ Graphops
* Gary Morris @ Staking facilities / 0xFury
* Juan Manuel Rodriguez Defago @ Bootnode
* Konstantin Zaitcev @ P2P
* Oliver Z @ The Graph Foundation
* Payne @ Stakesquid
{% endhint %}

## Indexer Subgraph Selection Guide

_**In this guide:**_

* Subgraph Selection: How Many Subgraphs Should an Indexer Serve?
  * Modelling Potential Revenue
  * Modelling on-chain Operational Expenses
* Subgraph Deployment Strategies
  * Weighting strategies for allocation
  * Weighting strategies for query revenue
  * Balancing Allocation Deployment versus Query Fee Revenue Share

### Subgraph Selection: How Many Subgraphs Should an Indexer Serve?

#### Modelling **Potential Revenue**

* How much revenue can an Indexer generate at a specific number of subgraphs
  * This is an Indexer-specific question, depending on two revenue streams:
    *   **Projected revenue from Staking Rewards:** Staking or Indexing rewards are heavily dependent upon the amount of GRT allocated within the network. The example tables below show how Indexer revenue can be impacted as a larger amount of the total GRT in the market enter the protocol and is allocated.

        ![Examples above show how effective network inflation rates impact Indexer revenue](<Indexer Subgraph Selection Guide/Untitled.png>)
* **Projected revenue from Query Business:** The Indexer's knowledge of the market's appetite for query business on subgraphs at a specific price or price range
  * This is challenging to project because the network does not openly share any information about the query demand within the network
  * Indexers have tools such as [Agora](https://github.com/graphprotocol/agora) to help understand how much query revenue they can make with a certain query cost model, however good projections require large volumes of real data in order to be useful
  * From those two revenue streams, how much is an Indexer willing to sacrifice to transaction fees
* Staking rewards will form the lion's share of the business in the early network stage, so initially they will largely be responsible for funding the transaction fees
* Query fees will build over time as the number of subgraphs on the network increases
  * The most effective (and therefore profitable) Indexers will understand the query market and other query mechanisms long before the network query volume begins to match the revenue generated via staking rewards
* Is it necessarily a sacrifice? Can those costs be claimed as a business cost or expense?
  * Entirely dependant on jurisdiction - consult your own Tax Advisor.
  * How does the total projected revenue impact overall subgraph selection?
* Early-stage subgraph selection outcomes are based largely on Indexer size (self stake and delegation), which drives total revenue potential
* Large self stake, large delegation → large stream of revenue generated via staking rewards → scope to support the costs of serving thousands of subgraphs
* Medium self stake, medium delegation → moderate stream of revenue via staking rewards → scope to support hundreds of subgraphs
* Small self stake, small delegation → low stream of revenue via staking rewards → scope to support less than one hundred subgraphs
* Things to consider depending on the size of your Indexing operation:
  * Smaller Indexers need to be conservative about subgraph selection, being sure to not over-extend, as to make their business unviable. In the short term this means focusing on optimising staking rewards, since the query market and number of subgraphs on the network is still in the growth phase.
  * The more that stake and delegation concentrates in the largest Indexers, the harder it will become for medium and small Indexers to run a viable business
    * This is mitigated by having many more subgraphs and query business in the network and ensuring that the largest Indexers understand their significant influence in the subgraph market and know how to apply that power in a positive way.

#### Modelling on-chain Operational Expenses

* In an ideal World all Indexers allocate to every subgraph
  * Serve more subgraphs, pull more query fees, make the maximum possible contribution to the network
* However the cost of doing business for an Indexer, beyond simple infrastructure and labor costs, is Ether - and Ether is a scarce resource and therefore relatively expensive.
* Indexers should choose a strategy wisely due to the expenses associated with each allocation - Ethereum Gas fees
  * Gas costs scale linearly with number of allocations.
    * The full lifecycle of one allocation includes four Ethereum transactions
      * AllocateFrom → CloseAllocation → Redeem → Claim
* **Average Graph Transaction Costs from a real Mainnet Indexing Operation**
  * Data comes from six months of Ethereum transaction data for Wavefive's indexing operation ([source](https://docs.google.com/spreadsheets/d/1zOtH7qGiSkN-IF-QUdt8MJp6Eh36ELDm\_OSNZwxPcjM/edit?usp=sharing))
  * Average total cost of all four transactions required for the full lifecycle of one allocation in the last six months - $77.75
  * Scaling up for more subgraphs and different monthly allocation lengths (assuming parallelAllocations=1): ![Modelling Indexer Transaction Costs](<Indexer Subgraph Selection Guide/Untitled 6.png>)
  * **The impact of Ether price and gas cost on Graph Indexing Business Decisions**
    * Although the above data is based on real transaction costs from a real Indexing operation, actual costs are entirely dependent on the price of Ether at the time of a transaction, and the current demand on the Ethereum network, so your mileage may vary. It is wise to have a reserve of Ether available to the business at all times, so the impact of Ether price fluctuations to your business can be mitigated to some degree.
    *   Oracleminer (aderks#7408 on Discord, [@MinerOracle](https://twitter.com/MinerOracle) on Twitter) provides a handy tool for predicting the cost of transactions [here](https://oracleminer.com/graph/indexer/0xbfe2a198cb0cdfb50fb03cd932c7387ddb0d25aa)

        ![Oracleminer's Graph Transaction costing tool](<Indexer Subgraph Selection Guide/Untitled 1.png>)
* Gas Price prediction tools
  * There are many gas price prediction tools out there. One of the most popular is [https://www.gasnow.org/](https://www.gasnow.org/) and you can use this tool to check demand, and therefore gas price, on the Ethereum network at any time.
  *   Many gas price tools also provide historical data, so you can plan out the most gas-efficient times to perform your on-chain Indexing operations.

      ![gasnow.org average historical gas price tool](<Indexer Subgraph Selection Guide/Untitled 2.png>)

#### Subgraph Deployment Strategies

* With consideration made for an Indexer's potential total monthly revenue and total potential on-chain transaction costs, let's consider what allocation deployment strategies an Indexer might apply once they know how many subgraphs they can support.
* The two basic revenue goals an Indexer can define for their operation are
  * Select subgraphs based on how much staking revenue can be generated from them
  * Select subgraphs based on how much query revenue can be generated from them
* The actual strategies that Indexers choose will vary, and in many circumstances will be a mix of a weighting strategy and some human intervention. This is especially likely the larger an Indexer is, where they have to be considerate about how they apply their large allocations to the network.
* The state of the network also plays a crucial role in what strategies an Indexer might pick. For example, in the early stages of the network when there is little signal and few subgraphs available, Indexers are likely to optimise for staking revenue over query revenue because they know that is the largest source of revenue until there are more subgraphs on the network.
* **Subgraph Selection for Staking Rewards**
  * It's important to note that the smaller an Indexer is in total stake (self stake + delegation) the easier it is to simply deploy the below strategies with very little pre-analysis of the network to avoid over-allocation, and therefore lower returns for all, on a subgraph. Large Indexers, in practice, need to be much more careful about analysing the existing allocations on a subgraph before choosing to allocate or they can negatively impact their own, as well as every other allocated Indexer's staking rewards.
    * Example from Konstantin Zaitcev, Engineer at [P2P.org](http://p2p.org):
      * "...it doesn't make sense for big Indexers to allocate somewhere, where available space is not so big. For example, even if I see 500k availability for allocation I can skip this subgraph. Because it will be unprofitable for us with daily re-allocations.
  * Stake weighting
    * What is stake weighting?
      * Building a subgraph selection model based on most profitable subgraphs for staking rewards by allocation state of the network
    * This is not as simple as "sort by stake allocated to a subgraph ascending and pick the top X"
    * Pros & Cons
      * Pros - At this early stage in the network, stake-weighting will produce the best return per GRT allocated when compared to other strategies. This is largely because the query side of the market is in a growth phase, while the staking side of the market is already in full swing, generating the majority of revenue for Indexer operations.
      * Cons - By following this strategy an Indexer is likely to have very poor performance KPIs on the query side of the market. This is because they are ignoring the need to balance their allocations against the query fees they generate, so they lose a very large proportion of the fees they charged for sending queries due the revenue share function. On mainnet we have observed Indexers losing up to 90% of their fees due to being stake-weighted, however the actual fees collected is only a small percentage of the staking rewards generated, so this is widely accepted as a reasonable tradeoff until query fees grow much larger.
    * How to stake-weight for subgraph selection
      * Calculate how many subgraphs you can support as per the _**Subgraph Selection: How Many Subgraphs Should an Indexer Serve?**_ section of this guide
      * Gather the following data about the network
        * Subgraphs deployed
        * GRT staked on the subgraph
        * Signalled tokens on the subgraph
        * Proportion of total network curation signal on the subgraph
        * Proportion of total network stake on the subgraph
        * Optimal total stake on the subgraph
        * GRT rewarded per GRT staked on the subgraph
        * The difference between the current and optimal stake on the subgraph
    * With the above information, the Indexer can assess which subgraphs are the most profitable to allocate to (GRT rewarded per GRT staked) **but more importantly,** by using the last statistic in the list, **difference between current and optimal stake on the subgraph,** the Indexer can assess if the subgraph is worth deploying their targeted amount of stake to.
    *   Example analysis

        ![Example subgraph analysis by stake-weighting](<Indexer Subgraph Selection Guide/Untitled 3.png>)
* The table has been sorted by potential rewards per 1M GRT allocated
* Notice how three subgraphs in particular are more profitable to stake on in the current network state
* Notice how adding your own stake to each subgraph will change how profitable it is
  * For this very reason, the larger an Indexer, the closer they might bring a profitable subgraph into or beyond **optimal staking.** By allocating beyond the optimal staking number, the Indexer will impact both their own profitability and that of every other Indexer allocated to that subgraph.
  * Effective Indexers with a large proportion of the total network stake take stake-weighted optimisation very seriously because they understand how their subgraph selection decisions can impact everyone, both positively and negatively.
  * Signal weighting
  * What is signal-weighting?
* Building a subgraph selection model based on the highest signalled subgraphs across the network, allocating a larger proportion of stake to the highest signalled subgraphs
  * Signal on the network is supposed to help an Indexer decide which subgraphs are the most valuable to Index and serve queries for. By following signal weightings closely, the Indexer is assuming/expecting that the curation signal will be followed by most Indexers, meaning that the overall network will generally be in equilibrium with regards to stake optimisation.
  * Pros & Cons
* Signal weighting is not effective for large indexers when followed exactly, especially when there are very few subgraphs in the network, because of the reasons stated in the stake-weighting section - blindly applying a large stake via signal weighting could negatively impact revenue for all Indexers.
* For small Indexers, signal-weighting can be a very effective way of trying to capture both a good share of the staking rewards, and an effective way of mitigating some of the issues explained for stake-weighting, where as much as 90% of an Indexer's query fees can end up being lost to the revenue share pool, because most Indexers are stake-weighting. This puts smaller Indexers in a good position in terms of demonstrating how they are supporting the network both on the stake and the fee side as best they can in the early stages of the network.
  * How to signal-weight for subgraph selection
* Calculate how many subgraphs you can support as per the _**Subgraph Selection: How Many Subgraphs Should an Indexer Serve?**_ section of this guide
* Gather the following data about the network
  * Subgraphs deployed
  * Signalled tokens on the subgraph
* With the above information and Indexer can sort the data by signalled tokens descending and divide their total stake across each selected subgraph in proportion to its signalled tokens.
  * Signal on as many of the high signal subgraphs as is practical in terms of transaction costs
  * In the early stages of the network, unless everyone is signal-weighting, large Indexers cannot stick to signal weighted decisions alone - this is due to the reasons explained at the start of this section - very large allocations can have a negative impact on overall profitability on a subgraph if the large Indexer isn't also considering the optimal stake scenario.
*   Example analysis

    ![Example subgraph analysis by signal-weighting](<Indexer Subgraph Selection Guide/Untitled 4.png>)
* The table has been sorted by Signal % total, from largest signal to smallest
* The higher the signal on a subgraph, the larger proportion of your stake should be allocated to it
  * Other stake-related strategies
  * Query Fee weighting (demand for query business on a subgraph based on historical fees collected)
* Weighting each subgraph allocation so that the Indexer deploys the most stake to the subgraphs with the highest demand for query business
* This strategy is unlikely to offer comparable returns to stake-weighting or even signal-weighting in the early growth stage of the subgraph market
* If the query fee market revenue grows to rival and exceed the staking revenue market, finding a balance between query fee weighting and stake/signal-weighting will likely become a more popular strategy for maximising Indexer return and maximising contributions to the network (see follow-on section on strategies for the future)
* The process of gathering the data for this strategy is more complex than other strategies outlined so far and may be a topic for a second version of this guide.
* **Subgraph Selection for query revenue**
  * Optimising for query revenue share
    * Once the Indexer knows the amount of query fees they are capturing per subgraph on average, they can tune the ratio between the query fees and the GRT allocation to each subgraph being served, in order to maximise the amount of GRT they receive from the revenue share function
    * Indexers needs to work together on improving the ratio of total fees to total GRT allocated to a subgraph, in order that everyone sees improved rebates from the revenue share function
    *   Indexers with very large stake compared to an average Indexer can have severe negative impact on everyone's rebates if their cost models are not tuned correctly.

        ![A basic example of the Revenue Share function, demonstrating how a very large Indexer can have a profoundly negative impact on the returns of smaller Indexers, while taking more than their "fair" share of the rebate pool and burning a large amount of fees at the same time.](<Indexer Subgraph Selection Guide/Untitled 5.png>)
* The reality of migration is that this imbalance is going to continue until there are significantly more subgraphs in the network and significantly more demand for query business.

#### Selection Strategies for the Future

* Balancing Allocation Deployment versus Query Fee Revenue Share
  * As described earlier, there are two sides to the revenue opportunity for Indexer - Staking rewards and Query fees.
  * In a perfect world, an Indexer will find a perfect balance between optimising staking rewards and optimising query fee rebates.
  * Optimizing for only one side of the revenue opportunity means sacrificing revenue on the other side. In the long-term, an effective Indexer will optimize for both.
  * In the early stages of the network, query fee revenue is significantly out-matched by indexerRewards
    * This means that Indexers that have the sole objective of maximising profit will be optimising for indexerRewards (staking rewards) rather than queryFees.
    * Indexers trying to support the query fee side of the market, via signal-weighting or other method, will likely be trading some revenue on the staking reward side for better overall performance on the query fee side.
