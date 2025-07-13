---
author: Ash
pubDatetime: 2025-06-22T7:20:00Z
title: Airflow 101
postSlug: airflow
featured: true
draft: false
tags:
  - data-engineering
ogImage: ""
description: A beginner's guide to airflow
---

## A bit of foreground before jumping into airflow

If you are here you probably already know airflow is an orchestration tool

<details>
  <summary>But what is orchestration?</summary>
 
<br />
    Data Orchestration is the coordination and automation of data flow across various tools and systems to deliver quality data products and analytics
 </details>
<br>
<details>
  <summary>What modern data orchestration brings to the table?</summary>
 
<br />

- Benefit of pipeline-as-code in python.
- Ability to integrate with hundreds od external systems.
- Time and event based scheduling and finally feature rich software with built-in observability and centralized UI.

 </details>
<br>

Now lets dive into **Apache airflow**

- It is an open-source tool for programmatically authoring, scheduling and monitoring your data pipeline.
- Airflow is designed for batch processing not stream processing. However you can use kafka with airflow
- It is highly scalable provided there is enough resource and infrastructure as the complexity increases.

<details>
  <summary>Keywords</summary>
 
<br />

- DAG: A directed acyclical graph that represents a single data pipeline
- Task: An individual unit of work in a DAG
- Operator: The specific work that a Task performs

 </details>
<br>
<details>
  <summary>Types of operators</summary>
 
<br />

- Assume you are building a DAG and want to run a Python script - Action operator

- Assume you are building a DAG and want to wait for a file to load before executing the next task. - Sensor operator
- Assume you are building a DAG and want to move data from one system or data source to another - Transfer operator
 </details>
<br>

<details>
  <summary>Airflow architecture</summary>
 
<br />

- **API server** - FastAPI server serving UI and handling task execution requests
- **Scheduler**- Schedule tasks when dependencies are fulfilled
- **DAG File Processor**- Dedicated process of parsing DAGs.
- **Metadata Database** - A database where all metadata are stored
- **Executor** - To determine how and where tasks are executed Doesn't execute a task but define where the task is to be executed for eg. kubernetes
- **Queue** - Defines the execution task order
- **Worker**- Process executing the tasks, defined by the executor.It is in charge of executing the logic of a DAG's tasks
- **Triggerer**- Process running asyncio to support deferrable operator
 </details>
<br>

How does airflow run a dag?

- The DAG File Processor constantly scans the DAGs directory for new files. The default time is every 5 minutes.
- After the DAG File Processor detects a new DAG, the DAG is processed and serialized into the metadata database.
- The scheduler checks for DAGs that are ready to run in the metadata database. The default time is every 5 seconds.
- Once a DAG is ready to run, its tasks are put into the executor's queue.
- Once a worker is available, it will retrieve a task to execute from the queue.
- The worker will then execute the task.
- UI gets updates

<details>
  <summary>Core components of Airflow</summary>
 
<br />
  
  - The import statements, where the specific operators or classes that are needed for the DAG are defined.
  - The DAG definition, where the DAG object is called and where specific properties, such as its name or how often you want to run it, are defined.
  - The DAG body, where tasks are defined with the specific operators they will run.
  - The dependencies, where the order of execution of tasks is defined using the right bitshift operator (>>) and the left bitshift operator (<<).

A DAG’s task can be either upstream or downstream to another task.

 </details>
<br>

Time to get hands dirty and install airflow through docker (_my fav_), with astro cli sitting on top. Assuming you have docker installed and setup

Run the following(Linux):

```
curl -sSL install.astronomer.io | sudo bash -s
```

And viola1! Airflow is installed

Verify using below command:

```
astro version
```

Make new folder in your desired location and initialize new airflow project

```
astro dev init
```

To run the airflow instance:

```
astro dev start
```

To stop the airflow instance:

```
astro dev stop
```

To start the airflow instance from scratch

```
astro dev kill
```

Astro creates the following directories upon initialization

<details> 
  <summary>Folder structure</summary>

- The dags directory: Contains Python files corresponding to data pipelines, including examples such as example_dag_advanced and example_dag_basic.
- The include directory: Used for storing files like SQL queries, bash scripts, or Python functions needed in data pipelines to keep them clean and organized.
- The plugins directory: Allows for the customization of the Airflow instance by adding new operators or modifying the UI.
- The tests directory: Contains files for running tests on data pipelines, utilizing tools like the pytest library.
- The .dockerignore file: Describes files and folders to exclude from the Docker image during the build.
- The .env file: Used for configuring Airflow instances via environment variables.
- The .gitignore file: Specifies files and folders to ignore when pushing the project to a git repository, useful for excluding sensitive information like credentials.
- The airflow_settings.yaml file: Stores configurations such as connections and variables to prevent loss when recreating the local development environment.
- The Dockerfile: Used for building the Docker image to run Airflow, with specifications for the Astro runtime Docker image and the corresponding Airflow version.
- The packages.txt file: Lists additional operating system packages to install in the Airflow environment.
- The README file: Provides instructions and information about the project.
</details>
</br>
<details>
  <summary>What is a DAG ?</summary>
  In Airflow, a directed acyclic graph (DAG) is a data pipeline defined in Python code. Each DAG represents a collection of tasks you want to run and is organized to show relationships between tasks in the Airflow UI. The mathematical properties of DAGs make them useful for building data pipelines:

- Directed: If multiple tasks exist, each must have at least one defined upstream or downstream task.
- Acyclic: Tasks cannot have a dependency on themselves. This avoids infinite loops.
- Graph: All tasks can be visualized in a graph structure, with relationships between tasks defined by nodes and vertices.

</details>
<br>

Best practice for defining a DAG:

```bash
from airflow.sdk import dag
from pendulum import datetime

@dag(
        schedule="@daily",
        start_date=datetime(2025, 7, 1),
        description="A DAG that runs daily starting from July 1, 2025.",
        tags=['team_a', 'source_a'],
        max_consecutive_failed_dag_runs=3
)
def my_dag():
    pass

my_dag()
```
