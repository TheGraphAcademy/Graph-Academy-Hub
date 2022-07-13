# Subgraph Studio FAQs

#### 1. How do I create an API Key? <a href="#1-how-do-i-create-an-api-key" id="1-how-do-i-create-an-api-key"></a>

In the Subgraph Studio, you can create API Keys as needed and add security settings to each of them.

#### 2. Can I create multiple API Keys? <a href="#2-can-i-create-multiple-api-keys" id="2-can-i-create-multiple-api-keys"></a>

A: Yes! You can create multiple API Keys to use in different projects. Check out the link [here](https://thegraph.com/studio/apikeys/).

#### 3. How do I restrict a domain for an API Key? <a href="#3-how-do-i-restrict-a-domain-for-an-api-key" id="3-how-do-i-restrict-a-domain-for-an-api-key"></a>

After creating an API Key, in the Security section, you can define the domains that can query a specific API Key.

#### 4. Can I transfer my subgraph to another owner? <a href="#4-can-i-transfer-my-subgraph-to-another-owner" id="4-can-i-transfer-my-subgraph-to-another-owner"></a>

Yes, subgraphs that have been published to Mainnet can be transferred to a new wallet or a Multisig. You can do so by clicking the three dots next to the 'Publish' button on the subgraph's details page and selecting 'Transfer ownership'.

Note that you will no longer be able to see or edit the subgraph in Studio once it has been transferred.

#### 5. How do I find query URLs for subgraphs if I’m not the developer of the subgraph I want to use? <a href="#5-how-do-i-find-query-ur-ls-for-subgraphs-if-i-m-not-the-developer-of-the-subgraph-i-want-to-use" id="5-how-do-i-find-query-ur-ls-for-subgraphs-if-i-m-not-the-developer-of-the-subgraph-i-want-to-use"></a>

You can find the query URL of each subgraph in the Subgraph Details section of The Graph Explorer. When you click on the “Query” button, you will be directed to a pane wherein you can view the query URL of the subgraph you’re interested in. You can then replace the `<api_key>` placeholder with the API key you wish to leverage in the Subgraph Studio.

Remember that you can create an API key and query any subgraph published to the network, even if you build a subgraph yourself. These queries via the new API key, are paid queries as any other on the network.
