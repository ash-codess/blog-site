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

# Data engineering

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

Understanding the Amazon DynamoDB

DynamoDB database is a key-value store that stores a set of key-value pairs. Let's say you have a set of key-value items where each item represents a product. Each item is characterized by a unique key (product ID) and has a set of corresponding attributes (the value of the key). DynamoDB stores this key-value data in a table where each row contains the attributes of one product and it uses the key to uniquely identify each row. This table is different from relational tables because it's schemaless, which means that neither the attributes nor their data types need to be defined beforehand. Each item can have its own distinct attributes.

For example in the product table that you will create in this section, you will have one item that represents a book (Title, Authors, ISBN, Price) and another item that represents a bicycle (BicycleType, Brand, Price, Color) both stored in the same DynamoDB table.

At peak load dynamodb takes 79.8 million requests per second and about 10 trillion requests daily. It is very easy easy to setup and provides auto-scaling while storing petabytes of data. One of the unique feature of dynamodb is even though it No-sql DB but it comes with ACID grantee, C here means serializable
Provides both eventual and strong consistency.

How to create a table in dynamodb?
We will use dynamodb create_table() method.It requires three parameters.
(TableName,KeySchema, AttributeDefinations)

There is an additional parameter that you can specify if you don't wish to pay for DynamoDB based on demand and you want to choose the provisioned mode:

- `ProvisionedThroughput`: a dictionary that specifies the read/write capacity (or throughput) for a specified table. It consists of two items:
  - `ReadCapacityUnits`: the maximum number of strongly consistent reads consumed per second;
  - `WriteCapacityUnits`: the maximum number of writes consumed per second.
