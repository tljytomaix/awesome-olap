<div align="center">

# Awesome OLAP [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[![Awesome OLAP](https://img.shields.io/badge/awesome--olap-reference-blue)](https://github.com/samber/awesome-olap)

</div>

A curated list of **OLAP databases**, **data engineering** tools, **columnar databases**, **data lake** and **lakehouse** frameworks — covering 100+ tools across 20+ categories, for data engineers.

> **OLAP** (Online Analytical Processing) refers to databases and query engines optimized for complex, read-heavy analytical queries over large datasets. Unlike OLTP systems, OLAP databases use columnar storage, vectorized execution, and distributed processing to aggregate and analyze billions of rows in seconds.

See also:

- [awesome-ai-native](https://github.com/samber/awesome-ai-native) - Products where the LLM is the product itself.
- [awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) - Collection of Prometheus alerting rules.
- [awesome-user-research](https://github.com/samber/awesome-user-research) - Tools for Product Managers and UX Researchers.

## Contents

<!--lint disable awesome-list-item-->
- [OLAP Databases](#olap-databases)
  - [Real-time analytics](#real-time-analytics)
  - [Search engines](#search-engines)
  - [Hybrid OLAP/OLTP NewSQL (aka HTAP)](#hybrid-olapoltp-newsql-aka-htap)
  - [Timeseries](#timeseries)
  - [Managed cloud services](#managed-cloud-services)
- [Storage engines](#storage-engines)
- [Data lake](#data-lake)
  - [File formats and serialization](#file-formats-and-serialization)
  - [Open table formats](#open-table-formats)
  - [Metastore](#metastore)
  - [Object Storage](#object-storage)
  - [Codecs, encoding and compression](#codecs-encoding-and-compression)
- [Brokers and distributed messaging](#brokers-and-distributed-messaging)
- [Ingestion and querying](#ingestion-and-querying)
  - [Stream processing](#stream-processing)
  - [Batch processing](#batch-processing)
  - [In-memory processing](#in-memory-processing)
  - [Distributed SQL processing](#distributed-sql-processing)
- [Scheduler](#scheduler)
- [Durable execution](#durable-execution)
- [ETL, ELT and reverse ETL](#etl-elt-and-reverse-etl)
- [BI & Visualization](#bi--visualization)
- [Datasets](#datasets)
- [Benchmark](#benchmark)
- [Readings](#readings)
  - [Papers](#papers)
  - [Architecture](#architecture)
  - [Data modeling](#data-modeling)
  - [Index](#index)
  - [Vector similarity search](#vector-similarity-search)
  - [Vectorized query processing](#vectorized-query-processing)
  - [Querying](#querying)
  - [Transactions](#transactions)
  - [Consensus](#consensus)
  - [Challenging platforms](#challenging-platforms)
  - [Blogs to follow](#blogs-to-follow)
  - [More](#more)
- [FAQ](#faq)
- [People to follow](#people-to-follow)
- [Events](#events)
- [Communities](#communities)
- [🤝 Contributing](#-contributing)
- [👤 Contributors](#-contributors)
- [💫 Show your support](#-show-your-support)
- [📝 License](#-license)
<!--lint enable awesome-list-item-->

## OLAP Databases

### Real-time analytics

The following columnar databases use a [shared-nothing architecture](https://en.wikipedia.org/wiki/Shared-nothing_architecture) and provide a sub-second response time. DDL, DML and DCL are operated via SQL. These databases also support tiering for long-term cold storage.

- [Apache Doris](https://doris.apache.org/) - MPP analytical database with MySQL-compatible interface, optimized for high-concurrency queries and real-time data ingestion.
- [Apache Druid](https://druid.apache.org/) - Real-time OLAP database optimized for streaming ingestion, time-series analytics, and sub-second queries on high-cardinality data.
- [Apache HBase](https://hbase.apache.org/) - Distributed, wide-column NoSQL database on top of HDFS, modeled after Google Bigtable.
- [Apache Pinot](https://pinot.apache.org/) - Distributed OLAP datastore for user-facing real-time analytics, designed for low-latency queries at high concurrency.
- [ClickHouse](https://clickhouse.com) - Column-oriented DBMS for online analytical processing, capable of processing billions of rows per second.
- [StarRocks](https://www.starrocks.io/) - MPP OLAP database with vectorized execution engine, optimized for real-time analytics and high-concurrency workloads.

### Search engines

Search engines complement OLAP systems for full-text search and log analytics use cases, where keyword relevance and inverted indexes matter more than aggregate query performance.

- [Elasticsearch](https://www.elastic.co/) - Search and analytics engine based on Apache Lucene.
- [Meilisearch](https://www.meilisearch.com/) - Open source search engine, that aims to be a ready-to-go solution.
- [OpenSearch](https://opensearch.org/) - Apache 2.0 fork of Elasticsearch.
- [Quickwit](https://quickwit.io/) - Search engine on top of object storage, using shared-everything architecture.
- [Typesense](https://typesense.org/) - Open-source, typo-tolerant search engine optimized for instant search-as-you-type experiences and developer productivity.

### Hybrid OLAP/OLTP NewSQL (aka HTAP)

HTAP (Hybrid Transactional-Analytical Processing) databases handle both transactional writes and analytical reads in a single engine, eliminating the need to maintain a separate data warehouse for reporting.

- [Citus](https://www.citusdata.com/) - PostgreSQL compatible distributed table.
- [CockroachDB](https://www.cockroachlabs.com/) - Distributed SQL database with strong consistency, horizontal scaling, and PostgreSQL compatibility for HTAP workloads.
- [TiDB](https://github.com/pingcap/tidb) - MySQL compatible SQL database that supports hybrid transactional and analytical processing workloads.
- [YugabyteDB](https://www.yugabyte.com/) - Distributed SQL database compatible with PostgreSQL and Cassandra APIs, designed for global, cloud-native HTAP applications.

### Timeseries

Time-series databases are optimized for append-heavy workloads where data is tagged, timestamped, and queried by time range — distinct from general OLAP because they prioritize ingestion throughput, automatic retention, and time-aligned aggregations.

- [Grafana Mimir](https://grafana.com/oss/mimir/) - Prometheus-compatible TSDB on top of object storage, horizontally scalable.
- [InfluxDB](https://www.influxdata.com/) - Purpose-built time series database optimized for high-write-throughput metrics, events, and IoT data with a SQL-like query language.
- [Prometheus](https://prometheus.io/) - Pull-based metrics collection and time series database, de facto standard for cloud-native monitoring.
- [QuestDB](https://questdb.io/) - High-performance time series database written in Java and C++, with SQL support and ingestion rates exceeding millions of rows per second.
- [TimeScaleDB](https://www.timescale.com/) - PostgreSQL-compatible TSDB with automatic partitioning and time-series-specific SQL extensions.
- [VictoriaMetrics](https://victoriametrics.com/) - Fast, cost-effective Prometheus-compatible TSDB with low memory and storage footprint.

### Managed cloud services

Fully managed cloud data warehouses trade self-hosted operational overhead for elastic scaling and pay-as-you-go pricing. All handle petabyte-scale analytics; they differ in cost model, latency profile, and ecosystem integrations.

- [AWS Redshift](https://aws.amazon.com/redshift/) - Fully managed petabyte-scale data warehouse on AWS.
- [Azure Synapse Analytics](https://azure.microsoft.com/en-us/products/synapse-analytics) - Unified analytics service combining data integration, warehousing, and big data on Azure.
- [Databricks](https://www.databricks.com/) - Lakehouse platform combining data warehousing and ML, built on Delta Lake and Apache Spark.
- [Firebolt](https://www.firebolt.io/) - Cloud-native OLAP warehouse engineered for sub-second query performance at scale.
- [Google BigQuery](https://cloud.google.com/bigquery) - Serverless, pay-as-you-go data warehouse with built-in ML and BI capabilities.
- [Snowflake](https://www.snowflake.com/en/) - Cloud data platform with a decoupled storage and compute architecture, supporting multi-cloud deployments.
- [Tinybird](https://www.tinybird.co/) - Real-time analytics API platform built on ClickHouse.

## Storage engines

Storage engines are the foundational frameworks on top of which higher-level databases and data systems are built. They handle durability, transactions, and low-level data organization.

- [FoundationDB](https://www.foundationdb.org/) - Distributed ordered key-value store with full ACID transactions, designed as a reliable foundation layer for building higher-level databases and services.
- [LevelDB](https://github.com/google/leveldb) - Google's embeddable key-value store using a log-structured merge-tree (LSM-tree); the inspiration for RocksDB and widely used in Blockchain and embedded systems.
- [RocksDB](https://rocksdb.org/) - Embeddable persistent key-value store by Meta, optimized for fast storage and used as the storage engine inside many distributed databases (TiKV, CockroachDB, Kafka).

## Data lake

The data lake approach (or "lakehouse") is a semi-structured schema that sits on top of object storage in the cloud.

It is composed of a few layers (from lower to higher level): codec, file format, table format + metastore, and the ingestion/query layer.

### File formats and serialization

These formats are popular for shared-everything databases, using object storage as a persistence layer. The data is organized in row or column, with strict schema definition. These files are immutable and offer partial reads (only headers, metadata, data page, etc). Mutation requires a new upload. Most formats support nested schema, codecs, compression, and data encryption. Index can be added to file metadata for faster processing.

A single file can weight between tens of MB to a few GB. Lots of small files require more merge operation. Larger files can be costly to update.

- [Apache Arrow Columnar Format](https://arrow.apache.org/docs/format/Columnar.html) - Columnar format for in-memory Apache Arrow processing.
- [Apache Avro](https://avro.apache.org/) - Row-oriented serialization for data streaming purpose.
- [Apache ORC](https://orc.apache.org/) - Column-oriented serialization for data storage purpose. Part of Hadoop platform.
- [Apache Parquet](https://parquet.apache.org/) - Column-oriented serialization for data storage purpose.
- [Apache Thrift](https://thrift.apache.org/) - Row-oriented serialization for RPC purpose.
- [Cap’n Proto](https://capnproto.org/) - Row-oriented serialization with zero-copy access, as fast as mmap.
- [Flatbuffer](https://flatbuffers.dev/) - Row-oriented serialization with zero-copy access, as fast as mmap.
- [Google Protobuf](https://protobuf.dev/) - Row-oriented serialization for RPC purpose.
- [Schema Registry](https://docs.confluent.io/platform/current/schema-registry/index.html) - Centralized repository for validating row-oriented events. Part of Kafka and Confluent platform.

### Open table formats

Open table formats are abstraction layer on top of Avro/Parquet files, with support for ACID transaction, CDC, partitioning, mixed streaming/batching processing, schema evolution and mutation. Schema and statistics are stored in a metastore, data is persisted locally or in a remote/cloud object storage.

Open tables are a cost-effective datawarehouse for petabyte scale.

- [Apache Hive](https://hive.apache.org/) - SQL-based data warehouse and query engine on top of Hadoop, and the origin of the Hive Metastore used by modern table formats.
- [Apache Hudi](https://hudi.apache.org/) - Open table format with strong CDC and upsert support, designed for incremental data pipelines.
- [Apache Iceberg](https://iceberg.apache.org/) - Open table format for huge analytic datasets, with snapshot isolation, schema evolution, and partition pruning.
- [DeltaLake](https://delta.io/) - Open table format bringing ACID transactions and scalable metadata to Apache Spark and beyond.

Comparison:
- [(2022) Open Table Formats: Delta vs Iceberg vs Hudi](https://medium.com/geekculture/open-table-formats-delta-iceberg-hudi-732f682ec0bb)
- [(2023) Choosing an open table format for your transactional data lake on AWS](https://aws.amazon.com/blogs/big-data/choosing-an-open-table-format-for-your-transactional-data-lake-on-aws/)
- [(2024) Apache Hudi vs Delta Lake vs Apache Iceberg: Feature Comparison Deep Dive](https://www.onehouse.ai/blog/apache-hudi-vs-delta-lake-vs-apache-iceberg-lakehouse-feature-comparison)

👆 Warning: pre-2022 articles should be considered as out-of-date, as open table formats are evolving quickly.

### Metastore

- [AWS Glue](https://aws.amazon.com/glue/) - Serverless data integration service with a managed catalog for AWS data assets.
- [Databricks unity catalog](https://docs.databricks.com/en/data-governance/unity-catalog/index.html) - Unified governance layer for data and AI assets across the Databricks platform.
- [Hive Metastore](https://cwiki.apache.org/confluence/display/hive/design) - Component of Hadoop HiveServer2 that can be used standalone as a schema registry for table metadata.
- [Nessie](https://projectnessie.org/) - Git-like versioning catalog for data lakes, enabling branch and merge operations on Iceberg/Delta/Hudi tables.

### Object Storage

- [Apache HDFS](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html) - Hadoop distributed file system, the original large-scale storage layer for the big data ecosystem.
- [AWS S3](https://aws.amazon.com/s3/) - Highly durable and available object storage service, the dominant cloud storage backend for data lakes.
- [Azure Blob Storage](https://azure.microsoft.com/en-us/products/storage/blobs) - Microsoft's massively scalable object storage for unstructured data.
- [GCP Cloud Storage](https://cloud.google.com/storage) - Google's unified object storage service for any amount of data.
- [Minio](https://min.io/) - S3-compatible self-hosted object storage, suitable for on-premise data lake deployments.

### Codecs, encoding and compression

- [Bit packing](https://kinematicsoup.com/news/2016/9/6/data-compression-bit-packing-101) - Encoding integers using only the bits required, eliminating wasted high-order zeros in columnar data.
- [Brotli](https://en.wikipedia.org/wiki/Brotli) - General-purpose lossless compression by Google, offering better ratios than gzip at comparable speed.
- [Deflate](https://en.wikipedia.org/wiki/Deflate) - Classic lossless compression combining LZ77 and Huffman coding; the basis of gzip and zlib.
- [Delta](https://en.wikipedia.org/wiki/Delta_encoding) - Stores differences between successive values instead of absolutes, ideal for monotonically increasing columns like timestamps.
- [Dictionary + RLE](https://www.linkedin.com/pulse/encodings-parquet-akhil-pathirippilly-mana/) - Replaces repeated values with dictionary codes, then run-length encodes consecutive duplicates; effective for low-cardinality columns.
- [Gorilla](https://dl.acm.org/doi/10.14778/2824032.2824078) - Facebook's XOR-based float compression for time-series metrics, achieving 1.37 bytes/value on typical monitoring data.
- [LZ4](https://en.wikipedia.org/wiki/LZ4_(compression_algorithm)) - Extremely fast lossless compression algorithm prioritizing throughput over ratio, widely used in real-time pipelines.
- [Snappy](https://en.wikipedia.org/wiki/Snappy_(compression)) - Google's fast lossless codec optimized for speed over compression ratio, default in many Hadoop/Parquet deployments.
- [zstd](https://en.wikipedia.org/wiki/Zstd) - Facebook's modern lossless codec delivering high compression ratios at fast speeds; often preferred over gzip in data lakes.

## Brokers and distributed messaging

Message brokers sit between producers and consumers in the data stack, providing durable, ordered event streams that decouple ingestion from processing and enable replay, fan-out, and exactly-once delivery semantics.

- [Apache Kafka](https://kafka.apache.org/) - Distributed event streaming platform, the de facto standard for high-throughput data pipelines and event-driven architectures.
- [Apache Pulsar](https://pulsar.apache.org/) - Distributed messaging and streaming platform with multi-tenancy, geo-replication, and a decoupled storage layer.
- [NATS / JetStream](https://nats.io/) - Lightweight cloud-native messaging system; JetStream adds persistence, replay, and streaming semantics.
- [RabbitMQ Streams](https://www.rabbitmq.com/streams.html) - Persistent, append-only log streams for RabbitMQ, enabling high-throughput message replay and fan-out.
- [Redpanda](https://redpanda.com/) - Kafka-compatible streaming data platform written in C++, with no ZooKeeper dependency and lower latency.

## Ingestion and querying

### Stream processing

Real-time data processing (also called event streaming) handles data as it is generated — enabling low-latency pipelines, continuous aggregations, and immediate downstream reactions to events.

- [Akka Streams](https://doc.akka.io/docs/akka/current/stream/index.html) - Reactive stream processing library for JVM, built on the actor model.
- [Apache Beam](https://beam.apache.org/) - Unified SDK for cross-language stream and batch processing. Available in Go, Python, Java, Scala and TypeScript.
- [Apache Flink](https://flink.apache.org/) - Stateful stream processing with exactly-once semantics, supporting event time and out-of-order data.
- [Apache Kafka Streams](https://kafka.apache.org/documentation/streams/) - Lightweight stream processing library embedded in the Kafka client, no separate cluster required.
- [Apache Spark Streaming](https://spark.apache.org/streaming/) - Micro-batch stream processing on top of Spark, integrating with the broader Spark ecosystem.
- [Redpanda Connect (formerly Benthos)](https://www.redpanda.com/connect) - Declarative stream processing toolkit in Go, with a wide connector library.
- [Materialize](https://materialize.com/) - Operational data warehouse that incrementally maintains SQL views over streaming data, always-fresh without recomputation.
- [RisingWave](https://risingwave.com/) - Distributed SQL streaming database (PostgreSQL-compatible) with sub-100ms end-to-end freshness and native Iceberg integration.

### Batch processing

Process periodically a large amount of data in a single batch.

- [Apache Spark](https://spark.apache.org/) - Distributed batch processing engine with in-memory computation, supporting SQL, ML, and graph workloads.
- [MapReduce](https://en.wikipedia.org/wiki/MapReduce) - Programming model for processing large datasets in parallel across a cluster; the foundation of the Hadoop ecosystem.

### In-memory processing

Non real-time SQL queries executed against a large database can be processed locally. This method might not fit into memory or lead to very long job duration.

- [Apache Arrow](https://arrow.apache.org/) - Low-level in-memory columnar data format with zero-copy access across languages via gRPC/IPC interfaces.
- [Apache Arrow DataFusion](https://arrow.apache.org/datafusion/) - High-level SQL and DataFrame query engine built on Apache Arrow, written in Rust.
- [chDB](https://github.com/chdb-io/chdb) - Embeddable in-process OLAP engine powered by ClickHouse, callable from Python without a server.
- [clickhouse-local](https://clickhouse.com/docs/en/operations/utilities/clickhouse-local) - Lightweight CLI version of ClickHouse for running SQL queries against CSV, JSON, Parquet and other files.
- [delta-rs](https://github.com/delta-io/delta-rs) - Standalone DeltaLake driver for Python and Rust. Does not depend on Spark.
- [Delta Standalone](https://docs.delta.io/latest/delta-standalone.html) - Standalone DeltaLake driver for Java and Scala. Does not depend on Spark.
- [DuckDB](https://duckdb.org/) - In-process SQL OLAP query engine for Parquet, CSV, and JSON files. Built on Apache Arrow.
- [Pandas](https://pandas.pydata.org/) - Python Da