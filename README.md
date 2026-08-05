<div align="center">

# Sang Hyun Lee

**Data &amp; AI Platform Engineer** &nbsp;·&nbsp; Seoul, Korea

I build the infrastructure that moves data at scale — streaming ingestion, lakehouse storage,<br/>
distributed query engines — and the LLM agents that make it usable.<br/>
Currently at **SK Telecom**, on a petabyte-scale data platform.

<a href="https://www.linkedin.com/in/sanghyun-lee-7b9b6a236"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="mailto:shyundev@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email"/></a>
<a href="mailto:shyun9417@sk.com"><img src="https://img.shields.io/badge/Work-sk.com-334155?style=flat-square&labelColor=1E293B" alt="Work email at sk.com"/></a>
<a href="https://www.youtube.com/watch?v=qUT-uaEE-Fk"><img src="https://img.shields.io/badge/Trino%20Summit%20talk-FF0000?style=flat-square&logo=youtube&logoColor=white" alt="Trino Summit talk"/></a>

</div>

---

## What I work on

**⚡ Streaming lakehouse pipelines**<br/>
Kafka → Flink → Iceberg ingestion for high-volume sensor and process data, sustaining roughly 3M records/sec into a petabyte-scale lake. Benchmarked Iceberg against Hudi across insert, upsert, query and maintenance workloads before committing to the table format; built out the Flink Kubernetes Operator deployment, and Spark (Scala) maintenance jobs — compaction, sorting, snapshot expiry — orchestrated on Airflow.

**🔎 Query engine performance**<br/>
A 100+ node Trino cluster fields 300+ queries per minute, individual queries scanning terabytes. Most of the wins came from the storage side — partition strategy, sort order, compaction cadence — and the rest from the query side: pushdown improvements and approximate aggregations where exactness wasn't required. This architecture was the subject of my Trino Summit 2023 talk.

**☸️ Multi-tenant runtime on Kubernetes**<br/>
A self-service platform that provisions per-user Spark and StarRocks clusters on demand, operating thousands of them concurrently: custom operators and CRDs, a Java/Spring orchestration service, Helm packaging, ArgoCD GitOps, and Prometheus/OpenSearch observability. Running an OLAP engine as a multi-tenant service — rather than as one shared cluster — is where most of my engine-internals work comes from.

**🤖 Agents for platform operations**<br/>
An agent that consumes query history and cluster state snapshots off Kafka, diagnoses resource, configuration and query-level problems, and proposes concrete fixes — applied only after human approval. Deterministic rules and cost models do the heavy lifting; the model handles classifying unseen symptoms, correlating signals, and rewriting queries.

**🧠 Domain-expert agents**<br/>
A knowledge-graph-driven agent for operational troubleshooting, structured as *graph selection → graph traversal → path evaluation*: LLM-based graph selection to cover the gaps in vector similarity search, hierarchical filtering over a partitioned graph, parallel sub-agents that traverse branches and prune infeasible paths early, self-correcting tool-call loops, and a final helpfulness/groundedness evaluation that picks or aggregates the answer path. Includes Text-to-SQL over Oracle and Postgres, and on-prem inference tuning with vLLM (speculative decoding, prefix caching).

**🎯 Domain-specialized LLM**<br/>
Fine-tuned SK Telecom's A.X foundation model (32B) with DeepSpeed and TRL into an HR-domain assistant, reaching ~90% of the then-SOTA general model's quality on evaluations scored by domain experts — at a fraction of the serving cost.

---

## Talks

<table>
<tr>
<td width="50%" valign="top">
<a href="https://www.youtube.com/watch?v=qUT-uaEE-Fk"><img src="assets/trino-summit-2023.jpg" width="100%" alt="Efficient Kappa Architecture with Trino — Trino Summit 2023"/></a>
<h3>Efficient Kappa Architecture with Trino</h3>
<b>Trino Summit 2023</b>
<p>One pipeline instead of two — serving terabyte-scale queries over data that is still arriving, on Kafka, Flink, Iceberg and Trino.</p>
<a href="https://www.youtube.com/watch?v=qUT-uaEE-Fk"><img src="https://img.shields.io/badge/%E2%96%B6%20Watch-FF0000?style=flat-square&logo=youtube&logoColor=white" alt="Watch"/></a>
<a href="https://trino.io/assets/blog/trino-summit-2023/efficient-kappa-architecture-sk-telecom.pdf"><img src="https://img.shields.io/badge/Slides-334155?style=flat-square" alt="Slides"/></a>
</td>
<td width="50%" valign="top">
<a href="https://www.communitydays.org/event/2025-11-28/ai-community-conference-aico-seoul#sessions?id=1043638"><img src="assets/aico-2025.jpg" width="100%" alt="Building Domain-Expert Agents — AI Community Conference Seoul 2025"/></a>
<h3>Building Domain-Expert Agents</h3>
<b>AI Community Conference (AICO) Seoul 2025</b>
<p>Moving an agent from general capability to domain expertise — knowledge graphs over flat retrieval, traversal with early pruning, and grading the path rather than only the answer.</p>
<a href="https://www.communitydays.org/event/2025-11-28/ai-community-conference-aico-seoul#sessions?id=1043638"><img src="https://img.shields.io/badge/Session%20details-334155?style=flat-square" alt="Session details"/></a>
</td>
</tr>
</table>

---

## Open source

Fixes to the query engines, catalogs and operators we run in production.

| Project | Merged PR | Area | Fix |
| --- | --- | --- | --- |
| Apache Polaris | [#5247](https://github.com/apache/polaris/pull/5247) | Auth | Turn a transient metastore outage during authentication into a retryable 503 rather than a permanent 500 |
| Apache Polaris | [#5363](https://github.com/apache/polaris/pull/5363) | Auth | Return one generic 503 so an unauthenticated caller cannot tell which internal lookup failed |
| Apache Polaris | [#5361](https://github.com/apache/polaris/pull/5361) | Persistence | Add the missing grant index to the CockroachDB schema, so permission checks stop scanning every grant in the realm |
| StarRocks | [#78722](https://github.com/StarRocks/starrocks/pull/78722) | Query execution | Clamp UTF-8 character stepping to the value's own bytes, stopping an out-of-bounds read that returned other rows' data |
| StarRocks | [#79037](https://github.com/StarRocks/starrocks/pull/79037) | Query execution | Return 0 from months_diff and years_diff for two dates in the same month or year, instead of -1 |

---

## Experience

<table>
<tr><td><b>2023 — present</b></td><td><b>SK Telecom</b><br/><sub>Data Platform</sub></td><td>Streaming lakehouse at petabyte scale · query runtime as a multi-tenant Kubernetes service · LLM agents and domain fine-tuning</td></tr>
<tr><td><b>2022 — 2023</b></td><td><b>KFTC</b><br/><sub>Korea Financial Telecommunications &amp; Clearings Institute · Data Analytics</sub></td><td>Real-time fraud detection on open banking traffic, peaks of 500K TPS · batch ETL landing hundreds of millions of rows across thousands of tables daily · nationwide ATM and branch data service spanning 38 institutions</td></tr>
<tr><td><b>2019 — 2021</b></td><td><b>Samsung Research</b><br/><sub>Data Analytics Lab</sub></td><td>Household clustering over 100M+ device logs — graph construction, Louvain clustering, day-over-day cluster tracking. Rebuilt a single-node pipeline on Spark: 2 hours → 30 minutes</td></tr>
</table>

<sub>B.S. in Information Systems, Hanyang University</sub>

---

## Tech

<table>
<tr><td valign="top"><b>Streaming &amp; batch</b></td><td><img src="https://img.shields.io/badge/Kafka-334155?style=flat-square&logo=apachekafka&logoColor=white" alt="Kafka"/> <img src="https://img.shields.io/badge/Flink-334155?style=flat-square&logo=apacheflink&logoColor=white" alt="Flink"/> <img src="https://img.shields.io/badge/Spark-334155?style=flat-square&logo=apachespark&logoColor=white" alt="Spark"/> <img src="https://img.shields.io/badge/Airflow-334155?style=flat-square&logo=apacheairflow&logoColor=white" alt="Airflow"/></td></tr>
<tr><td valign="top"><b>Lakehouse &amp; query</b></td><td><img src="https://img.shields.io/badge/Iceberg-334155?style=flat-square" alt="Iceberg"/> <img src="https://img.shields.io/badge/Polaris-334155?style=flat-square" alt="Polaris"/> <img src="https://img.shields.io/badge/Trino-334155?style=flat-square&logo=trino&logoColor=white" alt="Trino"/> <img src="https://img.shields.io/badge/StarRocks-334155?style=flat-square" alt="StarRocks"/> <img src="https://img.shields.io/badge/Hive-334155?style=flat-square&logo=apachehive&logoColor=white" alt="Hive"/> <img src="https://img.shields.io/badge/Impala-334155?style=flat-square" alt="Impala"/> <img src="https://img.shields.io/badge/Kudu-334155?style=flat-square" alt="Kudu"/> <img src="https://img.shields.io/badge/Hadoop-334155?style=flat-square&logo=apachehadoop&logoColor=white" alt="Hadoop"/></td></tr>
<tr><td valign="top"><b>AI &amp; LLM</b></td><td><img src="https://img.shields.io/badge/vLLM-334155?style=flat-square" alt="vLLM"/> <img src="https://img.shields.io/badge/DeepSpeed-334155?style=flat-square" alt="DeepSpeed"/> <img src="https://img.shields.io/badge/TRL-334155?style=flat-square&logo=huggingface&logoColor=white" alt="TRL"/> <img src="https://img.shields.io/badge/PyTorch-334155?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch"/></td></tr>
<tr><td valign="top"><b>Platform</b></td><td><img src="https://img.shields.io/badge/Kubernetes-334155?style=flat-square&logo=kubernetes&logoColor=white" alt="Kubernetes"/> <img src="https://img.shields.io/badge/Helm-334155?style=flat-square&logo=helm&logoColor=white" alt="Helm"/> <img src="https://img.shields.io/badge/ArgoCD-334155?style=flat-square&logo=argo&logoColor=white" alt="ArgoCD"/> <img src="https://img.shields.io/badge/Docker-334155?style=flat-square&logo=docker&logoColor=white" alt="Docker"/> <img src="https://img.shields.io/badge/Jenkins-334155?style=flat-square&logo=jenkins&logoColor=white" alt="Jenkins"/> <img src="https://img.shields.io/badge/Prometheus-334155?style=flat-square&logo=prometheus&logoColor=white" alt="Prometheus"/> <img src="https://img.shields.io/badge/OpenSearch-334155?style=flat-square&logo=opensearch&logoColor=white" alt="OpenSearch"/></td></tr>
<tr><td valign="top"><b>Languages</b></td><td><img src="https://img.shields.io/badge/Java-334155?style=flat-square&logo=openjdk&logoColor=white" alt="Java"/> <img src="https://img.shields.io/badge/Scala-334155?style=flat-square&logo=scala&logoColor=white" alt="Scala"/> <img src="https://img.shields.io/badge/Python-334155?style=flat-square&logo=python&logoColor=white" alt="Python"/> <img src="https://img.shields.io/badge/SQL-334155?style=flat-square&logo=postgresql&logoColor=white" alt="SQL"/> <img src="https://img.shields.io/badge/Go-334155?style=flat-square&logo=go&logoColor=white" alt="Go"/></td></tr>
</table>

---

<div align="center">
<sub>

[LinkedIn](https://www.linkedin.com/in/sanghyun-lee-7b9b6a236) &nbsp;·&nbsp; [shyundev@gmail.com](mailto:shyundev@gmail.com) &nbsp;·&nbsp; [shyun9417@sk.com](mailto:shyun9417@sk.com) &nbsp;·&nbsp; earlier work, archived at [github.com/sahyle9417](https://github.com/sahyle9417) and [gitlab.com/sahyle9417](https://gitlab.com/sahyle9417)

</sub>
</div>
