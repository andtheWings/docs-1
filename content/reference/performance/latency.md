---
title: SQL Latency and Throughput
---

Our approach to SQL performance benchmarking is to use `sysbench`, an
industry standard benchmkarking tool.

### Performance Roadmap

Dolt is slower than MySQL. The goal is to get Dolt to within 2-4 times
the speed of MySQL for common operations. If a query takes MySQL 1
second, we expect it to take Dolt 2-4 seconds. Or, if MySQL can run 8
queries in 10 seconds, then we want Dolt to run 2-4 queries in 10
seconds. The `multiple` column represents this relationship with
regard to a particular benchmark.

It's important recognize that these are industry standard tests, and
are OLTP oriented. Many Dolt use-cases are non-OLTP, and Dolt is fast
for bulk operations common in, for example, data pipeline contexts.

### Benchmark Data

Below are the results of running `sysbench` MySQL tests against Dolt
SQL Server for the most recent release of Dolt. We will update this
with every release. The tests attempt to run as many queries as
possible in a fixed 2 minute time window. The `Dolt` and `MySQL`
columns show the median latency of each query during that 2 minute
time window.

The Dolt version is `0.28.2`.

| Read Tests | Dolt | MySQL | Multiple |
| :--- | :--- | :--- | :--- |
| covering\_index\_scan | 11.04 | 1.42 | 8.0 |
| index\_scan | 132.49 | 34.95 | 4.0 |
| oltp\_point\_select | 1.7 | 0.15 | 11.0 |
| oltp\_read\_only | 34.95 | 2.71 | 13.0 |
| select\_random\_points | 2.91 | 0.28 | 10.0 |
| select\_random\_ranges | 3.96 | 0.3 | 13.0 |
| table\_scan | 147.61 | 35.59 | 4.0 |
| mean |  |  | _9.0_ |

| Write Tests | Dolt | MySQL | Multiple |
| :--- | :--- | :--- | :--- |
| bulk\_insert | 0.001 | 0.001 | 1.0 |
| oltp\_delete | 2.71 | 0.14 | 19.0 |
| oltp\_insert | 8.9 | 2.52 | 4.0 |
| oltp\_read\_write | 62.19 | 6.32 | 10.0 |
| oltp\_update\_index | 10.27 | 2.61 | 4.0 |
| oltp\_update\_non\_index | 7.17 | 2.57 | 3.0 |
| oltp\_write\_only | 30.81 | 3.68 | 8.0 |
| mean |  |  | _7.0_ |

| Overall Mean Multiple | _8.0_ |
| :--- | :--- |
<br/>
