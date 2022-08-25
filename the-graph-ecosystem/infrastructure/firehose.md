# Firehose

A Firehose is a gRPC service providing an ordered, yet fork-aware, stream of blocks, developed by The Graph's core developers to better support performant indexing at scale. This is not currently an indexer requirement, but Indexers are encouraged to familiarise themselves with the technology, ahead of full network support. Learn more here: [Firehose Documentation by Streamingfast](https://firehose.streamingfast.io/introduction/firehose-overview).&#x20;

### Purpose

#### What is it?

Firehose is a core component of StreamingFast’s suite of open-source blockchain technologies.

#### Streaming-first & Files-based

Firehose provides a files-based and streaming-first approach to processing blockchain data.&#x20;

#### Blockchain Data Extraction

Firehose is responsible for extracting data from blockchain nodes in a highly efficient manner. Firehose also consumes, processes, and streams blockchain data to consumers of nodes running Firehose-enabled, instrumented blockchain client software.

#### Speed Increases Across Blockchains

Firehose makes paramount improvements in the speed and performance of data availability for _any blockchain_.

The full [StreamingFast software suite](https://github.com/streamingfast) enables low-latency processing of real-time blockchain data in the form of binary data streams. [Substreams](https://substreams.streamingfast.io/) is another application in the suite that works with Firehose to execute massive operations on historical blockchain data, in an _extremely parallelized manner_.

### Motivation

#### Why does it exist?

Firehose was created to increase the speed and performance of blockchain data extraction from problems encountered in deployed, real-world applications.&#x20;

#### Firehose Prevents Downtime

Companies experienced up to three week-long periods of downtime due to the reprocessing of blockchain data in a linear fashion. Firehose was designed for highly efficient parallelized node data processing, at a massively large scale, circumventing these unwanted and problematic downtimes.

#### Unrivaled Blockchain Data Processing Speeds

Firehose was designed to process blockchain at speeds that were previously unseen and _thought to be impossible_.&#x20;

#### Resolving Slow JSON-RPC Responses

Another factor that heavily contributed to the design of Firehose is the brittleness and slow response times of, often inconsistent, JSON-RPC systems.

### Capabilities

#### How it works

The Firehose instrumentation service is added to a node for efficient capture and simple storage of blockchain data.&#x20;

#### Data Extraction, Storage, & Access

Firehose extracts, transforms and saves blockchain data in a highly performant file-based strategy. Blockchain developers can then access data extracted by Firehose through binary data streams.

#### Firehose Single Source of Truth (SSOT)

Firehose provides a single source of truth for developers looking to utilize blockchain data for their blockchain application development efforts.

#### The Graph & Firehose

Firehose is intended to stand as a replacement for The Graph’s original blockchain data extraction layer. [The Graph](https://thegraph.com/) is an indexing protocol used for the organization of blockchain data.

#### Technical Overview

To get started with Firehose, the first step is to learn about its core [concepts and technical architecture](broken-reference).&#x20;

#### Existing Firehose Users

Experienced node operators can get up and running by using one of the pre-instrumented blockchain node codebases provided by StreamingFast. Look in the [Firehose Setup ](broken-reference)section of the Firehose documentation for further information.

#### Custom Firehose Setups & New Chains

Lastly, developers can learn how to implement custom Firehose nodes in the [Integrate new chains](broken-reference) section of the Firehose documentation.

