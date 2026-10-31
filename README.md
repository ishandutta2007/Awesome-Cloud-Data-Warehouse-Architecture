# Awesome-Cloud-Data-Warehouse-Architecture

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/ishandutta2007/Awesome-Cloud-Data-Warehouse-Architecture?style=social&color=white)](https://github.com/ishandutta2007/Awesome-Cloud-Data-Warehouse-Architecture/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ishandutta2007/Awesome-Cloud-Data-Warehouse-Architecture/pulls)

> A curated list of **Cloud Data Warehouse (CDW)** architectures, analytical databases, Massively Parallel Processing (MPP) engines, and open Lakehouse query infrastructures.

**Top Cloud Data Warehouse Architecture (Open-Source & Managed) 🌟 Star if you like it! 🌟**

*Focused on Separation of Storage and Compute, MPP Engines, Lakehouse Integration, Vectorized Execution & Self-Hosted Analytical Databases.*

**Last updated: October 2026**

---

## Overview

This repository tracks notable **SaaS platforms** and **open-source projects** for modern **Cloud Data Warehouse Architecture**. These tools enable organizations to store, transform, and analyze petabyte-scale datasets with high concurrency and sub-second latency—ranging from fully managed serverless platforms with elastic scaling and workload isolation to open-source distributed analytical databases that provide full control over infrastructure and cost models.

Whether you are evaluating hyperscaler data warehouses (Amazon Redshift, Google BigQuery, Snowflake, Databricks SQL) or deploying self-hosted real-time OLAP engines (ClickHouse, StarRocks, Apache Doris, Apache Pinot, DuckDB), this guide offers a transparent, structured breakdown of architecture, commercial market dynamics, pricing tiers, and open-source ecosystems.

---

## Table of Contents

- [Sector Overview & Market Dynamics](#sector-overview--market-dynamics)
- [SaaS & Hosted CDW Platforms](#saas--hosted-cdw-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [Key Architectural Trade-offs](#key-architectural-trade-offs)
- [How to Contribute](#how-to-contribute)
- [License & Disclaimer](#license--disclaimer)

---

## Sector Overview & Market Dynamics

The global Cloud Data Warehouse (CDW) and modern lakehouse analytical market is estimated at **$14.9 billion to $16.5 billion in 2026**, expanding rapidly at a Compound Annual Growth Rate (CAGR) of **~21%–25%** driven by generative AI workloads, real-time analytics, and enterprise data migration away from legacy on-premises appliances. 

The sector is **moderately fragmented**: while hyperscale cloud providers (AWS, Microsoft Azure, Google Cloud) and independent industry titans (Snowflake, Databricks) capture significant revenue share, the space is heavily fractured rather than a pure "winner-take-all" market. Rapid emergence of open table formats (Apache Iceberg, Delta Lake), federated query layers (Trino, Starburst), embedded analytics (DuckDB), and high-throughput real-time OLAP engines (ClickHouse, StarRocks, Apache Doris) allows specialized vendors and open-source architectures to capture substantial market niches across hybrid, multi-cloud, and real-time operational workloads.

---

## SaaS & Hosted CDW Platforms

The following table compares leading SaaS and fully managed cloud data warehouse platforms. Entries are sorted in descending order by **Company Size (Revenue / Market Capitalization / Valuation)**.

| Company / Product | Company Size (Market Cap / Valuation / ARR) | Architecture & Capabilities | Pricing (Starting Tier) | Free Tier / Trial Limits | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **[Google BigQuery](https://cloud.google.com/bigquery)** | **~$2.1T+** (Alphabet Market Cap) | Fully serverless, columnar storage with Capacitor engine; execution over petabit Jupiter network; separation of compute and storage. | **$6.25 / TB** scanned (On-Demand) or editions starting from **$0.04 / slot-hour** (Standard Edition); storage from **$0.02 / GB/mo** | **Always Free Tier:** 1 TB queries/month scanned and 10 GB storage free every month forever. New users also receive a $300 90-day credit trial. | Spiky or unpredictable workloads needing zero operational overhead and instant serverless scaling. |
| **[Azure Synapse Analytics](https://azure.microsoft.com/en-us/products/synapse-analytics)** | **~$3.0T+** (Microsoft Market Cap) | Unified analytics workspace combining Dedicated SQL pools (MPP), Serverless SQL pools (lake querying), and Spark pools over ADLS Gen2. | **$5.00 / TB** processed (Serverless SQL); Dedicated SQL pools start at **$1.20 / hour** (`DW100c` tier); storage from **$0.023 / GB/mo** | **30-Day Free Trial:** $200 free credits valid for 30 days via Azure Free Account (no permanent free tier for Synapse SQL pools). | Microsoft-centric enterprise ecosystems seeking single-pane integration with Power BI and Fabric. |
| **[Amazon Redshift](https://aws.amazon.com/redshift/)** | **~$2.0T+** (Amazon Market Cap) | MPP columnar warehouse with RA3 nodes (managed local SSD tiered transparently to Amazon S3); Serverless option with auto-scaling RPUs. | **$0.25 / hour** per node (`dc2.large` provisioned) or **$0.375 / RPU-hour** (Serverless, min 8 RPUs); storage from **$0.024 / GB/mo** | **2-Month Free Trial:** 750 hours/month of `dc2.large` instance free for 2 months (or $300 Redshift Serverless credits valid for 90 days). | AWS-native ecosystems needing mature petabyte-scale MPP with tight S3 and AWS Glue integration. |
| **[Databricks SQL](https://www.databricks.com/)** | **~$190B** (Valuation, Series I/J) | Lakehouse data warehousing using decoupled serverless SQL warehouses directly against open Delta Lake tables, governed by Unity Catalog. | **$0.22 / DBU** (Serverless SQL starts at **$0.70 / DBU**; standard compute from **$0.20–$0.40 / DBU**) plus underlying cloud VM infrastructure | **Free Edition (Forever Free):** 1 SQL warehouse (max 2X-Small), 5 concurrent jobs for learning. **Business Free Trial:** 14-day free trial with $400 credits. | Unified lakehouse architecture running warehouse BI workloads directly on data lake storage without data duplication. |
| **[Snowflake](https://www.snowflake.com/)** | **~$110B–$115B** (Market Cap, NYSE: SNOW) | Multi-cluster, shared-data architecture with complete separation of storage, compute (Virtual Warehouses), and cloud services across AWS, Azure, GCP. | **$2.00 / credit** (Standard Edition On-Demand, e.g., X-Small warehouse = 1 credit/hour = $2.00/hour); compressed storage **$40.00 / TB/mo** | **30-Day Free Trial:** $400 in usage credits valid for 30 days (whichever expires first; no credit card required upfront). | Enterprise multi-cloud deployments requiring strict workload isolation, zero-maintenance operations, and data sharing. |
| **[ClickHouse Cloud](https://clickhouse.com/cloud)** | **~$15B** (Valuation, Series D) / **$250M ARR** | Fully managed serverless ClickHouse with compute-compute isolation, ClickPipes managed ingestion, object-storage decoupling, and autoscaling. | **~$65–$70 / month** baseline continuous compute (Basic Tier) with scale-to-zero capabilities when idle; storage at **$0.026 / GB/mo** | **30-Day Free Trial:** $300 in free trial credits valid for 30 days (whichever expires first). | Real-time analytics, high-frequency event ingestion, observability, and sub-second log analytics. |
| **[Starburst Galaxy](https://www.starburst.io/)** | **~$3.35B–$3.4B** (Valuation, Series D) / **$100M+ ARR** | Fully managed Trino-based lakehouse query engine featuring zero-ops Apache Iceberg pipelines, cross-cloud querying, and automated table optimization. | **$0.50 / credit** (Pro Tier) and **$0.75 / credit** (Enterprise Tier); Warp Speed acceleration clusters available | **Free Forever Tier:** 2 forever-free clusters for lightweight exploration. **30-Day Trial:** $500 free Enterprise credits for 30 days. | Federated queries across disparate databases and object stores with automated Apache Iceberg table management. |
| **[Teradata Vantage](https://www.teradata.com/)** | **~$3.2B** (Market Cap, NYSE: TDC) | Hybrid multi-cloud analytical platform with native parallel processing, ClearScape Analytics (in-database AI/ML), and integrated graph engines. | **$4.00 / Vantage Unit (VU)** consumption tier on AWS/Azure (or private contracted capacity starting ~$3,000–$5,000/mo) | **30-Day Free Trial:** Available through Teradata VantageCloud trial sandbox environments with pre-loaded credits for 30 days. | Traditional large enterprises migrating on-premises enterprise data warehouses to hybrid cloud architectures. |
| **[Firebolt](https://www.firebolt.io/)** | **~$1.4B** (Valuation, Series C) | Decoupled cloud data warehouse engine featuring single-binary execution, local NVMe SSD caching, sparse indexing, and extreme query concurrency. | **$0.10–$0.30 / engine core hour** (billed per second with auto-stop/resume) + pass-through cloud object storage costs | **30-Day Free Trial:** $200 in free cloud compute credits upon registration. Firebolt Core is free for self-managed local testing. | Low-latency, high-concurrency customer-facing analytical applications and sub-second BI dashboards. |
| **[Yellowbrick](https://yellowbrick.com/)** | **~$250M+** (Total Venture Funding Raised) | PostgreSQL-compatible, Kubernetes-native MPP analytical data warehouse deployable in private clouds, AWS, Azure, GCP, or on-premises. | **$0.28 / vCPU-hour** (Burst Monthly on-demand) or **$613 / vCPU/year** (1-Year Subscription); entry departmental plans start at **$10,000 / month** | **30-Day Free Trial:** 30-day proof-of-concept free trial available upon request for testing cluster performance and hybrid-cloud setups. | Highly regulated enterprises, financial institutions, and hybrid cloud environments requiring data residency and dedicated VPC control. |

---

## Open-Source GitHub Projects

Curated open-source analytical databases, Massively Parallel Processing (MPP) engines, lakehouse table formats, and vectorized query runtimes.

Repositories are sorted in descending order by **GitHub Star Count**. Every badge links directly to that repository's GitHub Stargazers page.

| Repository | GitHub Stars Badge | License | Language / Stack | Core Architectural Focus | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **[ClickHouse](https://github.com/ClickHouse/ClickHouse)** | [![Stars](https://img.shields.io/github/stars/ClickHouse/ClickHouse?style=social&color=white)](https://github.com/ClickHouse/ClickHouse/stargazers) | Apache-2.0 | C++ | Column-oriented DBMS utilizing MergeTree engines and vectorized execution; extreme single-table aggregation speed. | Real-time observability, event streams, clickstream data, and sub-second analytical reporting. |
| **[DuckDB](https://github.com/duckdb/duckdb)** | [![Stars](https://img.shields.io/github/stars/duckdb/duckdb?style=social&color=white)](https://github.com/duckdb/duckdb/stargazers) | MIT | C++, C | In-process vectorized columnar SQL OLAP database (the "SQLite for Analytics"); zero external dependencies, direct Parquet/Iceberg querying. | Local analytics, data science pipelines, client-side Python/R analytical applications, and embedded serverless ETL. |
| **[TDengine](https://github.com/taosdata/TDengine)** | [![Stars](https://img.shields.io/github/stars/taosdata/TDengine?style=social&color=white)](https://github.com/taosdata/TDengine/stargazers) | AGPL-3.0 | C, Rust | High-performance distributed time-series big data platform with built-in caching, stream computing, and SQL data warehousing. | Industrial IoT, smart metering, telemetry tracking, and connected vehicle time-series warehousing. |
| **[Apache Arrow](https://github.com/apache/arrow)** | [![Stars](https://img.shields.io/github/stars/apache/arrow?style=social&color=white)](https://github.com/apache/arrow/stargazers) | Apache-2.0 | C++, Rust, Python, Go | Universal columnar in-memory data standard and zero-copy shared memory framework powering modern vectorized analytics. | Cross-system zero-copy data exchange, columnar in-memory compute kernels, and analytical middleware. |
| **[Presto](https://github.com/prestodb/presto)** | [![Stars](https://img.shields.io/github/stars/prestodb/presto?style=social&color=white)](https://github.com/prestodb/presto/stargazers) | Apache-2.0 | Java, C++ (Velox) | Distributed MPP SQL query engine developed by Meta for interactive analytical queries against multi-petabyte sources. | Interactive ad-hoc querying across petabyte-scale data lakes and enterprise data mesh topologies. |
| **[Apache Doris](https://github.com/apache/doris)** | [![Stars](https://img.shields.io/github/stars/apache/doris?style=social&color=white)](https://github.com/apache/doris/stargazers) | Apache-2.0 | C++, Java | Full-featured MPP analytical database with vectorized engine, Unique Key upsert support, inverted indexes, and MySQL protocol compatibility. | Interactive BI dashboards, high-concurrency point queries, real-time data warehousing, and log analytics. |
| **[Apache Druid](https://github.com/apache/druid)** | [![Stars](https://img.shields.io/github/stars/apache/druid?style=social&color=white)](https://github.com/apache/druid/stargazers) | Apache-2.0 | Java | Real-time distributed analytical datastore designed for sub-second OLAP queries and continuous streaming ingestion from Kafka/Kinesis. | Real-time operational dashboards, application telemetry, and high-ingestion time-stamped event data. |
| **[Trino](https://github.com/trinodb/trino)** | [![Stars](https://img.shields.io/github/stars/trinodb/trino?style=social&color=white)](https://github.com/trinodb/trino/stargazers) | Apache-2.0 | Java | Massively Parallel Processing (MPP) distributed SQL query engine for federated queries across heterogeneous sources without moving data. | Lakehouse query abstraction, cross-catalog queries, and federated analytics across Iceberg, Delta, and relational databases. |
| **[Citus](https://github.com/citusdata/citus)** | [![Stars](https://img.shields.io/github/stars/citusdata/citus?style=social&color=white)](https://github.com/citusdata/citus/stargazers) | AGPL-3.0 | C | PostgreSQL extension that horizontally shards data and query execution across multiple PostgreSQL nodes for distributed analytical processing. | Multi-tenant SaaS applications, real-time operational analytics, and scaling existing PostgreSQL infrastructure horizontally. |
| **[StarRocks](https://github.com/StarRocks/starrocks)** | [![Stars](https://img.shields.io/github/stars/StarRocks/starrocks?style=social&color=white)](https://github.com/StarRocks/starrocks/stargazers) | Apache-2.0 | C++, Java | Next-generation sub-second MPP OLAP database with asynchronous incremental materialized views and direct lakehouse query acceleration. | Lakehouse BI acceleration over Apache Iceberg/Delta Lake, real-time multi-table JOINs, and high-concurrency reporting. |
| **[Apache DataFusion](https://github.com/apache/datafusion)** | [![Stars](https://img.shields.io/github/stars/apache/datafusion?style=social&color=white)](https://github.com/apache/datafusion/stargazers) | Apache-2.0 | Rust | Extensible vectorized SQL query engine and execution framework built in Rust on Apache Arrow; powers modern database engines. | Building custom analytical database engines, embedded lakehouse query runtimes, and distributed execution engines. |
| **[Apache Iceberg](https://github.com/apache/iceberg)** | [![Stars](https://img.shields.io/github/stars/apache/iceberg?style=social&color=white)](https://github.com/apache/iceberg/stargazers) | Apache-2.0 | Java, Rust, Python | High-performance open table format for huge analytic tables; supports ACID transactions, hidden partitioning, and schema evolution. | Establishing open, vendor-neutral lakehouse storage layers queryable by Trino, StarRocks, Spark, Snowflake, and BigQuery. |
| **[Delta Lake](https://github.com/delta-io/delta)** | [![Stars](https://img.shields.io/github/stars/delta-io/delta?style=social&color=white)](https://github.com/delta-io/delta/stargazers) | Apache-2.0 | Scala, Java, Rust | Open-source storage framework that brings ACID transactions, time travel, and scalable metadata handling to Apache Spark and big data engines. | Spark-centric lakehouses, enterprise data lakes requiring reliable stream/batch ACID writes and change-data-capture (CDC). |
| **[Apache Hudi](https://github.com/apache/hudi)** | [![Stars](https://img.shields.io/github/stars/apache/hudi?style=social&color=white)](https://github.com/apache/hudi/stargazers) | Apache-2.0 | Java | Transactional data lake platform providing record-level upserts, deletes, incremental streaming queries, and index-assisted point lookups. | Streaming-heavy ingestion, CDC log compaction, and near-real-time upsert pipelines directly in cloud object storage. |
| **[Apache Pinot](https://github.com/apache/pinot)** | [![Stars](https://img.shields.io/github/stars/apache/pinot?style=social&color=white)](https://github.com/apache/pinot/stargazers) | Apache-2.0 | Java | Distributed columnar OLAP datastore with inverted, range, and star-tree indexes designed to execute low-latency queries at ultra-high QPS. | User-facing analytics products (e.g., LinkedIn Who Viewed My Profile, Uber Eats analytics) and high-throughput real-time dashboards. |
| **[Apache Paimon](https://github.com/apache/paimon)** | [![Stars](https://img.shields.io/github/stars/apache/paimon?style=social&color=white)](https://github.com/apache/paimon/stargazers) | Apache-2.0 | Java | Streaming data lake storage format based on LSM-Tree structure for high-speed streaming data ingestion and real-time update lookups. | Flink-native streaming pipelines, real-time lakehouse ingestion, and high-frequency upserts. |
| **[Apache Kylin](https://github.com/apache/kylin)** | [![Stars](https://img.shields.io/github/stars/apache/kylin?style=social&color=white)](https://github.com/apache/kylin/stargazers) | Apache-2.0 | Java | Distributed analytical engine designed to provide a SQL interface and multi-dimensional analysis (MOLAP) on Hadoop/Spark with sub-second queries. | Fixed-dimensional corporate reporting and massive pre-aggregated BI cubes over petabytes of historical data. |
| **[Apache DataFusion Ballista](https://github.com/apache/datafusion-ballista)** | [![Stars](https://img.shields.io/github/stars/apache/datafusion-ballista?style=social&color=white)](https://github.com/apache/datafusion-ballista/stargazers) | Apache-2.0 | Rust | Distributed compute platform implemented in Rust, powered by Apache Arrow and DataFusion for lightweight MPP execution. | Cloud-native distributed query execution, serverless analytical workers, and Rust-based big data processing pipelines. |

---

## Key Architectural Trade-offs

1. **Fully Managed SaaS vs. Self-Hosted MPP Engines**
   - **Snowflake, BigQuery, and Databricks SQL** eliminate operational overhead with multi-cluster isolation and autoscaling, but ongoing cloud compute consumption can scale significantly with unoptimized queries.
   - **ClickHouse, StarRocks, and Apache Doris** offer 5x–10x hardware efficiency and predictable fixed compute costs, but require dedicated site reliability engineering (SRE) for cluster scaling, sharding, and backup replication.

2. **Serverless On-Demand vs. Decoupled Compute Clusters**
   - **Google BigQuery** processes queries serverlessly without requiring compute provisioning; pricing is driven by data scanned ($6.25/TB) or flat slot capacity.
   - **Snowflake & Firebolt** isolate virtual compute clusters from cloud object storage, ensuring independent workload isolation where compute shuts down when idle.

3. **Pure-Play Query Engines vs. Storage-Engine OLAP Databases**
   - **Trino and Presto** store zero data, federating SQL queries across Iceberg, S3, PostgreSQL, and Snowflake.
   - **ClickHouse, Druid, and Pinot** bundle custom indexing and storage layouts (MergeTree, Star-Tree indexes) optimized for extreme sub-second point lookups and streaming aggregations.

4. **Lakehouse Table Formats (Iceberg vs. Delta vs. Hudi vs. Paimon)**
   - **Apache Iceberg** is the vendor-neutral standard for open lakehouses, supported natively by Snowflake, BigQuery, StarRocks, and Trino.
   - **Delta Lake** provides deep optimization within Databricks and Apache Spark ecosystems.
   - **Apache Hudi and Paimon** specialize in LSM-tree upserts, streaming change data capture (CDC), and continuous ingestion workflows.

---

## How to Contribute

We welcome community contributions! To add a new platform or update information:

1. Fork this repository.
2. Update `README.md` with factual architecture descriptions, transparent pricing benchmarks, or open-source repositories.
3. For open-source tools, include the GitHub stars badge formatted as:
   `[![Stars](https://img.shields.io/github/stars/{owner}/{repo}?style=social&color=white)](https://github.com/{owner}/{repo}/stargazers)`
4. Ensure entries are placed in the appropriate sorted table.
5. Submit a descriptive Pull Request (PR).

---

## License & Disclaimer

- Distributed under the [MIT License](LICENSE).
- **Disclaimer**: Company valuations, market capitalization figures, and list pricing tiers are collected from public filings, vendor pricing pages, and verified financial reporting as of October 2026. Consult vendor documentation for real-time workload-specific quote modeling.
