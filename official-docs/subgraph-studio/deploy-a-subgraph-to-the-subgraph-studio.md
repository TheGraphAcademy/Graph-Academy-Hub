# Deploy a Subgraph to the Subgraph Studio

Deploying a Subgraph to the Subgraph Studio is quite simple. This will take you through the steps to:

* Install The Graph CLI (with both yarn and npm)
* Create your Subgraph in the Subgraph Studio
* Authenticate your account from the CLI
* Deploying a Subgraph to the Subgraph Studio

### Installing Graph CLI <a href="#installing-graph-cli" id="installing-graph-cli"></a>

We are using the same CLI to deploy subgraphs to our [hosted service](https://thegraph.com/hosted-service/) and to the [Subgraph Studio](https://thegraph.com/studio/). Here are the commands to install graph-cli. This can be done using npm or yarn.

**Install with yarn:**

```
yarn global add @graphprotocol/graph-cli
```

**Install with npm:**

```
npm install -g @graphprotocol/graph-cli
```

### Create your Subgraph in Subgraph Studio <a href="#create-your-subgraph-in-subgraph-studio" id="create-your-subgraph-in-subgraph-studio"></a>

Before deploying your actual subgraph you need to create a subgraph in [Subgraph Studio](https://thegraph.com/studio/). We recommend you read our [Studio documentation](https://thegraph.com/docs/en/studio/subgraph-studio/) to learn more about this.

### Initialize your Subgraph <a href="#initialize-your-subgraph" id="initialize-your-subgraph"></a>

Once your subgraph has been created in Subgraph Studio you can initialize the subgraph code using this command:

```
graph init --studio <SUBGRAPH_SLUG>
```

The `<SUBGRAPH_SLUG>` value can be found on your subgraph details page in Subgraph Studio:

![Subgraph Studio - Slug](https://thegraph.com/docs/img/doc-subgraph-slug.png)

After running `graph init`, you will be asked to input the contract address, network, and ABI that you want to query. Doing this will generate a new folder on your local machine with some basic code to start working on your subgraph. You can then finalize your subgraph to make sure it works as expected.

### Graph Auth <a href="#graph-auth" id="graph-auth"></a>

Before being able to deploy your subgraph to Subgraph Studio, you need to login into your account within the CLI. To do this, you will need your deploy key that you can find on your "My Subgraphs" page or your subgraph details page.

Here is the command that you need to use to authenticate from the CLI:

```
graph auth --studio <DEPLOY KEY>
```

### Deploying a Subgraph to Subgraph Studio <a href="#deploying-a-subgraph-to-subgraph-studio" id="deploying-a-subgraph-to-subgraph-studio"></a>

Once you are ready, you can deploy your subgraph to Subgraph Studio. Doing this won't publish your subgraph to the decentralized network, it will only deploy it to your Studio account where you will be able to test it and update the metadata.

Here is the CLI command that you need to use to deploy your subgraph.

```
graph deploy --studio <SUBGRAPH_SLUG>
```

After running this command, the CLI will ask for a version label, you can name it however you want, you can use labels such as `0.1` and `0.2` or use letters as well such as `uniswap-v2-0.1`. Those labels will be visible in Graph Explorer and can be used by curators to decide if they want to signal on this version or not, so choose them wisely.

Once deployed, you can test your subgraph in Subgraph Studio using the playground, deploy another version if needed, update the metadata, and when you are ready, publish your subgraph to Graph Explorer.

\
