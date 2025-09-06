---
author: Ash
pubDatetime: 2025-03-15T1:20:00Z
title: Data-engineering-101
postSlug: Data-eng 101
featured: true
draft: false
tags:
  - data-engineering
ogImage: ""
description: DATA ENGINEERING 101
---

# Data engineering lingo

This blog contains some commonly use terms in world of data engineering.

<details>
  <summary>Types of data source</summary>
 
<br />
    
    - Structured data source: Data organized as tables of rows and columns.
    
    - Semi-structured data source: Data that is not in tabular form but still have some structure. Ex - JSON, XML
    
    - Unstructured data source: Data that does not have any pre-defined structure. Ex -text, video, audio, images, etc

 </details>
<br>

<details>
    <summary>Types of source system</summary>
<br />

    - Databases: Store data in an organized way, structured or semi-structured

    - Files: Sequence of bytes representing information TXT, png, mp3, csv etc

    - Streaming system - Continuous flow of data, semi structured data. Eg- IOT sensor

</details>
<br>

<details>
<summary>ACID properties</summary>
<br />

    - Atomicity: It ensures that transactions are treated as single individual unit.

    - Consistency:Any changes to the data made within a transaction follow the set of rules or constraints defined by database schema.

    - Isolation: Each transaction is executed in sequential order.

    - Durability: Once a transaction is completed, its effects are permanent and will survive subsequent system failures.

</details>

### What is a data warehouse(storage+compute)?

It is database for analytics and optimized for analytical workloads.
They usually contain structured data so when it comes to unstructured data we use data lake. Storing large amount of uncleaned data can rack up cost pretty fast.
Examples of data warehouse- Snowflake, AWS redshift, microsoft synapse, google bigquery.

### What is datalake(storage layer)?

Typically it a dumping ground for data. It is where data from different source gets stored after going through etl process. It can be used to store data in multiple formats.
It is read only it is where you decide what all high priority data gets to move to data warehouse for analytical purpose.

HIVE brought sql to the data lake. If you store bunch of files inside a folder it will treat folder as a table.

### What is data lakehouse?

A data lakehouse have:
Table format: Apace iceberg
catalog: To discover different tables we have eg. nessie
Query engine: Lets you query in data lake. eg dremio

Essentially a deconstructed data warehouse which can help us save cost.

### What is a table format?

Problem? Storage system like data lake doesn't know relationship between files stored on them. Other tools are not gonna know the just by looking at the files to which table they belong whether table A,B or C as storage system is not aware of it.

Table format allows us to group files into unique datasets so now when a tools comes to data lake it can look at the metadata and know to which table it belongs.

Table format is basically taking the data files that you have and creating metadata on top of it. A metadata is collection of information that make something easier to use. It helps make searching the data more efficient.

Metadata on these file provide?

- What is the schema of these files
- How the files are partitioned
- What are statistics on these fields.

_To be continued.._
