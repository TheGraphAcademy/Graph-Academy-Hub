# Query the Hosted Service

With the subgraph deployed, visit the [Hosted Service](https://thegraph.com/hosted-service/) to open up a [GraphiQL](https://github.com/graphql/graphiql) interface where you can explore the deployed GraphQL API for the subgraph by issuing queries and viewing the schema.

An example is provided below, but please see the [Query API](https://thegraph.com/docs/en/developer/graphql-api/) for a complete reference on how to query the subgraph's entities.

**Example**

This query lists all the counters our mapping has created. Since we only create one, the result will only contain our one `default-counter`:

```
{  counters {    id    value  }}
```

### Using The Hosted Service <a href="#using-the-hosted-service" id="using-the-hosted-service"></a>

The Graph Explorer and its GraphQL playground is a useful way to explore and query deployed subgraphs on the Hosted Service.

Some of the main features are detailed below:

![Explorer Playground](https://thegraph.com/docs/img/explorer-playground.png)

***

[\
](https://thegraph.com/docs/en/hosted-service/deploy-subgraph-hosted/)
