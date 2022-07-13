---
description: >-
  Documentation for Indexers how to get subgraph's ipfs hash from id and vise
  versa
---

# IPFS hash converter

## Getting id from ipfs hash

*   Transform id to ipfsh hash using python:

    ```
    $ pip install base58
    $ python
       print("0x"+base58.b58decode("ipfs_hash").hex()[4:])
    ```

## Getting ipfs from id

*   Get id using graphql request

    ```
    query {
      subgraphDeployments {
        id
      }
    }
    ```
*   Transform ipfs hash to id using python

    ```
    $ pip install base58
    $ python
       print(base58.b58encode(bytes.fromhex("1220"+"subgraph_id"[2:])).decode('utf-8'))
    ```

## Scripts and links

* You can use python script which located [here](https://github.com/StakeSquid/graphprotocol-testnet-docker/blob/master/subgraph\_convert.py)
* Online tool also available [here](https://incoherency.co.uk/base58/)
* Some techical overview available [here](https://ethereum.stackexchange.com/questions/17094/how-to-store-ipfs-hash-using-bytes32)
